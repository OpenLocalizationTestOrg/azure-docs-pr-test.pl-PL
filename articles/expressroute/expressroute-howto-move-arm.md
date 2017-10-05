---
title: "Przenieś obwody usługi ExpressRoute ze środowiska klasycznego do Menedżera zasobów: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera opis sposobu przenieść obwodu klasycznego modelu wdrażania usługi Resource Manager przy użyciu programu PowerShell."
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
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="023ed-103">Przenieść obwody usługi ExpressRoute z klasycznego modelu wdrażania usługi Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="023ed-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="023ed-104">Aby używać obwodu usługi ExpressRoute dla klasycznego i modeli wdrażania usługi Resource Manager, należy przenieść obwodu do modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="023ed-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="023ed-105">Poniższe sekcje pomóc Przenieś obwodu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="023ed-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="023ed-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="023ed-106">Before you begin</span></span>

* <span data-ttu-id="023ed-107">Sprawdź, czy masz najnowszą wersję modułów programu Azure PowerShell (co najmniej w wersji 1.0).</span><span class="sxs-lookup"><span data-stu-id="023ed-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="023ed-108">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="023ed-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="023ed-109">Upewnij się, że użytkownik przejrzał [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="023ed-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="023ed-110">Przejrzyj informacje, które są przekazywane pod [przenoszenie obwodu usługi ExpressRoute z klasycznego do Menedżera zasobów](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="023ed-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="023ed-111">Upewnij się, że pełni rozumiesz limity i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="023ed-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="023ed-112">Sprawdź, że obwód jest w pełni funkcjonalna w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="023ed-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="023ed-113">Upewnij się, że masz grupę zasobów, który został utworzony w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="023ed-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="023ed-114">Przenieś obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="023ed-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="023ed-115">Krok 1: Zbieranie szczegółów obwód w klasycznym modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="023ed-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="023ed-116">Zaloguj się do klasycznego środowiska platformy Azure i zebrać klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="023ed-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="023ed-117">Zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="023ed-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="023ed-118">Wybierz odpowiednią subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="023ed-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="023ed-119">Zaimportuj moduły programu PowerShell platformy Azure i usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="023ed-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="023ed-120">Poniższe polecenie cmdlet umożliwia uzyskanie kluczy usługi dla wszystkich sieci obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="023ed-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="023ed-121">Po pobraniu klucze, skopiuj **klucza usługi** obwodu, który chcesz przenieść do modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="023ed-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="023ed-122">Krok 2: Zaloguj się i utworzyć grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="023ed-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="023ed-123">Zaloguj się do środowiska usługi Resource Manager i utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="023ed-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="023ed-124">Zaloguj się do środowiska usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="023ed-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="023ed-125">Wybierz odpowiednią subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="023ed-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="023ed-126">Zmodyfikuj fragment poniżej, aby utworzyć nową grupę zasobów, jeśli nie masz już grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="023ed-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="023ed-127">Krok 3: Przenieś obwodu ExpressRoute do modelu wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="023ed-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="023ed-128">Teraz można przystąpić do przenieść obwodu usługi ExpressRoute z klasycznym modelu wdrażania modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="023ed-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="023ed-129">Przed kontynuowaniem zapoznaj się z informacjami podanymi w [przenoszenie obwodu usługi ExpressRoute z klasycznego modelu wdrażania usługi Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="023ed-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="023ed-130">Aby przenieść obwodu, zmodyfikuj i uruchom następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="023ed-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="023ed-131">Po zakończeniu przenoszenia nową nazwę, która znajduje się w poprzednim poleceniu cmdlet będzie wykorzystywana do adresowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="023ed-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="023ed-132">Zasadniczo można zmienić nazwy obwodu.</span><span class="sxs-lookup"><span data-stu-id="023ed-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="023ed-133">Modyfikowania dostępu do obwodu</span><span class="sxs-lookup"><span data-stu-id="023ed-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="023ed-134">Aby włączyć dostęp obwodu ExpressRoute oba modele wdrażania</span><span class="sxs-lookup"><span data-stu-id="023ed-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="023ed-135">Po przeniesieniu obwodu ExpressRoute klasycznego modelu wdrażania usługi Resource Manager, możesz włączyć dostęp do obu modeli wdrażania.</span><span class="sxs-lookup"><span data-stu-id="023ed-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="023ed-136">Uruchom następujące polecenia cmdlet, aby umożliwić dostęp do obu modeli wdrażania:</span><span class="sxs-lookup"><span data-stu-id="023ed-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="023ed-137">Uzyskiwanie szczegółowych informacji obwodu.</span><span class="sxs-lookup"><span data-stu-id="023ed-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="023ed-138">Ustaw "Zezwalaj na operacje klasycznego" na wartość TRUE.</span><span class="sxs-lookup"><span data-stu-id="023ed-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="023ed-139">Zaktualizuj obwodu.</span><span class="sxs-lookup"><span data-stu-id="023ed-139">Update the circuit.</span></span> <span data-ttu-id="023ed-140">Po tej operacji zakończyło się pomyślnie, można wyświetlić w klasycznym modelu wdrażania obwodu.</span><span class="sxs-lookup"><span data-stu-id="023ed-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="023ed-141">Uruchom następujące polecenie cmdlet, aby uzyskać szczegóły obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="023ed-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="023ed-142">Musi być widoczna na liście klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="023ed-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="023ed-143">Możesz teraz zarządzać łącza do obwodu ExpressRoute, za pomocą poleceń modelu klasycznym wdrożenia klasyczne sieci wirtualne i polecenia Menedżera zasobów dla sieci wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="023ed-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="023ed-144">Następujące artykuły ułatwiają zarządzanie łącza do obwodu ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="023ed-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="023ed-145">Link sieci wirtualnej do obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="023ed-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="023ed-146">Link do obwodu usługi ExpressRoute w klasycznym modelu wdrożenia sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="023ed-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="023ed-147">Aby wyłączyć dostęp obwodu ExpressRoute do klasycznym modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="023ed-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="023ed-148">Uruchom następujące polecenia cmdlet, aby wyłączyć dostęp do klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="023ed-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="023ed-149">Uzyskiwanie szczegółowych informacji z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="023ed-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="023ed-150">Ustaw "Zezwalaj na operacje klasycznego" na wartość FALSE.</span><span class="sxs-lookup"><span data-stu-id="023ed-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="023ed-151">Zaktualizuj obwodu.</span><span class="sxs-lookup"><span data-stu-id="023ed-151">Update the circuit.</span></span> <span data-ttu-id="023ed-152">Po tej operacji zakończyło się pomyślnie, nie będzie mogła wyświetlać obwodu w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="023ed-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="023ed-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="023ed-153">Next steps</span></span>

* [<span data-ttu-id="023ed-154">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="023ed-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="023ed-155">Link sieci wirtualnej do obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="023ed-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)