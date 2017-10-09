---
title: "aaaList toowhitelist porty i adresy URL dla usługi Azure RemoteApp wdrożony w sieci wirtualnych klienta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, które porty i adresy URL tooconfigure potrzebne do komunikacji za pośrednictwem usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lista dostępu toopermit porty i adresy URL dla usługi Azure RemoteApp wdrożonych klientów sieci wirtualnej
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Jeśli wdrażasz kolekcji usługi Azure RemoteApp w chmurze czy hybrydowa w sieć wirtualną (VNET), przejrzyj następujące informacje o portach hello. Aby uzyskać więcej informacji o sieciach wirtualnych, przeczytaj [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md). Jeśli po utworzeniu grupy zabezpieczeń sieci (NSG) Ograniczanie ruchu toohello sieci wirtualnej zasobów w kolekcji, upewnij się, że hello następujące porty są dozwolone za pomocą zasad zabezpieczeń hello na powitania sieci wirtualnej. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, przeczytaj [co to jest grupa zabezpieczeń sieci? (NSG) ](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Usługa Azure RemoteApp podsieci musi punkty końcowe toothese dostępu i adresy URL:
* *. servicebus.windows.net
* *. servicebus.net
* https://*.RemoteApp.windowsazure.com  
* https://www.RemoteApp.windowsazure.com 
* https://*RemoteApp.windowsazure.com  
* https://*.Core.Windows.NET  
* Wychodzące: TCP: TCP: 443, 9351, 9352, 10101 10175 
* Opcjonalne — UDP: 10201 10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Klienci usługi Azure RemoteApp muszą uzyskać dostęp do punktów końcowych toothese i adres URL:
Przez klientów, które oznacza I hello komputerów osobistych, urządzeń itp. tej osoby Użyj tooconnect toohello aplikacje wdrożone w hello kolekcji usługi Azure RemoteApp.

* https://telemetry.RemoteApp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (opcjonalne porty UDP hello są dla tego adresu) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.RemoteApp.windowsazure.com 
* https://*.Core.Windows.NET  
* Wychodzące: TCP: 443  
* Opcjonalne - UDP: 3391 

