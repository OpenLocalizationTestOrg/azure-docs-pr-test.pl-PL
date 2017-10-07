---
title: "aaaDNS strefy i rejestruje Przegląd - usługi Azure DNS | Dokumentacja firmy Microsoft"
description: "Przegląd pomocy technicznej do hostowania strefy DNS i rekordy DNS firmy Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Przegląd stref DNS i rekordów

Ta strona zawiera wyjaśnienie założeń klucza hello domen, strefy DNS i rekordy DNS i zestawy rekordów i jak są one obsługiwane w usłudze Azure DNS.

## <a name="domain-names"></a>Nazwy domen

Witaj System nazw domen jest hierarchią domen. Hierarchia Hello rozpoczyna się od domeny "główny" hello, której nazwa to po prostu "**.**".  Poniżej są domeny najwyższego poziomu, takie jak „com”, „net”, „org”, „uk” lub „jp”.  Pod nimi są domeny drugiego poziomu, takie jak „org.uk” lub „co.jp”. Witaj domen w hierarchii DNS hello są globalnie rozproszone, hostowane przez serwery DNS na całym świecie hello.

Rejestratora nazw domen jest organizacją, która pozwala toopurchase nazwy domeny, takie jak "contoso.com".  Zakup hello prawo toocontrol hello DNS hierarchię w ramach tej samej nazwie, na przykład umożliwiając toodirect tooyour hello nazwy "www.contoso.com" firmowa witryna sieci web zapewnia nazwę domeny. Rejestrator Hello może obsługiwać domeny hello w jego własnej nazwy serwerów w Twoim imieniu lub pozwalają toospecify alternatywnej nazwy serwerów.

Usługa Azure DNS zawiera nazwę globalnie rozproszone, wysokiej dostępności infrastruktury serwera, które można użyć toohost domeny. Hosting domeny w usłudze Azure DNS, można zarządzać rekordami DNS z hello tego samego poświadczeń, interfejsy API narzędzia, rozliczeń i pomocy technicznej, jak innymi usługami Azure.

Usługa Azure DNS nie obsługuje obecnie zakupów nazw domen. Jeśli chcesz toopurchase nazwę domeny, należy toouse rejestratora nazw domen innych firm. Rejestrator Hello zazwyczaj pobiera małych opłata. następnie Hello domeny może być hostowana w usłudze Azure DNS zarządzania rekordów DNS. Zobacz [delegować tooAzure domeny DNS](dns-domain-delegation.md) szczegółowe informacje.

## <a name="dns-zones"></a>Strefy DNS

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>Rekordy DNS

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Czas wygaśnięcia

czas Hello toolive lub TTL, określa, jak długo każdy rekord jest buforowany przez klientów przed ponownym uruchomieniem zapytania. W hello powyżej przykładzie hello TTL jest 3600 sekund lub 1 godzina.

W usłudze Azure DNS, powitalne czas wygaśnięcia jest określany dla zestawu rekordów hello, a nie dla każdego rekordu, a więc hello tę samą wartość jest używana dla wszystkich rekordów w tym rekordzie Ustaw.  Można określić dowolną wartość TTL od 1 do 2 147 483 647 sekund.

### <a name="wildcard-records"></a>Symbol wieloznaczny rekordów

Usługa DNS platformy Azure obsługuje [rekordy z użyciem symboli wieloznacznych](https://en.wikipedia.org/wiki/Wildcard_DNS_record). Symbol wieloznaczny rekordy są zwracane w odpowiedzi tooany zapytania o zgodnej nazwie (chyba że istnieje lepsze dopasowanie pochodzące zestawu rekordów bez symboli wieloznacznych). Usługa DNS platformy Azure obsługuje zestawy rekordów z użyciem symboli wieloznacznych dla wszystkich typów rekordów z wyjątkiem NS i SOA.

toocreate rekord symbolu wieloznacznego ustawić, użyj nazwy zestawu rekordów hello "\*". Można również również użyć nazwy z '\*"jako jego skrajnej lewej etykiecie, na przykład"\*.foo ".

### <a name="cname-records"></a>Rekordy CNAME

Zestawy rekordów CNAME nie mogą współistnieć z innymi zestawami rekordów o hello takie same nazwy. Na przykład nie można utworzyć zestawu z hello nazwie względnej "www" rekordów CNAME i A zarejestrować hello nazwie względnej "www" na powitania takie same czasu.

Ponieważ hello wierzchołku strefy (nazwa = "@") zawsze zawiera rekordów NS i SOA hello zestawy, które zostały utworzone podczas tworzenia strefy hello, nie można utworzyć zestawu rekordów CNAME w wierzchołku strefy hello.

Te ograniczenia wynikają z hello standardy usługi DNS i nie są ograniczenia usługi Azure DNS.

### <a name="ns-records"></a>Rekordy NS

zestaw rekordów Hello NS w wierzchołku strefy hello (nazwy "@") jest tworzony automatycznie w każdej strefie DNS i usuwane automatycznie po usunięciu hello strefy (nie można go usunąć osobno).

Ten zestaw rekordów zawiera nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy. Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS. Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów. Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS. 

Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello. Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) można tworzyć, modyfikować i usunięte bez ograniczeń.

### <a name="soa-records"></a>Rekordów SOA

Zestaw rekordów SOA jest tworzony automatycznie w wierzchołku hello każdej strefy (nazwa = "@") i usuwane automatycznie po usunięciu hello strefy.  Rekordów SOA nie można utworzyć ani usunąć oddzielnie.

Można zmodyfikować wszystkie właściwości hello rekord SOA, z wyjątkiem właściwości "host" hello, która jest wstępnie skonfigurowane toorefer toohello podstawowa nazwa podana nazwa serwera przez usługę Azure DNS.

### <a name="spf-records"></a>Rekordy SPF

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>Rekordy SRV

[Rekordy SRV](https://en.wikipedia.org/wiki/SRV_record) są używane przez różne lokalizacje serwera toospecify usług. Podczas określania rekordów SRV w usłudze Azure DNS:

* Witaj *usługi* i *protokołu* musi być określony jako część nazwy zestawu rekordów hello, prefiksem znaki podkreślenia.  Na przykład "\_sip.\_ TCP.name ".  Dla rekord w wierzchołku strefy hello, nie istnieje żadne toospecify potrzeby "@" w nazwie rekordu hello, po prostu użyć hello usługę i protokół, na przykład "\_sip.\_ TCP ".
* Witaj *priorytet*, *wagi*, *portu*, i *docelowej* są określone jako parametry każdego rekordu w zestawie rekordów hello.

### <a name="txt-records"></a>Rekordów TXT

Rekordów TXT są używane toomap domeny nazwy tooarbitrary ciągi. Są one używane przez różne aplikacje, w szczególności pokrewne tooemail konfiguracji, np. hello [Framework zasad nadawcy (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) i [DomainKeys zidentyfikowane poczty (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

Standardy usługi DNS Hello zezwolenie na jednym toocontain rekordu TXT wielu ciągów, z których każdy może być aktywne too254 znaków. W przypadku wielu ciągów są łączone przez klientów i traktowane jako pojedynczy ciąg.

Podczas wywoływania metody hello API REST usługi Azure DNS, należy toospecify każdy ciąg TXT oddzielnie.  Korzystając z portalu Azure hello, interfejsy programu PowerShell lub interfejsu wiersza polecenia należy określić pojedynczy ciąg na rekord, który automatycznie jest podzielony na segmenty 254 znaków, jeśli to konieczne.

Witaj, który nie należy mylić wielu ciągów w rekordzie DNS z hello wiele rekordów TXT w zestawie rekordów TXT.  Zestaw rekordów TXT może zawierać wiele rekordów *z których każdy* może zawierać wielu ciągów.  Usługa DNS platformy Azure obsługuje długość ciągu całkowita się too1024 znaków wszystkich rekordów TXT (we wszystkich rekordów połączone).

## <a name="tags-and-metadata"></a>Znaczniki i metadane

### <a name="tags"></a>Tagi

Znaczniki są listą par nazwa wartość i są używane przez usługi Azure Resource Manager toolabel zasobów.  Usługa Azure Resource Manager używa tagów tooenable filtrowane widoki rachunku Azure i pozwala również tooset zasad na jakie znaczniki są wymagane. Aby uzyskać więcej informacji na temat tagów, zobacz [używanie tagów tooorganize zasobów platformy Azure](../azure-resource-manager/resource-group-using-tags.md).

Usługa DNS platformy Azure obsługuje przy użyciu usługi Azure Resource Manager tagów zasobów strefy DNS.  Nie obsługuje tagi zestawów rekordów DNS, mimo że jako alternatywę "metadanych" jest obsługiwana na zestawów rekordów DNS, jak wyjaśniono poniżej.

### <a name="metadata"></a>Metadane

Jako alternatywne toorecord ustawia tagi, usługi DNS platformy Azure obsługuje dodawanie adnotacji do zestawów rekordów przy użyciu "metadanych".  Podobne tootags metadanych umożliwia możesz tooassociate pary nazwa wartość z każdego zestawu rekordów.  Może to być przydatne, na przykład ustawić cel hello toorecord każdego rekordu.  W przeciwieństwie do tagów metadane nie może być używane tooprovide filtrowany widok rachunku Azure i nie można określić w zasadach usługi Azure Resource Manager.

## <a name="etags"></a>Elementy etag

Załóżmy, że dwie osoby lub dwoma procesami spróbuj toomodify rekordu DNS na powitania sam czas. Który wins? I będzie wygrał użytkownik hello wiadomo, że zostały one zastąpione zmiany utworzone przez innego użytkownika?

Usługa Azure DNS korzysta elementy etag toohandle równoczesnych zmian toohello tego samego zasobu bezpiecznie. Elementy etag są niezależne od [usługi Azure Resource Manager "Tagi"](#tags). Każdy zasób DNS (strefy lub zestawu rekordów) ma element Etag skojarzone z nim. Zawsze, gdy zasób jest pobierana, również są pobierane jego Etag. Podczas aktualizowania zasobu, możesz wybrać ponownie toopass hello Etag dzięki usłudze Azure DNS można zweryfikować tego hello Etag na powitania serwera dopasowań. Ponieważ każdy zasób tooa aktualizacji powoduje hello Etag ponownie generowane, element etag wskazuje, że nastąpiła zmiana współbieżnych. Elementy etag można również podczas tworzenia nowego tooensure zasobu, który zasób hello już nie istnieje.

Domyślnie programu PowerShell usługi Azure DNS korzysta toozones równoczesnych zmian tooblock elementy etag i zestawy rekordów. opcjonalne Hello *-zastąpić* przełącznika może być używane toosuppress kontroli Etag, w tym przypadku wszystkie równoczesnych zmian zostaną zastąpione.

Na poziomie hello hello API REST usługi Azure DNS elementy etag określono korzystanie z nagłówków HTTP.  Ich zachowanie znajduje się w poniższej tabeli hello:

| Nagłówek | Zachowanie |
| --- | --- |
| Brak |Umieść zawsze powiedzie się (nie są sprawdzane Etag) |
| IF-match<etag> |Umieść powiedzie się tylko, jeśli zasób istnieje i element Etag odpowiada |
| IF-match * |Umieść powiedzie się tylko, jeśli istnieje zasób |
| IF-none-match * |Umieść powiedzie się tylko, jeśli zasób nie istnieje. |


## <a name="limits"></a>Limity

następujące domyślne limity Hello się przy użyciu usługi Azure DNS:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Następne kroki

* toostart przy użyciu usługi Azure DNS, Dowiedz się, jak za[utworzyć strefę DNS](dns-getstarted-create-dnszone-portal.md) i [utworzyć rekordy DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate istniejącej strefy DNS, Dowiedz się, jak za[importowanie i eksportowanie pliku strefy DNS](dns-import-export.md).
