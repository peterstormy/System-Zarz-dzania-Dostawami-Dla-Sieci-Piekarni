Dostawa

    Opis: Reprezentuje fizyczny proces transportu pieczywa do punktu.

    Atrybuty: godzinaDostawy (planowana godzina przyjazdu).

    Metody: potwierdzOdbior() (elektroniczne zatwierdzenie dostawy przez kierowcę).

Magazyn

    Opis: Przechowuje informacje o aktualnym stanie produktów w piekarni.

    Atrybuty: stanAktualny (ilość sztuk na stanie).

    Metody: aktualizujStan() (zdejmuje towar po złożeniu zapotrzebowania).

Produkt

    Opis: Obiekt handlowy będący przedmiotem zamówień i zwrotów.

    Atrybuty: gramatura (waga pieczywa), sklad.

    Metody: sprawdzDostepnosc() (weryfikuje czy produkt można zamówić).

Trasa

    Opis: Zbiór punktów sprzedaży uszeregowanych w kolejności dostaw.

    Atrybuty: listaPrzystankow (kolejność sklepów).

    Metody: obliczKilometry() (wyliczanie dystansu dla logistyki).

Zwrot

    Opis: Dokumentacja niesprzedanego pieczywa wracającego do piekarni.

    Atrybuty: powodZwrotu, iloscSztuk.

    Metody: zatwierdzZwrot() (finalizacja procesu przez kierowcę).
