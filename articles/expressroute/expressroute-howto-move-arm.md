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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="eded1-103">Przenieś obwody usługi ExpressRoute z hello toohello klasycznego modelu wdrażania Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eded1-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="eded1-104">toouse obwodu usługi ExpressRoute hello klasycznego i modeli wdrażania usługi Resource Manager, należy przenieść modelu wdrażania usługi Resource Manager hello obwodu toohello.</span><span class="sxs-lookup"><span data-stu-id="eded1-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="eded1-105">Hello następujące sekcje pomocne podczas przenoszenia obwodu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eded1-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eded1-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="eded1-106">Before you begin</span></span>

* <span data-ttu-id="eded1-107">Sprawdź, czy masz najnowszą wersję hello hello modułów programu Azure PowerShell (co najmniej w wersji 1.0).</span><span class="sxs-lookup"><span data-stu-id="eded1-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="eded1-108">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eded1-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="eded1-109">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="eded1-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="eded1-110">Przejrzyj informacje hello są przekazywane pod [przenoszenie obwodu usługi ExpressRoute z klasycznym tooResource Menedżera](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="eded1-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="eded1-111">Upewnij się, należy zapoznać się hello limity i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="eded1-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="eded1-112">Sprawdź, czy obwodu hello pełnej funkcjonalności w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eded1-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="eded1-113">Upewnij się, że masz grupę zasobów, który został utworzony w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="eded1-114">Przenieś obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="eded1-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="eded1-115">Krok 1: Zbieranie szczegółów obwodu z hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="eded1-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="eded1-116">Zaloguj się toohello klasycznego środowiska platformy Azure i zebrać hello klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="eded1-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="eded1-117">Zaloguj się tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eded1-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="eded1-118">Wybierz odpowiednią subskrypcję platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="eded1-119">Zaimportuj moduły programu PowerShell hello platformy Azure i usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eded1-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="eded1-120">Użyj polecenia cmdlet hello tooget hello usługi kluczy dla wszystkich sieci obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eded1-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="eded1-121">Po pobraniu hello klucze, skopiuj hello **klucza usługi** obwodu hello, które mają modelu wdrażania usługi Resource Manager toohello toomove.</span><span class="sxs-lookup"><span data-stu-id="eded1-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="eded1-122">Krok 2: Zaloguj się i utworzyć grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="eded1-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="eded1-123">Zaloguj się w środowisku usługi Resource Manager toohello i utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="eded1-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="eded1-124">Zaloguj się w środowisku usługi Azure Resource Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="eded1-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="eded1-125">Wybierz odpowiednią subskrypcję platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="eded1-126">Jeśli nie masz już grupę zasobów, należy zmodyfikować fragment hello poniżej toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="eded1-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="eded1-127">Krok 3: Przenieś modelu wdrażania usługi Resource Manager toohello obwodu ExpressRoute hello</span><span class="sxs-lookup"><span data-stu-id="eded1-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="eded1-128">Użytkownik jest teraz gotowy toomove obwodu usługi ExpressRoute z modelu wdrażania usługi Resource Manager toohello hello wdrażania klasycznego modelu.</span><span class="sxs-lookup"><span data-stu-id="eded1-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="eded1-129">Przed kontynuowaniem należy przejrzeć hello informacji dostępnych w [przenoszenie obwodu usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="eded1-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="eded1-130">toomove obwodu, zmodyfikuj i uruchom następujące fragment hello:</span><span class="sxs-lookup"><span data-stu-id="eded1-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="eded1-131">Po zakończeniu przenoszenia hello hello nową nazwę, która znajduje się w poprzednim poleceniu cmdlet hello będzie używana tooaddress hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="eded1-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="eded1-132">obwód Hello zasadniczo zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="eded1-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="eded1-133">Modyfikowania dostępu do obwodu</span><span class="sxs-lookup"><span data-stu-id="eded1-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="eded1-134">tooenable dostępu obwodu ExpressRoute oba modele wdrażania</span><span class="sxs-lookup"><span data-stu-id="eded1-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="eded1-135">Po przeniesieniu programu ExpressRoute obwodu toohello Resource Manager wdrażania modelu klasycznego, można włączyć modele wdrażania tooboth dostępu.</span><span class="sxs-lookup"><span data-stu-id="eded1-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="eded1-136">Uruchom hello następujące modele wdrażania tooboth dostępu tooenable poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="eded1-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="eded1-137">Uzyskiwanie szczegółowych informacji obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="eded1-138">Ustaw tooTRUE "Zezwalaj na operacje klasycznym".</span><span class="sxs-lookup"><span data-stu-id="eded1-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="eded1-139">Zaktualizuj hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="eded1-139">Update hello circuit.</span></span> <span data-ttu-id="eded1-140">Po tej operacji zakończyło się pomyślnie, będzie możliwe tooview obwodu hello w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eded1-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="eded1-141">Uruchom następujące polecenia cmdlet tooget hello szczegóły hello obwodu ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="eded1-142">Musi być klucza usługi hello stanie toosee na liście.</span><span class="sxs-lookup"><span data-stu-id="eded1-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="eded1-143">Możesz teraz zarządzać obwodu ExpressRoute toohello łącza za pomocą polecenia modelu wdrażania klasycznego hello klasyczne sieci wirtualne i hello poleceń Menedżera zasobów dla sieci wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="eded1-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="eded1-144">Witaj następujące artykuły ułatwiają zarządzanie toohello łącza obwodu ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="eded1-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="eded1-145">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute w modelu wdrażania usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="eded1-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="eded1-146">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute w hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="eded1-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="eded1-147">toodisable ExpressRoute obwodu dostępu toohello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="eded1-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="eded1-148">Uruchom następujące polecenia cmdlet toodisable dostępu toohello klasycznego modelu wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="eded1-149">Uzyskiwanie szczegółowych informacji o hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="eded1-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="eded1-150">Ustaw tooFALSE "Zezwalaj na operacje klasycznym".</span><span class="sxs-lookup"><span data-stu-id="eded1-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="eded1-151">Zaktualizuj hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="eded1-151">Update hello circuit.</span></span> <span data-ttu-id="eded1-152">Po tej operacji zakończyło się pomyślnie, nie będzie możliwe tooview obwodu hello w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eded1-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="eded1-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eded1-153">Next steps</span></span>

* [<span data-ttu-id="eded1-154">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="eded1-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="eded1-155">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="eded1-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
