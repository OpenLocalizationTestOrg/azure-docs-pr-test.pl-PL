---
title: "Sposób planowania sieci wirtualnej dla kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaplanować sieci wirtualnej dla kolekcji usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a>Sposób planowania sieci wirtualnej Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Ten dokument zawiera opis sposobu konfigurowania sieci wirtualnej platformy Azure (VNET) i podsieci usługi Azure RemoteApp. Jeśli znasz sieci wirtualnych platformy Azure, jest możliwość, która ułatwia wirtualizację infrastruktury sieci w chmurze oraz tworzenie hybrydowych rozwiązań z platformy Azure i zasobami lokalnymi. Więcej informacji na ten temat można znaleźć [tutaj](../virtual-network/virtual-networks-overview.md).

Jeśli chcesz zdefiniować zasady zabezpieczeń dla ruchu (przychodzących i wychodzących) w Twojej sieci wirtualnej, w której wdrażana jest usługa Azure RemoteApp, zdecydowanie zaleca się utworzenie osobnej podsieci dla usługi Azure RemoteApp od pozostałej części wdrażanie na platformie Azure sieć wirtualna. Aby uzyskać więcej informacji na temat definiowania zasad zabezpieczeń w podsieci sieci wirtualnej platformy Azure, przeczytaj [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Typy kolekcji usługi Azure RemoteApp z sieci wirtualnych platformy Azure
Poniższej grafice Pokaż dwie opcje inną kolekcję, jeśli chcesz korzystać z sieci wirtualnej.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Azure kolekcji w chmurze usługi RemoteApp z sieci Wirtualnej
 ![Usługa Azure RemoteApp — kolekcji w chmurze z sieci Wirtualnej](./media/remoteapp-planvpn/ra-cloudvpn.png)

Reprezentuje kolekcję usługi Azure RemoteApp, gdy wszystkie zasoby, które sesji usługi RemoteApp hostów wymagają dostępu do są wdrażane na platformie Azure. Można je w tej samej sieci Wirtualnej jako sieci Wirtualnej usługi RemoteApp lub innej sieci Wirtualnej na platformie Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Azure RemoteApp kolekcji hybrydowej z sieci Wirtualnej
![Usługa Azure RemoteApp — kolekcji hybrydowej z sieci Wirtualnej](./media/remoteapp-planvpn/ra-hybridvpn.png)

Reprezentuje kolekcję usługi Azure RemoteApp, w których niektóre zasoby wymagające dostępu do hostów sesji usługi RemoteApp są wdrożone lokalnymi. Sieci Wirtualnej usługi RemoteApp jest połączony z siecią lokalną przy użyciu technologii hybrydowe platformy Azure, takich jak sieci VPN typu lokacja lokacja lub usługi Express Route.

## <a name="how-the-system-works"></a>Jak działa system
W obszarze obejmuje usługi Azure RemoteApp wdraża maszyn wirtualnych platformy Azure (z przekazanego obrazu) do podsieci sieci wirtualnej, która została wybrana opcja podczas inicjowania obsługi. Jeśli zostanie wybrana opcja kolekcję hybrydową, spróbujemy rozpoznać nazwę FQDN kontrolera domeny wprowadzony w przepływie pracy inicjowania obsługi administracyjnej na serwerze DNS w sieci wirtualnej.  
Jeśli łączysz się z istniejącą siecią wirtualną, upewnij się, że udostępnianie niezbędne porty sieciowe grupy zabezpieczeń w podsieci usługi Azure RemoteApp. 

Zalecane jest użycie [podsieci wystarczająco duży dla usługi Azure RemoteApp](remoteapp-vnetsizing.md). Największy obsługiwany przez sieć wirtualna Azure jest /8 (przy użyciu definicje podsieci CIDR). Podsieć powinna być wystarczająco duży, aby uwzględnić wszystkie RemoteApp maszyny wirtualne Azure podczas skalowania w górę, gdy więcej użytkownicy uzyskują dostęp do aplikacji. 

Poniżej przedstawiono czynności, które należy włączyć w podsieci sieci wirtualnej: 

1. Ruch wychodzący z podsieci powinno mieć dostęp na zakres portów 10101 10175 do komunikowania się z jednego z wewnętrznych usług Azure RemoteApp.
2. Ruch wychodzący powinno być dozwolone z podsieci do połączenia z magazynem Azure na porcie 443
3. Jeśli masz usługi Active Directory hostowana na platformie Azure, upewnij się, że w żadnej maszyny Wirtualnej w podsieci sieci wirtualnej dla usługi Azure RemoteApp jest w stanie nawiązać połączenia z tym kontrolerze domeny. System DNS w sieci wirtualnej powinna być w stanie rozpoznać nazwę FQDN kontrolera domeny.

## <a name="virtual-network-with-forced-tunneling"></a>Sieci wirtualnej przy użyciu tunelowania wymuszonego
[Wymuszone tunelowanie](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) jest teraz obsługiwane dla wszystkich nowych kolekcji usługi Azure RemoteApp. Obecnie nie obsługujemy migracji istniejącej kolekcji do obsługi wymuszonego tunelowania.  Konieczne będzie usunięcie wszystkich istniejących zbiorach przy użyciu sieci Wirtualnej, która łączysz się do usługi Azure RemoteApp i Utwórz nowe hasło, aby pobrać wymuszone tunelowanie, włączone na kolekcji. 

