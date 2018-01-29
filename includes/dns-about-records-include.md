### <a name="record-names"></a>Nazwy rekordów

W usłudze DNS platformy Azure rekordy są określane przy użyciu nazw względnych. *W pełni kwalifikowana* nazwa domeny (FQDN) zawiera nazwę strefy, której nie zawiera nazwa *względna*. Na przykład względna nazwa rekordu „www” w strefie „contoso.com” daje w pełni kwalifikowaną nazwę rekordu www.contoso.com.

Rekord *wierzchołka* to rekord DNS w katalogu głównym (*wierzchołku*) strefy DNS. Na przykład w strefie DNS „contoso.com” rekord wierzchołka ma także w pełni kwalifikowaną nazwę „contoso.com” (jest to czasami nazywane *samą* domeną).  Zgodnie z konwencją nazwa względna '@' jest używana do reprezentowania rekordów wierzchołków.

### <a name="record-types"></a>Typy rekordów

Każdy rekord DNS ma nazwę i typ. Rekordy są pogrupowane w różne typy według danych, które zawierają. Najczęściej spotykanym typem jest rekord „A”, który mapuje nazwę na adres IPv4. Innym często spotykanym typem jest rekord „MX”, który mapuje nazwę na serwer poczty e-mail.

Usługa Azure DNS obsługuje wszystkie popularne typy rekordów DNS: A, AAAA, CAA, CNAME, MX, NS, PTR, SOA, SRV i TXT. Należy pamiętać, że [rekordy SPF są reprezentowane przy użyciu rekordu TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Zestawy rekordów

Czasami trzeba utworzyć więcej niż jeden rekord DNS określonego typu o danej nazwie. Na przykład załóżmy, że witryna sieci Web „www.contoso.com” jest hostowana pod dwoma różnymi adresami IP. Witryna sieci Web wymaga dwóch różnych rekordów A, po jednym dla każdego adresu IP. Oto przykład zestawu rekordów:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

System DNS platformy Azure zarządza wszystkimi rekordami DNS za pomocą *zestawów rekordów*. Zestaw rekordów (określany także jako zestaw rekordów *zasobów*) jest kolekcją rekordów DNS w strefie, które mają taką samą nazwę i są tego samego typu. Większość zestawów rekordów zawiera jeden rekord. Sytuacje taka jak powyższa, w których zestaw rekordów zawiera więcej niż jeden rekord, również mają często miejsce.

Na przykład załóżmy, że utworzono wcześniej rekord A „www” w strefie „contoso.com” wskazujący na adres IP „134.170.185.46” (pierwszy rekord powyżej).  W celu utworzenia drugiego rekordu ten rekord zostanie dodany do istniejącego zestawu rekordów zamiast tworzenia dodatkowego zestawu rekordów.

Typy rekordów SOA i CNAME stanowią wyjątki. Standardy systemu DNS nie zezwalają na występowanie wielu rekordów tych typów o takiej samej nazwie, w związku z czym te zestawy rekordów mogą zawierać tylko jeden rekord.