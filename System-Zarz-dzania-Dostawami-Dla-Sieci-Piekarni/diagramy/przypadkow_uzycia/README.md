Opisy tekstowe wszystkich aktorów:

1. Pracownik Punktu (Aktor Biznesowy)

        Charakterystyka: Użytkownik operacyjny odpowiedzialny za punkt sprzedaży.
    
        Główne zadania: Inicjuje procesy logistyki „push” (zgłaszanie zwrotów) oraz „pull” (zapotrzebowanie na towar).
    
        Odpowiedzialność: Zapewnienie ciągłości sprzedażowej poprzez precyzyjne określenie potrzeb asortymentowych oraz rzetelne rozliczanie zwrotów.

2. Kierowca (Aktor Operacyjny)

        Charakterystyka: Użytkownik mobilny realizujący fizyczny obieg towaru.
    
        Główne zadania: Walidacja stanów fizycznych ze stanem systemowym podczas odbioru zwrotów oraz dostarczanie danych telemetrycznych (lokalizacja/status).
    
        Odpowiedzialność: Zgodność fizyczna odebranego towaru oraz informowanie systemu o postępach na trasie.

3. Dyspozytor (Aktor Nadzorczy)

        Charakterystyka: Użytkownik szczebla koordynacyjnego.
    
        Główne zadania: Monitoring procesów w czasie rzeczywistym, analiza odchyleń (opóźnienia) oraz odbiór danych zagregowanych do celów produkcyjnych.
    
        Odpowiedzialność: Optymalizacja logistyki i nadzór nad terminowością realizacji do


1. Opis przypadku użycia: „Złożenie zapotrzebowania na towar”

1.1. Uczestniczący aktorzy

    Pracownik Punktu

    Dyspozytor (jako odbiorca danych w systemie)

1.2. Podstawowy ciąg zdarzeń

    System wyświetla formularz zapotrzebowania.

    Pracownik Punktu wpisuje ilości zamawianego pieczywa.

    System automatycznie wywołuje przypadek użycia Aktualizacja stanów magazynowych (relacja <<include>>), aby zarezerwować towar.

    Pracownik zatwierdza zapotrzebowanie.

    System weryfikuje poprawność danych i dostępność na magazynie.

    System zapisuje zapotrzebowanie w rejestrze.

    System informuje o pomyślnym wysłaniu danych.

1.3. Alternatywne ciągi zdarzeń

    a) Brak towaru w magazynie: System wyświetla komunikat o braku i prosi o korektę ilości.

    b) Anulowanie: Pracownik klika „Anuluj”, system wraca do menu głównego bez zapisu.

1.4. Zależności czasowe

    Częstotliwość: raz dziennie na punkt.

    Czas realizacji: ~2 min.

1.5. Wartości uzyskiwane przez aktorów

    Potwierdzenie przyjęcia zamówienia do produkcji.

    Aktualny stan zapasów w systemie.

2. Opis przypadku użycia: „Rejestracja odbioru zwrotów”

2.1. Uczestniczący aktorzy

    Kierowca

    Pracownik Punktu (dostarczający dane o zwrotach)

2.2. Podstawowy ciąg zdarzeń

    Kierowca wybiera punkt na trasie.

    System wywołuje przypadek użycia Zgłoszenie zwrotów niesprzedanego pieczywa (relacja <<include>>), aby pobrać listę zwrotów przygotowaną przez Pracownika.

    Kierowca przelicza fizycznie towar i potwierdza zgodność z systemem.

    System zapisuje dane o odebranych zwrotach.

    System informuje o zakończeniu operacji.

2.3. Alternatywne ciągi zdarzeń

    a) Błędna ilość: Kierowca zgłasza rozbieżność, system pozwala na edycję ilości (jeśli system na to pozwala w logice biznesowej).

2.4. Zależności czasowe

    Częstotliwość: przy każdej dostawie (rano).

    Czas realizacji: ~1 min.

2.5. Wartości uzyskiwane przez aktorów

    Zwolnienie punktu z odpowiedzialności za niesprzedany towar.

    Dane o stratach gotowe do analizy.

3. Opis przypadku użycia: „Monitorowanie statusu tras”

3.1. Uczestniczący aktorzy

    Dyspozytor

    Kierowca (jako dostawca sygnału GPS/statusu)

3.2. Podstawowy ciąg zdarzeń

    System wyświetla mapę lub listę z aktualnym położeniem wszystkich kierowców.

    System odświeża statusy dostaw (np. „w drodze”, „dostarczono”) w czasie rzeczywistym.

    Dyspozytor obserwuje postęp prac.

3.3. Alternatywne ciągi zdarzeń

    a) Wystąpienie problemu na trasie: Wywoływany jest przypadek użycia Wyświetlanie szczegółów opóźnienia i lokalizacji (relacja <<extend>>), jeśli system wykryje przestój lub Kierowca zgłosi błąd.

3.4. Zależności czasowe

    Częstotliwość: ciągła w godzinach pracy logistyki.

3.5. Wartości uzyskiwane przez aktorów

    Pełna kontrola nad terminowością dostaw.
