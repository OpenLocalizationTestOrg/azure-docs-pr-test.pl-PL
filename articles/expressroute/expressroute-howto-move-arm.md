---
title: "Przenieś obwody usługi ExpressRoute z klasycznym tooResource Menedżera: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano, jak toomove toohello klasyczny obwód usługi Resource Manager deployment model przy użyciu programu PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Przenieś obwody usługi ExpressRoute z hello toohello klasycznego modelu wdrażania Resource Manager przy użyciu programu PowerShell

toouse obwodu usługi ExpressRoute hello klasycznego i modeli wdrażania usługi Resource Manager, należy przenieść modelu wdrażania usługi Resource Manager hello obwodu toohello. Hello następujące sekcje pomocne podczas przenoszenia obwodu przy użyciu programu PowerShell.

## <a name="before-you-begin"></a>Przed rozpoczęciem

* Sprawdź, czy masz najnowszą wersję hello hello modułów programu Azure PowerShell (co najmniej w wersji 1.0). Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Przejrzyj informacje hello są przekazywane pod [przenoszenie obwodu usługi ExpressRoute z klasycznym tooResource Menedżera](expressroute-move.md). Upewnij się, należy zapoznać się hello limity i ograniczenia.
* Sprawdź, czy obwodu hello pełnej funkcjonalności w hello klasycznego modelu wdrażania.
* Upewnij się, że masz grupę zasobów, który został utworzony w modelu wdrażania usługi Resource Manager hello.

## <a name="move-an-expressroute-circuit"></a>Przenieś obwodu usługi ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Krok 1: Zbieranie szczegółów obwodu z hello klasycznego modelu wdrażania

Zaloguj się toohello klasycznego środowiska platformy Azure i zebrać hello klucza usługi.

1. Zaloguj się tooyour konto platformy Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Wybierz odpowiednią subskrypcję platformy Azure hello.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Zaimportuj moduły programu PowerShell hello platformy Azure i usługi ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Użyj polecenia cmdlet hello tooget hello usługi kluczy dla wszystkich sieci obwody usługi ExpressRoute. Po pobraniu hello klucze, skopiuj hello **klucza usługi** obwodu hello, które mają modelu wdrażania usługi Resource Manager toohello toomove.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Krok 2: Zaloguj się i utworzyć grupę zasobów

Zaloguj się w środowisku usługi Resource Manager toohello i utworzyć nową grupę zasobów.

1. Zaloguj się w środowisku usługi Azure Resource Manager tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

2. Wybierz odpowiednią subskrypcję platformy Azure hello.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Jeśli nie masz już grupę zasobów, należy zmodyfikować fragment hello poniżej toocreate nową grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Krok 3: Przenieś modelu wdrażania usługi Resource Manager toohello obwodu ExpressRoute hello

Użytkownik jest teraz gotowy toomove obwodu usługi ExpressRoute z modelu wdrażania usługi Resource Manager toohello hello wdrażania klasycznego modelu. Przed kontynuowaniem należy przejrzeć hello informacji dostępnych w [przenoszenie obwodu usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-move.md).

toomove obwodu, zmodyfikuj i uruchom następujące fragment hello:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Po zakończeniu przenoszenia hello hello nową nazwę, która znajduje się w poprzednim poleceniu cmdlet hello będzie używana tooaddress hello zasobów. obwód Hello zasadniczo zostanie zmieniona.
> 

## <a name="modify-circuit-access"></a>Modyfikowania dostępu do obwodu

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable dostępu obwodu ExpressRoute oba modele wdrażania

Po przeniesieniu programu ExpressRoute obwodu toohello Resource Manager wdrażania modelu klasycznego, można włączyć modele wdrażania tooboth dostępu. Uruchom hello następujące modele wdrażania tooboth dostępu tooenable poleceń cmdlet:

1. Uzyskiwanie szczegółowych informacji obwodu hello.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Ustaw tooTRUE "Zezwalaj na operacje klasycznym".

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Zaktualizuj hello obwodu. Po tej operacji zakończyło się pomyślnie, będzie możliwe tooview obwodu hello w hello klasycznego modelu wdrażania.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Uruchom następujące polecenia cmdlet tooget hello szczegóły hello obwodu ExpressRoute hello. Musi być klucza usługi hello stanie toosee na liście.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Możesz teraz zarządzać obwodu ExpressRoute toohello łącza za pomocą polecenia modelu wdrażania klasycznego hello klasyczne sieci wirtualne i hello poleceń Menedżera zasobów dla sieci wirtualnych Menedżera zasobów. Witaj następujące artykuły ułatwiają zarządzanie toohello łącza obwodu ExpressRoute:

    * [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute w modelu wdrażania usługi Resource Manager hello](expressroute-howto-linkvnet-arm.md)
    * [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute w hello klasycznego modelu wdrażania](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute obwodu dostępu toohello klasycznego modelu wdrażania

Uruchom następujące polecenia cmdlet toodisable dostępu toohello klasycznego modelu wdrażania hello.

1. Uzyskiwanie szczegółowych informacji o hello obwodu usługi expressroute.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Ustaw tooFALSE "Zezwalaj na operacje klasycznym".

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Zaktualizuj hello obwodu. Po tej operacji zakończyło się pomyślnie, nie będzie możliwe tooview obwodu hello w hello klasycznego modelu wdrażania.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Następne kroki

* [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute](expressroute-howto-routing-arm.md)
* [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)
