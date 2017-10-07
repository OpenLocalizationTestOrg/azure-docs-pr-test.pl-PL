---
title: "aaaOverview usługi Azure DNS | Dokumentacja firmy Microsoft"
description: "Omówienie systemu DNS obsługującego usługę w systemie Microsoft Azure. Hosta domeny w systemie Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Omówienie usługi Azure DNS

System nazw domen Hello lub DNS, jest odpowiedzialny za tłumaczenia (lub rozpoznawania) nazwa witryny sieci Web lub usługi tooits adresu IP. Usługa DNS platformy Azure to Usługa hostingu domen DNS, rozpoznawania nazw przy użyciu infrastruktury Microsoft Azure. Hosting domeny na platformie Azure, można zarządzać systemie DNS rekordów przy użyciu hello tego samego poświadczeń, interfejsy API, narzędzia i rozliczeń jak innymi usługami Azure.

![Omówienie systemu DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Funkcje

* **Niezawodność i wydajność** -domen DNS w usłudze Azure DNS są hostowane w globalnej sieci platformy Azure serwerów nazw DNS. Używamy emisji dowolnej sieci tak, aby każdej zapytanie DNS zostanie odebrane przez serwer DNS dostępne najbliższego hello. Zapewnia to zarówno duża wydajność i wysoka dostępność dla domeny.

* **Integracja** — usługa Azure DNS hello mogą być używane toomanage rekordy DNS dla usługi Azure i mogą być używane tooprovide DNS sieci zewnętrznych zasobów. Usługa Azure DNS jest zintegrowany z hello portalu Azure i używa hello tych samych poświadczeń, rozliczeń i pomocy technicznej, jak innymi usługami Azure.

* **Zabezpieczenia** -hello usługa Azure DNS jest oparta na usłudze Azure Resource Manager. W efekcie korzysta z funkcji Menedżera zasobów, takich jak kontrola dostępu oparta na rolach, dzienniki inspekcji i blokowanie zasobów. Twoje domenach i rekordach mogą być zarządzane za pośrednictwem hello portalu Azure, poleceń cmdlet programu Azure PowerShell, a hello wiersza polecenia platformy Azure i platform. Aplikacje wymagające automatycznego zarządzania DNS można zintegrować z usługą hello za pośrednictwem hello interfejsu API REST i zestawy SDK.

Usługa Azure DNS nie obsługuje obecnie zakupów nazw domen. Jeśli chcesz toopurchase domen, należy toouse rejestratora nazw domen innych firm. Rejestrator Hello zazwyczaj pobiera małych opłata. następnie Hello domeny może być hostowana w usłudze Azure DNS zarządzania rekordów DNS. Zobacz [delegować tooAzure domeny DNS](dns-domain-delegation.md) szczegółowe informacje.

## <a name="pricing"></a>Cennik

Rozliczeń DNS jest oparta na powitania liczbę stref DNS udostępnianych na platformie Azure i hello liczby zapytań DNS. więcej informacji na temat cen, odwiedź stronę toolearn [cennik usługi Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>Często zadawane pytania

Często zadawane pytania dotyczące usługi Azure DNS, zobacz hello [DNS platformy Azure — często zadawane pytania](dns-faq.md).

## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat stref DNS i rekordy odwiedzając: [DNS strefy i rejestruje omówienie](dns-zones-records.md).

Dowiedz się, jak za[utworzyć strefę DNS](./dns-getstarted-create-dnszone-portal.md) w usłudze Azure DNS.

Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.

