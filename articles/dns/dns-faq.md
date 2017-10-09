---
title: "aaaAzure DNS — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure DNS"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Usługa DNS platformy Azure — często zadawane pytania

## <a name="about-azure-dns"></a>Usługa DNS platformy Azure — informacje

### <a name="what-is-azure-dns"></a>Co to jest system DNS platformy Azure?

System nazw domen Hello lub DNS, jest odpowiedzialny za tłumaczenia (lub rozpoznawania) nazwa witryny sieci Web lub usługi tooits adresu IP. Usługa DNS platformy Azure to Usługa hostingu domen DNS, rozpoznawania nazw przy użyciu infrastruktury Microsoft Azure. Hosting domeny na platformie Azure, można zarządzać systemie DNS rekordów przy użyciu hello tego samego poświadczeń, interfejsy API, narzędzia i rozliczeń jak innymi usługami Azure.

Domeny DNS w usłudze Azure DNS są hostowane w globalnej sieci platformy Azure serwerów nazw DNS. Używamy emisji dowolnej sieci tak, aby każdej zapytanie DNS zostanie odebrane przez serwer DNS dostępne najbliższego hello. Zapewnia to zarówno duża wydajność i wysoka dostępność dla domeny.

Hello usługa Azure DNS jest oparta na usłudze Azure Resource Manager. W efekcie korzysta z funkcji Menedżera zasobów, takich jak kontrola dostępu oparta na rolach, dzienniki inspekcji i blokowanie zasobów. Twoje domenach i rekordach mogą być zarządzane za pośrednictwem hello portalu Azure, poleceń cmdlet programu Azure PowerShell, a hello wiersza polecenia platformy Azure i platform. Aplikacje wymagające automatycznego zarządzania DNS można zintegrować z usługą hello za pośrednictwem hello interfejsu API REST i zestawy SDK.

### <a name="how-much-does-azure-dns-cost"></a>Ile kosztuje usługi Azure DNS

model rozliczeń usługi Azure DNS Hello jest oparty na powitania liczbę stref DNS udostępnianych w usłudze Azure DNS oraz hello liczby zapytań DNS, które otrzymują. Zniżki znajdują się na podstawie użycia.

Aby uzyskać więcej informacji, zobacz hello [usługi Azure DNS cennikiem](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Co to jest hello SLA dla usługi Azure DNS?

Firma Microsoft gwarantuje, że prawidłowe żądania DNS otrzyma odpowiedź z co najmniej jedną usługę Azure DNS nazwy serwera co najmniej czas hello 99,99%.

Aby uzyskać więcej informacji, zobacz hello [strony umowy SLA platformy Azure DNS](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>Co to jest strefy DNS? To jest hello sama domena DNS? 

Domena jest unikatową nazwę w systemie nazw domen hello, na przykład "contoso.com".

Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. Na przykład hello domeny "contoso.com" może zawierać wiele rekordów DNS, takie jak "mail.contoso.com" (dla serwera poczty) i "www.contoso.com" (dla witryny sieci web). Te może być obsługiwana przez hello strefę DNS "contoso.com".

Nazwa domeny jest *tylko nazwa*, podczas gdy strefa DNS jest zasobem danych zawierający hello rekordy DNS dla nazwy domeny. Usługa DNS platformy Azure pozwala toohost strefy DNS i zarządzanie nimi hello rekordy DNS dla domeny na platformie Azure. Dostępne są także serwery DNS tooanswer zapytania DNS z hello Internet.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>Należy toopurchase toouse nazwy domeny DNS usługi Azure DNS? 

Niekoniecznie.

Nie trzeba toopurchase toohost domeny strefę DNS w usłudze Azure DNS. Można utworzyć strefę DNS w dowolnym momencie bez będący właścicielem hello nazwy domeny. Zapytania DNS dla tej strefy rozwiąże tylko, jeśli są przekierowywane się, że serwery Azure DNS toohello przypisane toohello strefy.

Należy nazwy domeny hello toopurchase, jeśli chcesz toolink strefy DNS w hello hierarchii globalnej DNS — ta umożliwia DNS wysyła zapytanie z dowolnego miejsca w hello world toofind strefy DNS i udzielić odpowiedzi z rekordów DNS.

## <a name="azure-dns-features"></a>Funkcje usługi Azure DNS

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Usługi Azure DNS obsługuje trybu failover routingu lub punkt końcowy usługi DNS ruchu?

Trybu failover routingu i punktu końcowego usługi DNS ruchu są dostarczane przez usługę Azure Traffic Manager. Jest to oddzielne usługa Azure, która może być używany razem z usługi Azure DNS. Aby uzyskać więcej informacji, zobacz hello [Omówienie Menedżera ruchu](../traffic-manager/traffic-manager-overview.md).

Usługa DNS platformy Azure obsługuje tylko hosting domeny DNS "static", gdy każdego zapytania DNS dotyczące rekordu DNS danego zawsze otrzyma hello tej samej odpowiedzi DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>Usługi Azure DNS obsługuje rejestracji nazwy jej domeny?

Nie. Usługa Azure DNS nie obsługuje obecnie zakupów nazw domen. Jeśli chcesz toopurchase domen, należy toouse rejestratora nazw domen innych firm. Rejestrator Hello zazwyczaj pobiera małych opłata. następnie Hello domeny może być hostowana w usłudze Azure DNS zarządzania rekordów DNS. Zobacz [delegować tooAzure domeny DNS](dns-domain-delegation.md) szczegółowe informacje.

Jest to funkcja, które Śledzimy naszej listy prac. Korzystając z witryny firmy Microsoft opinię za[rejestrowania programu obsługi dla tej funkcji](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>Usługi Azure DNS obsługuje domen "private"?

Nie. Obecnie usługa DNS platformy Azure obsługuje tylko domen internetowych.

Jest to funkcja, które Śledzimy naszej listy prac. Korzystając z witryny firmy Microsoft opinię za[rejestrowania programu obsługi dla tej funkcji](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Informacje o wewnętrznych opcjach DNS na platformie Azure, zobacz [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>Usługa Azure DNS obsługuje rozszerzenia DNSSEC?

Nie. Usługa DNS platformy Azure aktualnie nie obsługuje rozszerzeń DNSSEC.

Jest to funkcja, które Śledzimy naszej listy prac. Korzystając z witryny firmy Microsoft opinię za[rejestrowania programu obsługi dla tej funkcji](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Usługa DNS platformy Azure obsługuje transferów stref (AXFR/IXFR)?

Nie. Usługa Azure DNS nie obsługuje obecnie transferów stref. Strefy DNS może być [zaimportować do usługi Azure DNS przy użyciu interfejsu wiersza polecenia Azure hello](dns-import-export.md). Zarządzanie rekordami DNS za pomocą hello [portalu zarządzania usługi Azure DNS](dns-operations-recordsets-portal.md), naszych [interfejsu API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [poleceń cmdlet programu PowerShell](dns-operations-recordsets.md), lub [ Interfejs wiersza polecenia narzędzia](dns-operations-recordsets-cli.md).

Jest to funkcja, które Śledzimy naszej listy prac. Korzystając z witryny firmy Microsoft opinię za[rejestrowania programu obsługi dla tej funkcji](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>Usługi DNS platformy Azure obsługuje adres URL przekierowania?

Nie. Adres URL przekierowania usługi nie są faktycznie usługi DNS — działają na poziomie HTTP hello, a nie hello poziom DNS. Niektóre toobundle dostawcy DNS adresu URL przekierowania usługi w ramach ich ogólną oferty. Jest to obecnie nieobsługiwane przez usługę Azure DNS.

Ta funkcja jest śledzony w naszej listy prac. Korzystając z witryny firmy Microsoft opinię za[rejestrowania programu obsługi dla tej funkcji](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Za pomocą usługi Azure DNS

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Czy mogę hostowane przy użyciu usługi Azure DNS i dostawcy usługi DNS innej domeny?

Tak. Usługa DNS platformy Azure obsługuje wspólnej hostingu domeny z innymi usługami DNS.

toodo, należy więc rekordów hello NS toomodify dla domeny hello (które kontroli, których dostawców odbierania DNS wysyła zapytanie dla domeny hello) serwery nazw toohello toopoint zarówno dostawców. Te rekordy NS muszą toobe zmodyfikowane w miejscach 3: w usłudze Azure DNS w hello inny dostawca w strefie nadrzędnej hello (zazwyczaj skonfigurowany za pomocą rejestratora nazw domen hello). Aby uzyskać więcej informacji dotyczących delegowania usługi DNS, zobacz [Delegowanie domeny DNS](dns-domain-delegation.md).

Ponadto należy tooensure czy hello rekordy DNS dla domeny hello są synchronizowane między zarówno dostawców DNS. Usługa Azure DNS nie obsługuje obecnie transferów stref DNS. Należy toosynchronize rekordy DNS przy użyciu albo hello [portalu zarządzania usługi Azure DNS](dns-operations-recordsets-portal.md), naszych [interfejsu API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [poleceń cmdlet programu PowerShell](dns-operations-recordsets.md) , lub [interfejsu wiersza polecenia narzędzia](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>Czy mam toodelegate mojej domeny tooall 4 Azure serwery DNS?

Tak. Usługa Azure DNS przypisuje 4 serwery nazw strefy DNS tooeach, izolacji błędów i zwiększonej odporności. tooqualify dla hello umowy SLA platformy Azure DNS, należy toodelegate tooall 4 serwerów nazwy domeny.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Jakie są limity użycia hello Azure DNS?

następujące domyślne limity Hello się przy użyciu usługi Azure DNS:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Strefy DNS platformy Azure można przenosić między grupami zasobów lub subskrypcji?

Tak. Strefy DNS można przenosić między grupami zasobów lub subskrypcji.

Nie ma żadnych wpływu na zapytania DNS podczas przenoszenia strefy DNS. Hello serwery nazw przypisane strefy toohello pozostają hello, jak zwykle w całym przetwarzane są takie same i zapytań DNS.

Aby uzyskać więcej informacji oraz instrukcje dotyczące toomove stref DNS, zobacz [przenoszenia zasobów tooa nową grupę zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Jak długo trwa dla efektu tootake zmiany DNS?

Nowych stref DNS i rekordy DNS są zwykle odzwierciedlone na serwery Azure DNS hello szybkiego, w ciągu kilku sekund.

Rekordy DNS tooexisting zmiany może zająć nieco dłużej, ale nadal może mieć odzwierciedlenie w hello serwery DNS platformy Azure w ciągu 60 sekund. W takim przypadku DNS buforowania poza usługi Azure DNS (przez klientów DNS i rozpoznawania nazw DNS cykliczne) również może wpłynąć hello czas poświęcony na toobe zmiany DNS skuteczne. Ten czas trwania pamięci podręcznej mogą być kontrolowane za pomocą hello czasu wygaśnięcia (TTL, Time-To-Live) właściwości każdego zestawu rekordów.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Jak chronić mój stref DNS przed przypadkowym usunięciem?

Usługa Azure DNS jest zarządzana przy użyciu usługi Azure Resource Manager i korzyści z hello funkcje kontroli dostępu do tej usługi Azure Resource Manager udostępnia. Kontrola dostępu oparta na rolach może być używane toocontrol użytkowników, którzy mają stref tooDNS odczytu lub zapisu i zestawy rekordów. Blokowania zasobów może być zastosowane tooprevent przypadkowemu modyfikacja lub usunięcie strefy DNS i zestawy rekordów.

Aby uzyskać więcej informacji, zobacz [ochrona strefy DNS i rekordy](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Jak skonfigurować rekordy SPF w usłudze Azure DNS?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Jak ustawić zapasowej międzynarodowej domeny nazwę (IDN) w usłudze Azure DNS?

Międzynarodowe nazwy domen (IDN) działają przez kodowanie, których używane są nazwa DNS "[punycode](https://en.wikipedia.org/wiki/Punycode)". Zapytania DNS są wykonywane przy użyciu tych nazw kodowany w formacie punycode.

Międzynarodowe nazwy domen (IDN) w usłudze Azure DNS można skonfigurować przy pierwszym konwertowania nazwy strefy hello lub toopunycode nazwy zestawu rekordów. Usługa Azure DNS nie obsługuje obecnie wbudowanej konwersję z/na ciąg punycode.

## <a name="next-steps"></a>Następne kroki

[Dowiedz się więcej o usłudze Azure DNS](dns-overview.md)
<br>
[Więcej informacji na temat stref DNS i rekordów](dns-zones-records.md)
<br>
[Wprowadzenie do usługi Azure DNS](dns-getstarted-portal.md)

