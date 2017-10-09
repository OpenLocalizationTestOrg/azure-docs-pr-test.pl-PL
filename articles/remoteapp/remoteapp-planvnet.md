---
title: "aaaHow tooplan sieci wirtualnej dla kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooplan sieci wirtualnej dla kolekcji usługi Azure RemoteApp."
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
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Jak tooplan sieci wirtualnej dla usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

W tym dokumencie opisano sposób tooset Twojej sieci wirtualnej platformy Azure (VNET) i podsieci hello usługi Azure RemoteApp. Jeśli znasz sieci wirtualnych platformy Azure, jest możliwość, która pomaga możesz toovirtualize sieci infrastruktury toohello chmury i toocreate hybrydowych rozwiązań z platformy Azure i zasobami lokalnymi. Więcej informacji na ten temat można znaleźć [tutaj](../virtual-network/virtual-networks-overview.md).

Jeśli chcesz toodefine zasad zabezpieczeń dla ruchu (przychodzących i wychodzących) w Twojej sieci wirtualnej, w której wdrażana jest usługa Azure RemoteApp, zdecydowanie zaleca się utworzenie osobnej podsieci dla usługi Azure RemoteApp z resztą hello wdrożeń w hello Azure sieć wirtualna. Aby uzyskać więcej informacji dotyczących sposobu toodefine zasady zabezpieczeń w sieci wirtualnej platformy Azure sieci podsieci, przeczytaj [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Typy kolekcji usługi Azure RemoteApp z sieci wirtualnych platformy Azure
Hello poniższej grafice Pokaż Witaj dwie opcje innej kolekcji należy toouse sieci wirtualnej.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Azure kolekcji w chmurze usługi RemoteApp z sieci Wirtualnej
 ![Usługa Azure RemoteApp — kolekcji w chmurze z sieci Wirtualnej](./media/remoteapp-planvpn/ra-cloudvpn.png)

Reprezentuje kolekcję usługi Azure RemoteApp, gdzie wszystkie zasoby hello czy hello RemoteApp sesji hosty muszą tooaccess są wdrażane na platformie Azure. Mogą być w hello tej samej sieci Wirtualnej jako sieci Wirtualnej usługi RemoteApp hello lub innej sieci Wirtualnej na platformie Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Azure RemoteApp kolekcji hybrydowej z sieci Wirtualnej
![Usługa Azure RemoteApp — kolekcji hybrydowej z sieci Wirtualnej](./media/remoteapp-planvpn/ra-hybridvpn.png)

Reprezentuje kolekcję usługi Azure RemoteApp, gdzie niektórych zasobów hello czy hello RemoteApp sesji hosty muszą tooaccess są wdrożone lokalnymi. Witaj sieci Wirtualnej usługi RemoteApp jest połączonych toohello sieci lokalnej za pomocą technologii hybrydowe platformy Azure, takich jak sieci VPN typu lokacja lokacja lub usługi Express Route.

## <a name="how-hello-system-works"></a>Jak działa hello system
W obszarze hello obejmuje usługę Azure RemoteApp wdraża podsieć sieci wirtualnej toohello maszyn wirtualnych platformy Azure (z przekazanego obraz), wybranych podczas inicjowania obsługi. Jeśli zostanie wybrana opcja kolekcję hybrydową, spróbujemy hello tooresolve nazwa FQDN kontrolera domeny hello wprowadzony w hello dostarczania przepływu pracy z powitania serwera DNS w sieci wirtualnej hello.  
Jeśli łączysz się z istniejącą siecią wirtualną tooan, upewnij się, że porty niezbędne hello tooexpose w sieciowych grup zabezpieczeń w podsieci usługi Azure RemoteApp. 

Zalecane jest użycie [podsieci wystarczająco duży dla usługi Azure RemoteApp](remoteapp-vnetsizing.md). Witaj największy obsługiwany przez sieć wirtualna Azure jest /8 (przy użyciu definicje podsieci CIDR). Podsieć powinna być wystarczająco duży tooaccommodate wszystkich hello Azure RemoteApp maszyn wirtualnych podczas skalowania w górę po więcej użytkownicy uzyskują dostęp do aplikacji hello. 

Poniżej przedstawiono czynności hello potrzebujesz tooenable na podsieć sieci wirtualnej: 

1. Ruch wychodzący z podsieci hello powinno być dozwolone na toocommunicate 10101 10175 zakresu portów z jednym hello wewnętrzny usługi Azure RemoteApp.
2. Ruch wychodzący powinno być dozwolone z tooAzure tooconnect Twojego podsieci magazynu na porcie 443
3. Jeśli masz usługi Active Directory hostowana na platformie Azure, upewnij się, że w żadnej maszyny Wirtualnej w ramach hello podsieć sieci wirtualnej dla usługi Azure RemoteApp jest kontrolerem domeny toothat tooconnect stanie. Hello DNS w sieci wirtualnej hello powinny być możliwe tooresolve hello FQDN tego kontrolera domeny.

## <a name="virtual-network-with-forced-tunneling"></a>Sieci wirtualnej przy użyciu tunelowania wymuszonego
[Wymuszone tunelowanie](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) jest teraz obsługiwane dla wszystkich nowych kolekcji usługi Azure RemoteApp. Obecnie nie obsługujemy hello migracji istniejącej toosupport kolekcji wymuszonego tunelowania.  Konieczne będzie toodelete wszystkich istniejących zbiorach przy użyciu hello sieci Wirtualnej, połączenie jest ustanawiane tooAzure RemoteApp, a następnie utworzyć nowe tooget jednego wymuszonego tunelowania włączony w kolekcji. 

