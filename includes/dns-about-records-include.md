### <a name="record-names"></a>Nazwy rekordów

W usłudze DNS platformy Azure rekordy są określane przy użyciu nazw względnych. A *w pełni kwalifikowana* nazwy domeny (FQDN) zawiera nazwę strefy hello, podczas gdy *względną* nie ma nazwy. Na przykład względna nazwa rekordu "www" w strefie hello "contoso.com" hello nadaje nazwę FQDN rekordu hello "www.contoso.com".

*Wierzchołku* rekord jest rekord DNS w głównym hello (lub *wierzchołku*) strefy DNS. Na przykład w hello strefę DNS "contoso.com" rekord wierzchołku ma również hello w pełni kwalifikowanej nazwy domeny "contoso.com" (jest to czasem nazywane *naked* domeny).  Według Konwencji hello względnej nazwy "@" jest używana toorepresent rekordów na wierzchołku.

### <a name="record-types"></a>Typy rekordów

Każdy rekord DNS ma nazwę i typ. Rekordy są pogrupowane w różne typy według danych toohello, które zawierają. najczęściej spotykanym typem Hello jest "" rekord, który mapuje nazwę tooan adres IPv4. Inny spotykanym typem jest rekord "MX", która mapuje nazwy serwera poczty tooa.

Usługa DNS platformy Azure obsługuje wszystkie popularne typy rekordów DNS: A, AAAA, CNAME, MX, NS, PTR, SOA, SRV i TXT. Należy pamiętać, że [rekordy SPF są reprezentowane przy użyciu rekordu TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Zestawy rekordów

Czasami trzeba toocreate więcej niż jeden rekord DNS o podanej nazwie i typu. Na przykład załóżmy, że witryna sieci web "www.contoso.com" hello znajduje się na dwóch różnych adresów IP. Witaj witryny sieci Web wymaga dwóch różnych rekordów, po jednym dla każdego adresu IP. Oto przykład zestawu rekordów:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

System DNS platformy Azure zarządza wszystkimi rekordami DNS za pomocą *zestawów rekordów*. Zestaw rekordów (znanej także jako *zasobów* zestawu rekordów) kolekcja hello rekordy DNS w strefie, które mają hello takie same nazwy i hello są tego samego typu. Większość zestawów rekordów zawiera jeden rekord. Jednak sytuacje hello jeden powyżej, w którym zestaw rekordów zawiera więcej niż jeden rekord, nie są rzadko.

Na przykład, załóżmy, że utworzono już rekordu A "www" w strefie hello "contoso.com", wskazując toohello IP adresów "134.170.185.46" (hello pierwszy rekord powyżej).  toocreate hello drugi rekord, który należy dodać wykaz istniejącego rekordu toohello ustawić, zamiast tworzyć dodatkowe zestawu rekordów.

Witaj SOA i typy rekordów CNAME stanowią wyjątki. Standardy usługi DNS Hello nie zezwalają na występowanie wielu rekordów z hello takie same nazwy dla tych typów, w związku z tym tych zestawów rekordów mogą zawierać tylko jeden rekord.
