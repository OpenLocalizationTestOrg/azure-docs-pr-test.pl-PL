---
title: "Omówienie delegowania DNS aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toochange, delegowanie domeny i używanie usługi Azure DNS nazwy hosting domeny tooprovide serwerów."
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
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegowanie stref DNS za pomocą usługi Azure DNS

Usługa DNS platformy Azure pozwala toohost strefy DNS i zarządzanie nimi hello rekordy DNS dla domeny na platformie Azure. Aby zapytania DNS dotyczące tooreach domeny usługi Azure DNS, hello domena ma toobe delegowane z domeny nadrzędnej hello tooAzure DNS. Należy pamiętać, że usługi Azure DNS nie jest hello rejestratora domen. W tym artykule opisano, jak działa delegowanie domeny i jak toodelegate tooAzure domen DNS.

## <a name="how-dns-delegation-works"></a>Jak działa delegowanie DNS

### <a name="domains-and-zones"></a>Domeny i strefy

Witaj System nazw domen jest hierarchią domen. Hierarchia Hello rozpoczyna się od domeny "główny" hello, której nazwa to po prostu "**.**".  Poniżej są domeny najwyższego poziomu, takie jak „com”, „net”, „org”, „uk” lub „jp”.  Pod tymi domenami najwyższego poziomu są domeny drugiego poziomu, takie jak „org.uk” lub „co.jp”.  I tak dalej. domeny Hello w hello hierarchii DNS są hostowane przy użyciu osobnych stref DNS. Te strefy są globalnie rozproszone, hostowane przez serwery DNS na całym świecie hello.

**Strefa DNS** — domena jest unikatową nazwę w hello System nazw domen, na przykład "contoso.com". Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. Na przykład hello domena "contoso.com" może zawierać wiele rekordów DNS, takie jak "mail.contoso.com" (dla serwera poczty) i "www.contoso.com" (dla witryny sieci Web).

**Rejestrator domen** — Rejestrator domen to firma, która może udostępniać nazwy domen internetowych. Sprawdź, domeny internetowej hello toouse jest dostępne i umożliwiają toopurchase go. Po zarejestrowaniu nazwy domeny hello jesteś hello prawnym właścicielem hello nazwy domeny. Jeśli masz już domeny internetowej, zostanie użyty hello bieżącej domeny Rejestrator toodelegate tooAzure DNS.

toofind więcej informacji, kto jest właścicielem danej nazwy domeny, lub Aby uzyskać informacje na temat toobuy domeny, zobacz [Internet domeny zarządzania w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Rozpoznawanie i delegowanie

Istnieją dwa typy serwerów DNS:

* *Autorytatywny* serwer DNS hostuje strefy DNS. Odpowiada na zapytania DNS dotyczące rekordów tylko w tych strefach.
* *Cykliczny* serwer DNS nie hostuje stref DNS. Wywołując autorytatywne serwery toogather hello dane DNS musi on odpowiada na zapytania DNS.

Usługa Azure DNS zapewnia autorytatywną usługę DNS.  Nie zapewnia cyklicznej usługi DNS. Usługi w chmurze i maszyn wirtualnych na platformie Azure są automatycznie skonfigurowana toouse cykliczne usługi DNS, oddzielnie dostarczonego w ramach infrastruktury platformy Azure. Aby uzyskać informacje dotyczące toochange te ustawienia DNS, zobacz temat [rozpoznawania nazw w usłudze Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

Klienci DNS na komputerach i urządzeniach przenośnych zwykle wywołują tooperform serwera DNS cykliczne wszelkich zapytań DNS potrzebnych powitania klienta aplikacji.

Rekursywny serwer DNS odbiera zapytanie dotyczące rekordu DNS takiego jak "www.contoso.com", najpierw musi toofind hello nazwy serwera hostingu hello strefę dla domeny "contoso.com" hello. toofind hello nazwę serwera, jego rozpoczyna się od serwerów nazw głównych hello i wyszukuje hello serwery nazw hostujące strefę "com" hello. Tworzy następnie kwerendę hello "com" nazwy serwerów toofind hello serwery nazw hostujące strefę "contoso.com" hello.  Na koniec jest w stanie tooquery te serwery nazw dla "www.contoso.com".

Ta procedura jest wywoływana rozpoznawanie nazwy DNS hello. Mówiąc ściślej rozpoznawanie nazw DNS obejmuje dodatkowe czynności, takie jak śledzenie rekordów CNAME, ale nie jest to ważne toounderstanding, jak działa delegowanie DNS.

Jak strefy nadrzędnej "punkt" toohello serwery nazw dla strefy podrzędnej? Robi to przy użyciu specjalnego rekordu DNS nazywanego rekordem NS (angielski akronim „NS” oznacza „name server”, czyli „serwer nazw”). Na przykład hello katalogu głównego strefy "com" zawiera rekordy NS i przedstawia hello serwerów nazw dla strefy "com" hello. Z kolei strefa "com" hello zawiera rekordy NS dla "contoso.com", która zawiera hello serwerów nazw dla strefy "contoso.com" hello. Konfigurowanie hello rekordy NS dla strefy podrzędnej w strefie nadrzędnej nazywa się delegujące hello domeny.

następujące obraz powitania przedstawiono przykładowe zapytanie DNS. Witaj contoso.net i partners.contoso.net są strefy DNS platformy Azure.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. Witaj żądań klientów `www.partners.contoso.net` ze swojego lokalnego serwera DNS.
1. Witaj lokalny serwer DNS nie ma rekordu hello tak ułatwia serwer nazw głównych tootheir żądania.
1. Witaj głównego nazwa serwera nie ma rekordu hello, ale zna adres hello hello `.net` serwer nazw udostępnia tego serwera DNS toohello adresu
1. Witaj DNS wysyła hello żądania toohello `.net` serwer nazw nie ma rekordu hello ale nie znać adres hello hello contoso.net nazwy serwera. W tym przypadku jest to strefa DNS hostowana w usłudze Azure DNS.
1. strefy Hello `contoso.net` , ale nie ma rekordu hello zna powitania serwera nazw dla `partners.contoso.net` i które odpowiada. W tym przypadku jest to strefa DNS hostowana w usłudze Azure DNS.
1. Serwer DNS Hello żąda adresu IP hello `partners.contoso.net` z hello `partners.contoso.net` strefy. Zawiera rekord A hello i odpowiada za hello adresu IP.
1. Serwer DNS Hello zapewnia klienta toohello adres IP hello
1. Klient Hello łączy toohello witryny sieci Web `www.partners.contoso.net`.

Każde delegowanie faktycznie zawiera dwie kopie rekordów NS hello; jeden hello strefie nadrzędnej wskazującej strefę podrzędną toohello i drugą w samej strefie podrzędnej hello. strefie "contoso.net" Hello zawiera rekordy hello NS "contoso.net" (w dodanie toohello rekordy NS w "net"). Te rekordy są nazywane autorytatywne rekordy NS i znajdują się na wierzchołku strefy podrzędnej hello hello.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-delegate-domain-azure-dns.md)

