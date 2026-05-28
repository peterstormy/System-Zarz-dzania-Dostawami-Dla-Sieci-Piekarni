# Diagramy sekwencji (przebiegu / interakcji)

---

## Diagram sekwencji 1 — Złożenie zamówienia

**Uczestnicy:** Pracownik, :PunktSprzedaży, :Zapotrzebowanie, :PozycjaZamówienia, :Produkt

### Opis komunikatów

- `złóżZamówienie(produkty)` — Pracownik inicjuje złożenie zamówienia, przekazując listę produktów do PunktuSprzedaży.
- `«create» Zapotrzebowanie()` — PunktSprzedaży tworzy nowy obiekt Zapotrzebowania.
- `weryfikujCzasZamówienia()` — Zapotrzebowanie sprawdza, czy zamówienie zostało złożone przed godziną graniczną.
- `zamówienie przyjęte` — odpowiedź zwrotna do PunktuSprzedaży, gdy zamówienie złożono przed godziną graniczną.
- `błąd: za późno na zamówienie` — odpowiedź zwrotna, gdy zamówienie złożono po godzinie granicznej.
- `odmowa zamówienia` — PunktSprzedaży informuje Pracownika o odrzuceniu zamówienia.
- `PozycjaZamówienia(produkt, ilość) «create»` — dla każdego produktu w zamówieniu tworzony jest obiekt PozycjiZamówienia.
- `zmniejszStanMagazynu(ilość)` — PozycjaZamówienia zleca Produktowi zmniejszenie stanu magazynowego o zamówioną ilość.
- `stan zaktualizowany` — Produkt potwierdza aktualizację stanu magazynowego.
- `błąd: brak w magazynie` — Produkt zgłasza brak wystarczającej ilości towaru w magazynie.
- `pozycja odrzucona` — PozycjaZamówienia informuje o odrzuceniu pozycji z powodu braku towaru.
- `«destroy»` — obiekt PozycjiZamówienia zostaje zniszczony po odrzuceniu.
- `obliczWartośćPozycji()` — PunktSprzedaży żąda obliczenia wartości pozycji zamówienia.
- `łącznaWartość()` — Zapotrzebowanie oblicza łączną wartość zamówienia.
- `zamówienie: Zapotrzebowanie` — zwrócony obiekt zamówienia z łączną wartością.
- `potwierdzenie złożenia` — PunktSprzedaży przekazuje Pracownikowi potwierdzenie złożenia zamówienia.

---

## Diagram sekwencji 2 — Przydzielenie kierowcy i realizacja trasy

**Uczestnicy:** Dyspozytor, :Trasa, :Użytkownik, :Zapotrzebowanie, :Produkt

### Opis komunikatów

- `przydzielKierowcę(kierowca)` — Dyspozytor zleca przydzielenie kierowcy do trasy.
- `maRolę(KIEROWCA)` — Trasa weryfikuje w obiekcie Użytkownika, czy posiada on rolę KIEROWCA.
- `true` — Użytkownik potwierdza posiadanie roli KIEROWCA.
- `kierowca przydzielony` — Trasa informuje Dyspozytora o pomyślnym przydzieleniu kierowcy.
- `false` — Użytkownik zwraca informację o braku wymaganej roli.
- `błąd: brak uprawnień` — Trasa informuje Dyspozytora o braku uprawnień użytkownika.
- `obliczDystansTrasy()` — Dyspozytor zleca obliczenie dystansu trasy.
- `dystans: Integer` — Trasa zwraca obliczony dystans jako liczbę całkowitą.
- `weryfikujCzasZamówienia()` — dla każdego Zapotrzebowania na trasie Trasa weryfikuje status zamówienia.
- `status: boolean` — Zapotrzebowanie zwraca status weryfikacji.
- `zmniejszStanMagazynu(ilość)` — Zapotrzebowanie zleca Produktowi zmniejszenie stanu magazynowego.
- `stan zaktualizowany` — Produkt potwierdza aktualizację stanu.
- `status = W_REALIZACJI` — Zapotrzebowanie aktualizuje swój status na W_REALIZACJI.
- `pomiń zamówienie` — komunikat informujący o pominięciu zamówienia, gdy status nie jest POTWIERDZONE.
- `trasa zrealizowana` — Trasa informuje Dyspozytora o zakończeniu realizacji trasy.

---

## Diagram sekwencji 3 — Zgłoszenie odpadów

**Uczestnicy:** Pracownik, :PunktSprzedaży, :RejestrOdpadów, :Produkt, Dyspozytor

### Opis komunikatów

- `zgłośOdpady(produkt, ilość, kategoria)` — Pracownik zgłasza odpady podając produkt, ilość oraz kategorię odpadów.
- `RejestrOdpadów(produkt, ilość, kategoria) «create»` — PunktSprzedaży tworzy nowy obiekt RejestruOdpadów z podanymi danymi.
- `stanMagazynowy` — RejestrOdpadów odpytuje Produkt o aktualny stan magazynowy.
- `ilość: Integer` — Produkt zwraca aktualną ilość towaru w magazynie.
- `zmniejszStanMagazynu(ilość)` — RejestrOdpadów zleca Produktowi zmniejszenie stanu magazynowego o ilość odpadów.
- `stan zaktualizowany` — Produkt potwierdza aktualizację stanu magazynowego.
- `błąd: niezgodność stanu` — Produkt zgłasza błąd, gdy ilość odpadów przekracza stan magazynowy.
- `generujRaportOdpadów()` — RejestrOdpadów generuje raport odpadów po zakończeniu pętli.
- `raport: RejestrOdpadów` — wygenerowany raport zwracany do PunktuSprzedaży.
- `powiadomienieDyspozytora(raport)` — PunktSprzedaży wysyła raport do Dyspozytora, gdy straty przekraczają próg.
- `potwierdzono powiadomienie` — Dyspozytor potwierdza odbiór powiadomienia.
- `odpady zarejestrowane` — PunktSprzedaży informuje Pracownika o pomyślnym zarejestrowaniu odpadów.
