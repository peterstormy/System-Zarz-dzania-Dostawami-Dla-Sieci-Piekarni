# Diagram Wdrożenia — System Zarządzania Dostawami Dla Sieci Piekarni

## Opis

Diagram wdrożenia przedstawia fizyczną architekturę systemu — rozmieszczenie komponentów na węzłach sprzętowych oraz sposoby ich komunikacji. Diagram obejmuje urządzenia klientów, serwery aplikacyjne, infrastrukturę danych, serwisy zewnętrzne oraz powiązania między nimi z uwzględnieniem protokołów komunikacyjnych i udostępnianych interfejsów.

---

## Węzły i artefakty

### Serwer Aplikacyjny

Centralny węzeł systemu zawierający dwa artefakty:

- **NGINX (Load Balancer / Reverse Proxy)** — przyjmuje wszystkie żądania przychodzące z zewnątrz i kieruje je do warstwy aplikacyjnej. Odpowiada za terminację TLS, równoważenie obciążenia oraz ochronę warstwy aplikacyjnej przed bezpośrednią ekspozycją na sieć publiczną. Udostępnia interfejs `IRestAPI`.

- **Spring Boot (REST API)** — realizuje logikę biznesową systemu. Obsługuje zarządzanie zamówieniami, trasami i dostawami, generowanie raportów oraz koordynację komunikacji z pozostałymi węzłami systemu.

### Baza Danych

Węzeł przechowywania danych zawierający:

- **PostgreSQL** — główna relacyjna baza danych systemu. Przechowuje dane o zamówieniach, dostawach, trasach, użytkownikach i raportach. Udostępnia interfejs `IZapytaniaDB`.

- **Redis** — baza klucz-wartość działająca jako pamięć podręczna. Redukuje liczbę zapytań do PostgreSQL przez przechowywanie często używanych danych w pamięci operacyjnej. Udostępnia interfejs `ICache`.

### Serwer Powiadomień

Węzeł odpowiedzialny za wysyłanie powiadomień do użytkowników systemu:

- **SMTP Mail Server** — serwer poczty wychodzącej obsługujący wysyłkę wiadomości e-mail (potwierdzenia zamówień, powiadomienia o statusie dostawy, raporty). Udostępnia interfejs `IMailSend`.

- **SMS Gateway** — bramka SMS wysyłająca wiadomości tekstowe do kierowców (przydzielenie trasy, zmiany harmonogramu, alerty). Udostępnia interfejs `ISMSSend`.

### Serwer Backupu

Węzeł przechowujący kopie zapasowe danych. Połączony z węzłem Baza Danych przez sieć lokalną.

- **Kopie zapasowe PostgreSQL** — cykliczne zrzuty bazy danych realizowane przez narzędzie pg_dump. Artefakt korzysta z interfejsu `IZapytaniaDB` w celu odczytu danych do archiwizacji.

### `<<device>>` Urządzenie Klienta

Urządzenie końcowe (komputer, tablet lub telefon) używane przez kierownika piekarni, dyspozytora lub zamawiającego.

- **Aplikacja Klienta** — interfejs użytkownika umożliwiający składanie zamówień, przeglądanie statusu dostaw oraz zgłaszanie reklamacji. Komunikuje się z systemem przez interfejs `IRestAPI`.

### `<<device>>` Telefon Dostawcy

Urządzenie mobilne używane przez kuriera podczas realizacji dostawy.

- **Aplikacja Kuriera** — aplikacja mobilna prezentująca trasę dostawy i listę punktów do obsługi. Korzysta z interfejsu `IRestAPI` do synchronizacji statusów oraz z interfejsu `ITrasa` do wyświetlania nawigacji.

### `<<external>>` Google Maps API

Zewnętrzna usługa mapowa dostarczana przez Google, integrowana z systemem przez sieć publiczną.

- **Maps REST API** — punkt końcowy API Google Maps służący do wyznaczania i optymalizacji tras dostawy. Udostępnia interfejs `ITrasa`.

---

## Interfejsy

Interfejsy udostępniane (notacja lollipop) definiują kontrakty komunikacyjne między artefaktami. Komponent udostępniający interfejs oznaczony jest kółkiem na końcu linii; komponenty korzystające z interfejsu łączą się z nim przerywaną strzałką.

| Interfejs | Udostępnia | Używają |
|---|---|---|
| `IZapytaniaDB` | PostgreSQL | Spring Boot, Kopie zapasowe PostgreSQL |
| `ICache` | Redis | Spring Boot |
| `IMailSend` | SMTP Mail Server | Spring Boot |
| `ISMSSend` | SMS Gateway | Spring Boot |
| `IRestAPI` | NGINX | Aplikacja Klienta, Aplikacja Kuriera |
| `ITrasa` | Maps REST API | Spring Boot, Aplikacja Kuriera |

---

## Połączenia między węzłami

Linie ciągłe między węzłami reprezentują fizyczne kanały komunikacji z podanym protokołem.

| Węzeł A | Węzeł B | Protokół |
|---|---|---|
| Urządzenie Klienta | Serwer Aplikacyjny | HTTPS |
| Telefon Dostawcy | Serwer Aplikacyjny | HTTPS |
| Serwer Aplikacyjny | Baza Danych | JDBC |
| Serwer Aplikacyjny | Serwer Powiadomień | SMTP/HTTP |
| Serwer Aplikacyjny | Google Maps API | Internet |
| Baza Danych | Serwer Backupu | LAN |
