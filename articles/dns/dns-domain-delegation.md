---
title: "Omówienie delegowania DNS na platformie Azure | Microsoft Docs"
description: "Dowiedz się, jak zmienić delegowanie domeny i korzystać z serwerów nazw usługi Azure DNS do zapewniania hostingu domeny."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 31a500502a4d3e729ecb79929ed6c1de156d6259
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegowanie stref DNS za pomocą usługi Azure DNS

Usługa Azure DNS umożliwia hostowanie strefy DNS i zarządzanie rekordami DNS dla domeny na platformie Azure. Aby zapytania DNS dla domeny miały dostęp do usługi Azure DNS, należy delegować domenę do usługi Azure DNS z domeny nadrzędnej. Należy pamiętać, że usługa Azure DNS nie jest rejestratorem domen. W tym artykule wyjaśniono, jak działa delegowanie domeny i jak delegować domeny do usługi Azure DNS.

## <a name="how-dns-delegation-works"></a>Jak działa delegowanie DNS

### <a name="domains-and-zones"></a>Domeny i strefy

System nazw domen (DNS, Domain Name System) jest hierarchią domen. Hierarchia rozpoczyna się od domeny głównej, której nazwa to po prostu „**.**”.  Poniżej są domeny najwyższego poziomu, takie jak „com”, „net”, „org”, „uk” lub „jp”.  Pod tymi domenami najwyższego poziomu są domeny drugiego poziomu, takie jak „org.uk” lub „co.jp”.  I tak dalej. Domeny w hierarchii DNS są hostowane przy użyciu osobnych stref DNS. Te strefy są globalnie rozproszone, hostowane przez serwery DNS na całym świecie.

**Strefa DNS** — Domena jest unikatową nazwą w systemie nazw domen, na przykład „contoso.com”. Strefa DNS jest używana do hostowania rekordów DNS dla określonej domeny. Na przykład domena „contoso.com” może zawierać wiele rekordów DNS, takich jak „mail.contoso.com” (dla serwera poczty) i „www.contoso.com” (dla witryny sieci Web).

**Rejestrator domen** — Rejestrator domen to firma, która może udostępniać nazwy domen internetowych. Weryfikuje ona, czy domena internetowa, której chcesz używać, jest dostępna, i umożliwi jej zakupienie. Po zarejestrowaniu nazwy domeny jesteś jej prawnym właścicielem. Jeśli masz już domenę internetową, będziesz korzystać z bieżącego rejestratora domeny do delegowania jej do usługi Azure DNS.

Aby dowiedzieć się, kto jest właścicielem danej nazwy domeny lub uzyskać informacje o tym, jak kupić domenę, zobacz [Zarządzanie domenami internetowymi w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Rozpoznawanie i delegowanie

Istnieją dwa typy serwerów DNS:

* *Autorytatywny* serwer DNS hostuje strefy DNS. Odpowiada na zapytania DNS dotyczące rekordów tylko w tych strefach.
* *Cykliczny* serwer DNS nie hostuje stref DNS. Odpowiada na zapytania DNS, wywołując autorytatywne serwery DNS w celu zebrania danych, których potrzebuje.

Usługa Azure DNS zapewnia autorytatywną usługę DNS.  Nie zapewnia cyklicznej usługi DNS. Usługa Cloud Services i maszyny wirtualne na platformie Azure są automatycznie skonfigurowane do korzystania z rekursywnych usług DNS udostępnianych oddzielnie w ramach infrastruktury platformy Azure. Aby uzyskać informacje na temat zmiany tych ustawień DNS, zobacz [Name Resolution in Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) (Rozpoznawanie nazw na platformie Azure).

Klienci DNS na komputerach i urządzeniach przenośnych zwykle wywołują cykliczny serwer DNS w celu wykonywania wszelkich zapytań DNS potrzebnych aplikacjom klienckim.

Gdy cykliczny serwer DNS odbiera zapytanie dotyczące rekordu DNS takiego jak „www.contoso.com”, najpierw musi znaleźć serwer nazw hostujący strefę dla domeny „contoso.com”. W celu znalezienia serwera nazw rozpoczyna od serwerów nazw głównych i wyszukuje serwery nazw hostujące strefę „com”. Następnie wykonuje zapytanie względem serwerów nazw „com”, aby znaleźć serwery nazw hostujące strefę „contoso.com”.  Na koniec jest w stanie wykonać względem tych serwerów nazw zapytanie dla „www.contoso.com”.

Ta procedura jest nazywana rozpoznawaniem nazwy DNS. Mówiąc ściślej, rozpoznawanie nazw DNS obejmuje dodatkowe czynności, takie jak śledzenie rekordów CNAME, ale nie jest to istotne dla zrozumienia, jak działa delegowanie DNS.

W jaki sposób strefa nadrzędna wskazuje serwery nazw dla strefy podrzędnej? Robi to przy użyciu specjalnego rekordu DNS nazywanego rekordem NS (angielski akronim „NS” oznacza „name server”, czyli „serwer nazw”). Na przykład strefa główna zawiera rekordy NS dla strefy „com” i pokazuje serwery nazw strefy „com”. Z kolei strefa „com” zawiera rekordy NS dla strefy „contoso.com”, która wyświetla serwery nazw dla strefy „contoso.com”. Konfigurowanie rekordów NS dla strefy podrzędnej w strefie nadrzędnej nazywa się delegowaniem domeny.

Na poniższej ilustracji przedstawiono przykładowe zapytanie DNS. Contoso.net i partners.contoso.net są strefami DNS na platformie Azure.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. Klient żąda adresu `www.partners.contoso.net` z lokalnego serwera DNS.
1. Lokalny serwer DNS nie ma tego rekordu, dlatego wysyła żądanie do swojego głównego serwera nazw.
1. Główny serwer nazw nie ma tego rekordu, ale dysponuje informacjami o adresie serwera nazw `.net`, udostępnia więc ten adres serwerowi DNS.
1. Serwer DNS wysyła żądanie do serwera nazw `.net`. Na tym serwerze nie ma właściwego rekordu, ale jest informacja o adresie serwera nazw contoso.net. W tym przypadku jest to strefa DNS hostowana w usłudze Azure DNS.
1. Strefa `contoso.net` nie ma szukanego rekordu, ale dysponuje informacjami o serwerze nazw dla adresu `partners.contoso.net` i w odpowiedzi przekazuje te informacje. W tym przypadku jest to strefa DNS hostowana w usłudze Azure DNS.
1. Serwer DNS żąda adresu IP `partners.contoso.net` ze strefy `partners.contoso.net`. Zawiera ona rekord A i w odpowiedzi zwraca adres IP.
1. Serwer DNS udostępnia adres IP klientowi.
1. Klient łączy się z witryną sieci Web `www.partners.contoso.net`.

Każde delegowanie faktycznie zawiera dwie kopie rekordów NS — jedną w strefie nadrzędnej wskazującej strefę podrzędną i drugą w samej strefie podrzędnej. Strefa „contoso.net” zawiera rekordy NS dla strefy „contoso.net” (oprócz rekordów NS w strefie „net”). Są to tak zwane autorytatywne rekordy NS i znajdują się na wierzchołku strefy podrzędnej.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [delegować domenę do usługi Azure DNS](dns-delegate-domain-azure-dns.md).

