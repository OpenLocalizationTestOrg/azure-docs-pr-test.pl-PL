---
title: "Migracji sieci wirtualnych ExpressRoute skojarzone z klasycznym tooResource Menedżera: Azure: programu PowerShell | Dokumentacja firmy Microsoft"
description: Na tej stronie opisano, jak toomigrate skojarzone sieci wirtualne tooResource Manager po przeniesieniu obwodu.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Migracji sieci wirtualnych ExpressRoute skojarzone z klasycznym tooResource Manager

W tym artykule opisano, jak toomigrate Azure ExpressRoute skojarzone sieci wirtualne od modelu wdrażania usługi Azure Resource Manager toohello hello wdrażania klasycznego modelu po przeniesieniu obwodu usługi ExpressRoute. 


## <a name="before-you-begin"></a>Przed rozpoczęciem
* Sprawdź, czy masz najnowszą wersję hello hello modułów programu Azure PowerShell. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Przejrzyj informacje hello są przekazywane pod [przenoszenie obwodu usługi ExpressRoute z klasycznym tooResource Menedżera](expressroute-move.md). Upewnij się, należy zapoznać się hello limity i ograniczenia.
* Sprawdź, czy obwodu hello pełnej funkcjonalności w hello klasycznego modelu wdrażania.
* Upewnij się, że masz grupę zasobów, który został utworzony w modelu wdrażania usługi Resource Manager hello.
* Przejrzyj powitania po migracji zasobów dokumentacji:

    * [Obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Często zadawane pytania: Obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Przejrzyj typowe błędy, migracji i środki zaradcze](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Obsługiwane i nieobsługiwane scenariusze

* Obwodu usługi ExpressRoute można przenieść ze środowiska Menedżera zasobów klasycznych toohello hello bez żadnego przestoju. Wszelkie obwodu ExpressRoute można przenosić z hello toohello klasycznego środowiska usługi Resource Manager, bez przestojów. Postępuj zgodnie z instrukcjami hello [przenoszenie obwody usługi ExpressRoute z hello toohello klasycznego modelu wdrażania Resource Manager przy użyciu programu PowerShell](expressroute-howto-move-arm.md). Jest to wymagań wstępnych toomove zasobów toohello połączonych sieci wirtualnej.
* Sieci wirtualne, bramy i skojarzonych z nimi wdrożeń w ramach sieci wirtualnej hello, które są dołączone tooan obwodu usługi expressroute w hello tej samej subskrypcji może być migrowane toohello Menedżera zasobów środowiska bez żadnego przestoju. Możesz wykonać hello kroki opisane nowsze toomigrate zasoby, takie jak sieci wirtualnych, bramy i maszyn wirtualnych wdrożonych w ramach sieci wirtualnej hello. Pamiętaj, że sieci wirtualne hello są poprawnie skonfigurowane, przed ich migracją. 
* Sieci wirtualne, bramy i skojarzonych z nimi wdrożeń w ramach sieci wirtualnej hello, które nie znajdują się w hello tej samej subskrypcji, który został hello obwodu ExpressRoute wymagają migracji hello toocomplete niektórych przestoju. Hello ostatniej sekcji dokumentu hello opisuje zasoby toomigrate toobe zostały wykonane kroki hello.
* Nie można migrować sieci wirtualnej zarówno bramę usługi ExpressRoute, jak i bramy sieci VPN.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Przenieś obwodu usługi ExpressRoute z klasycznym tooResource Manager
Należy przenieść obwodu usługi ExpressRoute z klasycznym toohello hello Resource Manager w środowisku przed podjęciem próby toomigrate zasoby, które są dołączony toohello obwodu ExpressRoute. tooaccomplish to zadań, zobacz następujące artykuły hello:

* Przejrzyj informacje hello są przekazywane pod [przenoszenie obwodu usługi ExpressRoute z klasycznym tooResource Menedżera](expressroute-move.md).
* [Przenieś obwód z klasycznym tooResource Manager przy użyciu programu Azure PowerShell](expressroute-howto-move-arm.md).
* Za pomocą portalu zarządzania usługi Azure hello. Witaj przepływu pracy można wykonać za[tworzenie nowych obwodu ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i wybierz opcję Importuj hello. 

Ta operacja nie jest związana przestoju. W trakcie migracji hello można kontynuować tootransfer danych między lokalnym i firmy Microsoft.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migracja sieci wirtualnej, bramy i skojarzonych z nimi wdrożeń

Hello procedura toomigrate zależą od tego, czy zasoby są w hello tej samej subskrypcji i/lub różnych subskrypcji.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Wykonaj migrację sieci wirtualnych, bram, i skojarzonych z nimi wdrożeń w hello tej samej subskrypcji, ponieważ hello obwodu usługi expressroute
W tej sekcji opisano toomigrate toobe zostały wykonane kroki hello sieci wirtualnej, bramy i skojarzonych z nimi wdrożeń w hello tej samej subskrypcji hello obwodu usługi expressroute. Nie jest wyłączenie skojarzony z tym migracji. Możesz kontynuować toouse wszystkie zasoby hello proces migracji. płaszczyzny zarządzania Hello jest zablokowane, gdy trwa migracja hello. 

1. Upewnij się, że obwodu ExpressRoute hello została przeniesiona z hello klasycznego toohello Menedżera zasobów środowiska.
2. Upewnij się, że w tej sieci wirtualnej hello zostało przygotowane do migracji hello odpowiednio.
3. Zarejestruj subskrypcję dla migracji zasobów. tooregister subskrypcji dla migracji zasobów, hello Użyj następującego fragmentu środowiska PowerShell:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Sprawdzanie poprawności, przygotowywania i migracji. toomove hello sieci wirtualnej, hello Użyj następującego fragmentu środowiska PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Można również przerwać migracji, uruchamiając następujące polecenia cmdlet programu PowerShell hello:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Następne kroki
* [Obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Często zadawane pytania: Obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Przejrzyj typowe błędy, migracji i środki zaradcze](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
