---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: środowiska PowerShell: usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="6c012-103">Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c012-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c012-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6c012-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="6c012-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c012-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="6c012-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c012-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="6c012-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6c012-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="6c012-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="6c012-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="6c012-109">W tym artykule opisano sposób toocreate Azure ExpressRoute obwodu przy użyciu programu PowerShell hello i polecenia cmdlet usługi Azure Resource Manager modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6c012-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6c012-110">Ten artykuł zawiera także jak toocheck hello stanu obwodu hello, zaktualizuj lub usuń i anulowanie zastrzeżenia go.</span><span class="sxs-lookup"><span data-stu-id="6c012-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6c012-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6c012-111">Before you begin</span></span>
* <span data-ttu-id="6c012-112">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c012-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6c012-113">Aby uzyskać więcej informacji, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c012-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6c012-114">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="6c012-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="6c012-115">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="6c012-116">1. Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6c012-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="6c012-117">toobegin konfigurację logowania tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c012-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="6c012-118">Użyj hello następujące przykłady toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="6c012-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6c012-119">Sprawdź subskrypcje hello hello konta:</span><span class="sxs-lookup"><span data-stu-id="6c012-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6c012-120">Wybierz subskrypcję hello, która ma toocreate obwodu usługi expressroute dla:</span><span class="sxs-lookup"><span data-stu-id="6c012-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="6c012-121">2. Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości</span><span class="sxs-lookup"><span data-stu-id="6c012-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="6c012-122">Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.</span><span class="sxs-lookup"><span data-stu-id="6c012-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="6c012-123">polecenia cmdlet programu PowerShell Hello **Get AzureRmExpressRouteServiceProvider** zwraca informację, która będzie używana w dalszych krokach:</span><span class="sxs-lookup"><span data-stu-id="6c012-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="6c012-124">Określ, czy toosee podane jest dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="6c012-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="6c012-125">Zanotuj hello następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="6c012-125">Make a note of hello following information.</span></span> <span data-ttu-id="6c012-126">Należy go później podczas tworzenia obwodu.</span><span class="sxs-lookup"><span data-stu-id="6c012-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="6c012-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6c012-127">Name</span></span>
* <span data-ttu-id="6c012-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="6c012-128">PeeringLocations</span></span>
* <span data-ttu-id="6c012-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="6c012-129">BandwidthsOffered</span></span>

<span data-ttu-id="6c012-130">Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6c012-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="6c012-131">3. Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="6c012-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="6c012-132">Jeśli nie masz już grupę zasobów, należy go utworzyć przed utworzeniem obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6c012-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="6c012-133">Można to zrobić, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="6c012-134">Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej.</span><span class="sxs-lookup"><span data-stu-id="6c012-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="6c012-135">Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania.</span><span class="sxs-lookup"><span data-stu-id="6c012-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="6c012-136">Hello poniżej przedstawiono przykładowe żądanie dla nowego klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="6c012-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="6c012-137">Upewnij się, że określono hello prawidłowe jednostki SKU warstwy i rodzina jednostek SKU:</span><span class="sxs-lookup"><span data-stu-id="6c012-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="6c012-138">Jednostka SKU warstwy określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="6c012-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="6c012-139">Można określić *standardowe* tooget hello standardowy SKU lub *Premium* dla hello premium dodatku.</span><span class="sxs-lookup"><span data-stu-id="6c012-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="6c012-140">Rodzina jednostek SKU Określa typ rozliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="6c012-141">Można określić *Metereddata* planu dane naliczane i *Unlimiteddata* planu nieograniczone danych.</span><span class="sxs-lookup"><span data-stu-id="6c012-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="6c012-142">Można zmienić typu rozliczeń hello z *Metereddata* za*Unlimiteddata*, ale nie można zmienić typu hello z *Unlimiteddata* zbyt*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="6c012-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c012-143">Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6c012-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="6c012-144">Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="6c012-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="6c012-145">odpowiedź Hello zawiera hello klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="6c012-145">hello response contains hello service key.</span></span> <span data-ttu-id="6c012-146">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="6c012-147">4. Wyświetl listę wszystkich obwody usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="6c012-148">tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone, uruchom hello **Get-AzureRmExpressRouteCircuit** polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c012-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="6c012-149">odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="6c012-150">Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureRmExpressRouteCircuit` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c012-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="6c012-151">Tworzenie hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="6c012-152">Klucz usługi będzie wyświetlane w hello *bindingTemplate* pola:</span><span class="sxs-lookup"><span data-stu-id="6c012-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="6c012-153">odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6c012-154">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="6c012-155">5. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="6c012-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="6c012-156">*ServiceProviderProvisioningState* zawiera informacje o hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="6c012-157">Stan zawiera stan hello na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6c012-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="6c012-158">Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6c012-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="6c012-159">Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="6c012-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="6c012-160">obwodu Hello ulegnie zmianie po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello:</span><span class="sxs-lookup"><span data-stu-id="6c012-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="6c012-161">Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="6c012-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="6c012-162">6. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza</span><span class="sxs-lookup"><span data-stu-id="6c012-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="6c012-163">Sprawdzanie stanu hello i stan hello hello obwodu klucza informuje o tym, gdy dostawca jest włączony obwodu.</span><span class="sxs-lookup"><span data-stu-id="6c012-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="6c012-164">Po skonfigurowaniu obwodu hello *ServiceProviderProvisioningState* pojawia się jako *obsługiwane administracyjnie*, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="6c012-165">odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="6c012-166">7. Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="6c012-166">7. Create your routing configuration</span></span>
<span data-ttu-id="6c012-167">Aby uzyskać instrukcje krok po kroku, zobacz hello [obwodu ExpressRoute konfiguracji routingu](expressroute-howto-routing-arm.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="6c012-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c012-168">Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi.</span><span class="sxs-lookup"><span data-stu-id="6c012-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="6c012-169">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6c012-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="6c012-170">8. Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="6c012-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="6c012-171">Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="6c012-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="6c012-172">Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](expressroute-howto-linkvnet-arm.md) artykuł podczas pracy z modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="6c012-173">Pobieranie stanu hello obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="6c012-174">Te informacje w dowolnym momencie można pobrać za pomocą hello **Get-AzureRmExpressRouteCircuit** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c012-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="6c012-175">Tworzenie hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="6c012-176">odpowiedź Hello będzie toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6c012-177">Wyświetlane są informacje dotyczące określonego obwodu ExpressRoute, przekazując nazwy grupy zasobów hello i nazwy obwodu jako parametr toohello wywołanie:</span><span class="sxs-lookup"><span data-stu-id="6c012-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="6c012-178">odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6c012-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6c012-179">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="6c012-180"><a name="modify"></a>Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="6c012-181">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="6c012-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="6c012-182">Możesz zrobić hello po bez przestojów:</span><span class="sxs-lookup"><span data-stu-id="6c012-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="6c012-183">Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6c012-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="6c012-184">Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="6c012-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="6c012-185">Zmiana wersji na starszą hello przepustowości obwodu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6c012-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="6c012-186">Zmień hello planu z danych naliczane tooUnlimited danych pomiaru.</span><span class="sxs-lookup"><span data-stu-id="6c012-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="6c012-187">Zmiana hello pomiaru planu z tooMetered nieograniczone danych, danych nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6c012-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="6c012-188">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="6c012-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="6c012-189">Aby uzyskać więcej informacji na limity i ograniczenia, można znaleźć toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="6c012-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="6c012-190">Dodatek tooenable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="6c012-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="6c012-191">Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu, używając powitania po fragment środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6c012-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="6c012-192">obwód Hello będzie teraz hello ExpressRoute premium dodatkowe funkcje są włączone.</span><span class="sxs-lookup"><span data-stu-id="6c012-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="6c012-193">Rozpocznie się rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6c012-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="6c012-194">Dodatek toodisable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="6c012-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6c012-195">Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="6c012-196">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-196">Note hello following:</span></span>

* <span data-ttu-id="6c012-197">Przed zmienią premium toostandard upewnij się, że hello liczba sieci wirtualnych, które są połączone toohello obwód jest mniejsza niż 10.</span><span class="sxs-lookup"><span data-stu-id="6c012-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="6c012-198">Jeśli tego nie zrobisz, żądanie aktualizacji nie powiedzie się i firma Microsoft będzie naliczać opłaty możesz stawkami premium.</span><span class="sxs-lookup"><span data-stu-id="6c012-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="6c012-199">Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi.</span><span class="sxs-lookup"><span data-stu-id="6c012-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="6c012-200">Jeśli nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a firma Microsoft będzie naliczać opłaty możesz stawkami premium.</span><span class="sxs-lookup"><span data-stu-id="6c012-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="6c012-201">Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="6c012-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="6c012-202">Jeśli rozmiar tabeli tras jest większa niż 4000 tras, sesji BGP hello porzuca i nie będzie reenabled, aż przejdzie hello liczby prefiksów anonsowanych poniżej 4000.</span><span class="sxs-lookup"><span data-stu-id="6c012-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="6c012-203">Dodatek premium ExpressRoute hello dla istniejącego obwodu hello można wyłączyć za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="6c012-204">przepustowości obwodu ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="6c012-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="6c012-205">Dla opcji obsługiwanych przepustowości dla dostawcy, sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="6c012-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="6c012-206">Można wybrać żadnych rozmiar większy niż rozmiar hello z istniejącym obwodem.</span><span class="sxs-lookup"><span data-stu-id="6c012-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c012-207">Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności.</span><span class="sxs-lookup"><span data-stu-id="6c012-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="6c012-208">Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6c012-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="6c012-209">Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="6c012-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="6c012-210">Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6c012-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="6c012-211">Po wybraniu, jaki rozmiar, należy użyć następującego polecenia tooresize hello obwodu:</span><span class="sxs-lookup"><span data-stu-id="6c012-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="6c012-212">Obwodu będzie ustalany po stronie firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="6c012-213">Następnie należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="6c012-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="6c012-214">Po wprowadzeniu tego powiadomienia, rozpocznie się możesz rozliczeń dla opcji przepustowości hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="6c012-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="6c012-215">Witaj toomove SKU z naliczane toounlimited</span><span class="sxs-lookup"><span data-stu-id="6c012-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="6c012-216">Witaj SKU obwodu ExpressRoute można zmienić za pomocą powitania po fragment programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6c012-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="6c012-217">klasycznym toohello dostępu toocontrol i środowisk usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c012-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="6c012-218">Przejrzyj instrukcjami hello [Przenieś obwody usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6c012-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="6c012-219">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="6c012-220">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-220">Note hello following:</span></span>

* <span data-ttu-id="6c012-221">Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="6c012-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="6c012-222">Jeśli ta operacja nie powiedzie się, sprawdź, czy toosee, jeśli wszystkie sieci wirtualne są połączone toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="6c012-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="6c012-223">Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok.</span><span class="sxs-lookup"><span data-stu-id="6c012-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="6c012-224">Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.</span><span class="sxs-lookup"><span data-stu-id="6c012-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="6c012-225">Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="6c012-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="6c012-226">Spowoduje to zatrzymanie rozliczeń dla obwodu hello</span><span class="sxs-lookup"><span data-stu-id="6c012-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="6c012-227">Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6c012-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="6c012-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c012-228">Next steps</span></span>

<span data-ttu-id="6c012-229">Po utworzeniu obwodu, upewnij się, że hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6c012-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="6c012-230">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6c012-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="6c012-231">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="6c012-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
