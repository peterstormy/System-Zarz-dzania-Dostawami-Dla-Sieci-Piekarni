# Opisy tekstowe diagramów stanów

---

# 1. Diagram stanu Zamówienie

## Opis diagramu

Diagram przedstawia cykl życia obiektu `Order` (zamówienie) w systemie zarządzania dostawami dla sieci piekarni. Pokazuje kolejne stany, przez które przechodzi zamówienie – od momentu jego utworzenia, poprzez weryfikację i realizację, aż do zakończenia procesu lub anulowania zamówienia.

Proces rozpoczyna się od stanu początkowego, po którym zamówienie przechodzi do stanu `nowe`. Oznacza to, że użytkownik utworzył nowe zamówienie w systemie. Następnie wykonywana jest operacja `submitOrder()`, która powoduje przejście do stanu `weryfikowane`.

W stanie `weryfikowane` sprawdzana jest poprawność danych zamówienia. System weryfikuje godzinę złożenia zamówienia, dostępność produktów oraz poprawność liczby zamówionych chlebów.

Zamówienie zostaje odrzucone, jeśli:
- zostało złożone po godzinie 22:00,
- liczba zamówionych chlebów jest mniejsza niż 40,
- liczba chlebów nie jest podzielna przez 5,
- produkty są niedostępne w magazynie.

Jeżeli dane są poprawne, zamówienie przechodzi do stanu `potwierdzone`. Następnie rozpoczyna się kompletowanie produktów, przygotowanie dostawy oraz realizacja transportu.

Po dostarczeniu produktów do punktu sprzedaży wykonywane jest potwierdzenie odbioru, a zamówienie przechodzi do stanu `zrealizowane`.

Diagram przewiduje również możliwość anulowania zamówienia przed rozpoczęciem dostawy.

---

## Opis elementów diagramu

| Element | Opis |
|---|---|
| Stan początkowy | Rozpoczęcie procesu obsługi zamówienia |
| `nowe` | Utworzenie nowego zamówienia |
| `weryfikowane` | Sprawdzanie poprawności zamówienia |
| `odrzucone` | Zamówienie nie spełnia warunków biznesowych |
| `potwierdzone` | Zamówienie zostało zaakceptowane |
| `kompletowane` | Produkty są przygotowywane w magazynie |
| `w trasie` | Zamówienie jest dostarczane |
| `dostarczone` | Produkty zostały dostarczone |
| `zrealizowane` | Proces zamówienia został zakończony |
| `anulowane` | Zamówienie zostało anulowane |
| Stan końcowy | Zakończenie procesu zamówienia |

---

# 2. Diagram stanu – Trasa dostawy

## Opis diagramu

Diagram przedstawia cykl życia obiektu `Trasa` w systemie zarządzania dostawami dla sieci piekarni. Diagram pokazuje kolejne etapy przygotowania i realizacji dostawy.

Proces rozpoczyna się od utworzenia nowej trasy przez system. Trasa przechodzi wtedy do stanu `utworzona`. Następnie wykonywane jest planowanie trasy dostawy oraz wyznaczenie kolejności punktów odbioru.

Po zaplanowaniu trasy system przypisuje kierowcę do realizacji dostawy. Trasa przechodzi wtedy do stanu `przypisano kierowcę`.

Kolejnym etapem jest załadunek produktów do pojazdu oraz rozpoczęcie realizacji dostawy. W trakcie realizacji kierowca dostarcza produkty do punktów sprzedaży.

Po dostarczeniu wszystkich zamówień trasa przechodzi do stanu `zakończona`.

Diagram przewiduje również możliwość anulowania trasy z powodu:
- braku kierowcy,
- awarii pojazdu,
- problemów logistycznych.

---

## Opis elementów diagramu

| Element | Opis |
|---|---|
| Stan początkowy | Rozpoczęcie procesu tworzenia trasy |
| `utworzona` | Utworzenie nowej trasy dostawy |
| `zaplanowana` | Wyznaczenie harmonogramu dostaw |
| `przypisano kierowcę` | Do trasy przypisano kierowcę |
| `załadowana` | Produkty zostały załadowane do pojazdu |
| `w realizacji` | Kierowca realizuje dostawy |
| `zakończona` | Wszystkie dostawy zostały wykonane |
| `anulowana` | Trasa została anulowana |
| `archiwizowana` | Zakończona trasa została zarchiwizowana |
| Stan końcowy | Zakończenie procesu realizacji trasy |

---

# 3. Diagram stanu – Rejestr odpadów

## Opis diagramu

Diagram przedstawia cykl życia obiektu `Odpady` (rejestr odpadów) w systemie zarządzania dostawami dla sieci piekarni. Diagram opisuje proces zgłaszania, weryfikacji oraz utylizacji niesprzedanego lub uszkodzonego pieczywa.

Proces rozpoczyna się od zgłoszenia odpadów przez pracownika punktu sprzedaży lub magazynu. Obiekt przechodzi wtedy do stanu `zgłoszony`.

Następnie wykonywana jest weryfikacja poprawności danych zgłoszenia. Sprawdzana jest ilość produktów, poprawność kategorii odpadu oraz zgodność danych magazynowych.

Jeżeli zgłoszenie zawiera błędy, przechodzi do stanu `odrzucony`, a proces zostaje zakończony.

Po poprawnej weryfikacji odpady zostają zakwalifikowane do odpowiedniego sposobu utylizacji. Następnie produkty są przekazywane do utylizacji i wpis przechodzi do stanu `zutylizowany`.

Ostatnim etapem procesu jest archiwizacja wpisu w systemie.

---

## Opis elementów diagramu

| Element | Opis |
|---|---|
| Stan początkowy | Rozpoczęcie procesu obsługi odpadów |
| `zgłoszony` | Utworzenie zgłoszenia odpadu |
| `zweryfikowany` | Potwierdzenie poprawności zgłoszenia |
| `zakwalifikowany do utylizacji` | Określenie sposobu utylizacji |
| `zutylizowany` | Produkty zostały zutylizowane |
| `zarchiwizowany` | Wpis został zapisany w archiwum |
| `odrzucony` | Zgłoszenie zostało odrzucone |
| Stan końcowy | Zakończenie procesu obsługi odpadów |
