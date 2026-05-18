# Diagram - Stan Zamówienia

Proces rozpoczyna się od stanu początkowego, po którym zamówienie przechodzi do stanu "nowe". Oznacza to, że użytkownik utworzył nowe zamówienie w systemie. Następnie wykonywana jest operacja submitOrder(), która powoduje przejście do stanu "weryfikowane".

Wtedy system sprawdza poprawność danych zamówienia. Weryfikowana jest:
- godzina złożenia zamówienia,
- dostępność produktów,
- liczba zamówionych chlebów.

Zamówienie zostaje odrzucone, jeśli:
- zostało złożone po godzinie 22:00,
- liczba chlebów przekracza 40 sztuk,
- liczba chlebów nie jest podzielna przez 5 (pakowanie w skrzynki po 5),
- brakuje produktów w magazynie.

W takim przypadku zamówienie przechodzi do stanu "odrzucone", a system wykonuje akcję powiadomienie() informującą użytkownika o odrzuceniu zamówienia.

Jeżeli dane są poprawne, zamówienie przechodzi do stanu "potwierdzone". Następnie wykonywana jest operacja startPicking(), która rozpoczyna kompletowanie produktów w magazynie i zmienia stan zamówienia na "kompletowane".

Po przygotowaniu zamówienia wykonywana jest operacja assignRoute(), oznaczająca przypisanie trasy i kierowcy do dostawy. Zamówienie przechodzi wtedy do stanu "w trasie".

Po dostarczeniu produktów do punktu sprzedaży wykonywana jest operacja confirmDelivery(), która zmienia stan zamówienia na "dostarczone". Następnie operacja closeOrder() kończy proces realizacji zamówienia i ustawia stan "zrealizowane".

Diagram przewiduje również możliwość anulowania zamówienia za pomocą operacji anuluj(). Zamówienie może zostać anulowane zarówno przed potwierdzeniem, jak i podczas kompletowania. W takim przypadku przechodzi do stanu "anulowane", który kończy jego cykl życia.