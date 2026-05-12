Alfabetyczny wykaz wszystkich klas:

Order (Zapotrzebowanie)

    Opis: Encja przechowująca nagłówek zamówienia złożonego przez dany punkt sprzedaży.

    Atrybuty: id (klucz główny), createdAt (data złożenia), status (stan zamówienia: NEW, CONFIRMED, itd.).

    Metody:

        totalPrice(): oblicza łączną wartość całego zamówienia.

        validateOrderTime(): weryfikuje, czy zamówienie zostało złożone przed godziną graniczną (np. 22:00).

OrderItem (Pozycja zamówienia)

    Opis: Klasa szczegółowa łącząca konkretny produkt z ilością w ramach danego zamówienia.

    Atrybuty: id, product (referencja do produktu), quantity (zamówiona ilość).

    Metody:

        calculateSubtotal(): oblicza wartość danej pozycji (cena produktu x ilość).

PointOfSale (Punkt Sprzedaży)

    Opis: Reprezentuje fizyczny sklep lub piekarnię firmową, która generuje popyt i zatrudnia personel.

    Atrybuty: id, name (nazwa punktu), address (lokalizacja dostawy), phone (kontakt).

    Metody:

        generateDailyReport(): tworzy zestawienie sprzedaży dla danego punktu.

        getStaffList(): zwraca listę użytkowników przypisanych do tego punktu.

Product (Produkt)

    Opis: Definicja towaru (pieczywa) dostępnego w ofercie wraz z aktualnym stanem magazynowym po produkcji.

    Atrybuty: id, name, weight (gramatura), price (cena jednostkowa), stockQuantity (dostępna ilość).

    Metody:

        reduceStock(amount): zmniejsza stan po wydaniu towaru do dostawy.

        addStock(amount): zwiększa stan po nocnej produkcji.

Route (Trasa)

    Opis: Harmonogram logistyczny grupujący zamówienia do zrealizowania przez konkretnego kierowcę w danym dniu.

    Atrybuty: id, driver (przypisany User), deliveryDate, orders (lista zamówień/przystanków).

    Metody:

        assignDriver(User): przypisuje kierowcę do trasy.

        calculateRouteDistance(): oblicza dystans trasy w celu optymalizacji kosztów paliwa.

User (Użytkownik)

    Opis: Centralna klasa systemu autoryzacji, definiująca role i uprawnienia pracowników.

    Atrybuty: id, username, password, role (Staff, Driver, Dispatcher).

    Metody:

        login(): proces uwierzytelniania.

        changePassword(): zarządzanie bezpieczeństwem konta.

        hasRole(role): weryfikacja uprawnień do konkretnych modułów systemu.

WasteLog (Rejestr Odpadów)

    Opis: Dokumentuje zwroty niesprzedanego pieczywa i zarządza procesem ich specjalnej utylizacji.

    Atrybuty: id, product, quantity, disposalDate, category (typ utylizacji).

    Metody:

        generateWasteReport(): generuje raport strat i metod utylizacji dla celów analitycznych i ekologicznych.
