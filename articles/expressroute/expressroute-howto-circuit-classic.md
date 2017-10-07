---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: środowiska PowerShell: klasyczny Portal Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej obwodu usługi ExpressRoute. Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="de4e8-104">Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="de4e8-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de4e8-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="de4e8-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="de4e8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de4e8-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="de4e8-107">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de4e8-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="de4e8-108">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="de4e8-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="de4e8-109">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="de4e8-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="de4e8-110">W tym artykule przedstawiono toocreate kroki hello obwodu usługi Azure ExpressRoute przy użyciu programu PowerShell polecenia cmdlet i hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="de4e8-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="de4e8-111">Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="de4e8-112">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="de4e8-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="de4e8-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="de4e8-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="de4e8-114">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="de4e8-114">Step 1.</span></span> <span data-ttu-id="de4e8-115">Przejrzyj wymagania wstępne hello i artykuły przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="de4e8-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="de4e8-116">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="de4e8-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="de4e8-117">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="de4e8-117">Step 2.</span></span> <span data-ttu-id="de4e8-118">Zainstaluj najnowsze wersje hello hello moduły programu PowerShell Azure usługi zarządzania (ko)</span><span class="sxs-lookup"><span data-stu-id="de4e8-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="de4e8-119">Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) wskazówki krok po kroku na temat tooconfigure moduły programu Azure PowerShell hello toouse komputera.</span><span class="sxs-lookup"><span data-stu-id="de4e8-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="de4e8-120">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="de4e8-120">Step 3.</span></span> <span data-ttu-id="de4e8-121">Zaloguj się za tooyour konto platformy Azure i wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="de4e8-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="de4e8-122">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="de4e8-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="de4e8-123">Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="de4e8-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="de4e8-124">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="de4e8-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="de4e8-125">Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="de4e8-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="de4e8-126">Następnie należy użyć następującego polecenia cmdlet tooadd hello tooPowerShell Twojej subskrypcji platformy Azure dla hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="de4e8-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="de4e8-127">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="de4e8-128">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="de4e8-128">Step 1.</span></span> <span data-ttu-id="de4e8-129">Zaimportuj hello moduły programu PowerShell dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="de4e8-130">Jeśli jeszcze nie należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello modułów hello Azure i usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="de4e8-131">Zaimportuj moduły hello z hello lokalizacji, które były zainstalowane tooon komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="de4e8-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="de4e8-132">W zależności od metody hello są używane moduły hello tooinstall, hello lokalizacji może być inna niż powitania po przykładzie.</span><span class="sxs-lookup"><span data-stu-id="de4e8-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="de4e8-133">W razie potrzeby zmodyfikować przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="de4e8-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="de4e8-134">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="de4e8-134">Step 2.</span></span> <span data-ttu-id="de4e8-135">Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości</span><span class="sxs-lookup"><span data-stu-id="de4e8-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="de4e8-136">Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.</span><span class="sxs-lookup"><span data-stu-id="de4e8-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="de4e8-137">polecenia cmdlet programu PowerShell Hello `Get-AzureDedicatedCircuitServiceProvider` zwraca informację, która będzie używana w dalszych krokach:</span><span class="sxs-lookup"><span data-stu-id="de4e8-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="de4e8-138">Określ, czy toosee podane jest dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="de4e8-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="de4e8-139">Zanotuj następujące informacje, ponieważ będzie on potrzebny później podczas tworzenia obwód hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="de4e8-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="de4e8-140">Name</span></span>
* <span data-ttu-id="de4e8-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="de4e8-141">PeeringLocations</span></span>
* <span data-ttu-id="de4e8-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="de4e8-142">BandwidthsOffered</span></span>

<span data-ttu-id="de4e8-143">Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="de4e8-144">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="de4e8-144">Step 3.</span></span> <span data-ttu-id="de4e8-145">Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="de4e8-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="de4e8-146">Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej.</span><span class="sxs-lookup"><span data-stu-id="de4e8-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="de4e8-147">Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania.</span><span class="sxs-lookup"><span data-stu-id="de4e8-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de4e8-148">Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="de4e8-149">Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="de4e8-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="de4e8-150">Hello poniżej przedstawiono przykładowe żądanie dla nowego klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="de4e8-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="de4e8-151">Lub, jeśli chcesz toocreate obwodu usługi ExpressRoute z dodatkiem premium hello hello Użyj poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="de4e8-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="de4e8-152">Zobacz toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów dotyczących dodatek hello w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="de4e8-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="de4e8-153">odpowiedź Hello będzie zawierać hello klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="de4e8-153">hello response will contain hello service key.</span></span> <span data-ttu-id="de4e8-154">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="de4e8-155">Krok 4.</span><span class="sxs-lookup"><span data-stu-id="de4e8-155">Step 4.</span></span> <span data-ttu-id="de4e8-156">Wyświetl listę wszystkich obwody usługi ExpressRoute hello</span><span class="sxs-lookup"><span data-stu-id="de4e8-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="de4e8-157">Możesz uruchomić hello `Get-AzureDedicatedCircuit` polecenia tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone:</span><span class="sxs-lookup"><span data-stu-id="de4e8-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="de4e8-158">odpowiedź Hello będzie coś podobnego toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="de4e8-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="de4e8-159">Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureDedicatedCircuit` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="de4e8-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="de4e8-160">Co hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="de4e8-161">Klucz usługi będzie wyświetlane w hello *bindingTemplate* pola.</span><span class="sxs-lookup"><span data-stu-id="de4e8-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="de4e8-162">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="de4e8-163">Krok 5.</span><span class="sxs-lookup"><span data-stu-id="de4e8-163">Step 5.</span></span> <span data-ttu-id="de4e8-164">Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="de4e8-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="de4e8-165">*ServiceProviderProvisioningState* zawiera informacje na temat hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="de4e8-166">*Stan* zawiera stan hello na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="de4e8-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="de4e8-167">Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.</span><span class="sxs-lookup"><span data-stu-id="de4e8-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="de4e8-168">Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="de4e8-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="de4e8-169">obwód Hello przejdzie toohello po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie:</span><span class="sxs-lookup"><span data-stu-id="de4e8-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="de4e8-170">Obwodu usługi ExpressRoute musi mieć następujące stan możesz toobe stanie toouse hello go:</span><span class="sxs-lookup"><span data-stu-id="de4e8-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="de4e8-171">Krok 6.</span><span class="sxs-lookup"><span data-stu-id="de4e8-171">Step 6.</span></span> <span data-ttu-id="de4e8-172">Okresowo sprawdzać stan hello i stan hello hello obwodu klucza</span><span class="sxs-lookup"><span data-stu-id="de4e8-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="de4e8-173">Dzięki temu można dowiedzieć się, gdy dostawca jest włączony obwodu.</span><span class="sxs-lookup"><span data-stu-id="de4e8-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="de4e8-174">Po skonfigurowaniu obwodu hello *ServiceProviderProvisioningState* będą wyświetlane jako *obsługiwane administracyjnie* pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="de4e8-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="de4e8-175">Krok 7.</span><span class="sxs-lookup"><span data-stu-id="de4e8-175">Step 7.</span></span> <span data-ttu-id="de4e8-176">Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="de4e8-176">Create your routing configuration</span></span>
<span data-ttu-id="de4e8-177">Zobacz toohello [obwodu ExpressRoute konfiguracji routingu (tworzenia i modyfikowania obwodu komunikacji równorzędnych)](expressroute-howto-routing-classic.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="de4e8-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de4e8-178">Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi.</span><span class="sxs-lookup"><span data-stu-id="de4e8-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="de4e8-179">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="de4e8-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="de4e8-180">Krok 8.</span><span class="sxs-lookup"><span data-stu-id="de4e8-180">Step 8.</span></span> <span data-ttu-id="de4e8-181">Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="de4e8-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="de4e8-182">Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="de4e8-183">Odwołuje się zbyt[połączeń ExpressRoute obwody sieci toovirtual](expressroute-howto-linkvnet-classic.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="de4e8-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="de4e8-184">Jeśli potrzebujesz toocreate sieć wirtualną przy użyciu hello klasycznego modelu wdrażania w przypadku połączeń ExpressRoute, zobacz [utworzyć sieć wirtualną w przypadku połączeń ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="de4e8-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="de4e8-185">Pobieranie stanu hello obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="de4e8-186">Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureCircuit` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="de4e8-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="de4e8-187">Co hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="de4e8-188">Przez przekazanie klucza usługi hello jako parametr wywołanie toohello można uzyskać informacji na temat określonych obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="de4e8-189">Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="de4e8-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="de4e8-190">Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="de4e8-191">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="de4e8-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="de4e8-192">Możesz zrobić hello po bez przestojów:</span><span class="sxs-lookup"><span data-stu-id="de4e8-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="de4e8-193">Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="de4e8-194">Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="de4e8-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="de4e8-195">Należy pamiętać, że zmiany na starszą wersję hello przepustowości obwodu nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="de4e8-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="de4e8-196">Zmień hello planu z danych naliczane tooUnlimited danych pomiaru.</span><span class="sxs-lookup"><span data-stu-id="de4e8-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="de4e8-197">Należy pamiętać, zmiana planu zliczania hello z tooMetered nieograniczone danych, danych nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="de4e8-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="de4e8-198">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="de4e8-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="de4e8-199">Zobacz toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) Aby uzyskać więcej informacji na temat limity i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="de4e8-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="de4e8-200">Dodatek tooenable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="de4e8-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="de4e8-201">Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="de4e8-202">Obwodu będzie teraz hello ExpressRoute premium dodatkowe funkcje są włączone.</span><span class="sxs-lookup"><span data-stu-id="de4e8-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="de4e8-203">Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="de4e8-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="de4e8-204">Dodatek toodisable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="de4e8-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="de4e8-205">Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="de4e8-206">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="de4e8-206">Considerations</span></span>

* <span data-ttu-id="de4e8-207">Należy się upewnić, numer hello obwodu toohello połączone sieci wirtualnych jest mniejsza niż 10, aby obniżyć z premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="de4e8-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="de4e8-208">Jeśli tego nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a będziesz rachunku hello premium stawki.</span><span class="sxs-lookup"><span data-stu-id="de4e8-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="de4e8-209">Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi.</span><span class="sxs-lookup"><span data-stu-id="de4e8-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="de4e8-210">Jeśli tego nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a będziesz rachunku hello premium stawki.</span><span class="sxs-lookup"><span data-stu-id="de4e8-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="de4e8-211">Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="de4e8-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="de4e8-212">Jeśli rozmiar tabeli tras jest większa niż 4000 tras, sesji BGP hello spowoduje porzucenie i nie będzie reenabled, aż przejdzie hello liczby prefiksów anonsowanych poniżej 4000.</span><span class="sxs-lookup"><span data-stu-id="de4e8-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="de4e8-213">Wyłącz dodatek hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="de4e8-213">Disable hello premium add-on</span></span>
<span data-ttu-id="de4e8-214">Dodatek premium ExpressRoute hello dla istniejącego obwodu można wyłączyć za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="de4e8-215">przepustowości obwodu ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="de4e8-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="de4e8-216">Sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) obsługiwane opcje przepustowości dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="de4e8-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="de4e8-217">Można wybrać żadnych ma rozmiar większy niż rozmiar hello obwodu istniejących tak długo, jak umożliwia hello fizyczny port (na którym jest tworzony obwodu).</span><span class="sxs-lookup"><span data-stu-id="de4e8-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de4e8-218">Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności.</span><span class="sxs-lookup"><span data-stu-id="de4e8-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="de4e8-219">Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="de4e8-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="de4e8-220">Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="de4e8-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="de4e8-221">Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="de4e8-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="de4e8-222">Zmień rozmiar obwodu</span><span class="sxs-lookup"><span data-stu-id="de4e8-222">Resize a circuit</span></span>

<span data-ttu-id="de4e8-223">Po wybraniu rozmiar, jaki należy można użyć następującego polecenia tooresize hello obwodu:</span><span class="sxs-lookup"><span data-stu-id="de4e8-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="de4e8-224">Obwodu będzie zostały wielkości po stronie firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="de4e8-225">Należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="de4e8-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="de4e8-226">Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń można uzyskać hello zaktualizować opcji przepustowości z tego punktu w.</span><span class="sxs-lookup"><span data-stu-id="de4e8-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="de4e8-227">Jeśli zostanie wyświetlony następujący błąd podczas zwiększyć przepustowość obwodu hello hello, to pozostaje nie wystarczającą przepustowość na fizyczny port hello, gdy jest tworzony z istniejącym obwodem.</span><span class="sxs-lookup"><span data-stu-id="de4e8-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="de4e8-228">Masz toodelete ten obwód i utworzyć nowy obwód rozmiar hello, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="de4e8-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="de4e8-229">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="de4e8-230">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="de4e8-230">Considerations</span></span>

* <span data-ttu-id="de4e8-231">Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute dla toosucceed tej operacji.</span><span class="sxs-lookup"><span data-stu-id="de4e8-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="de4e8-232">Sprawdź toosee, jeśli masz żadnych sieci wirtualnych, które są połączone obwodu toohello, jeśli ta operacja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="de4e8-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="de4e8-233">Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok.</span><span class="sxs-lookup"><span data-stu-id="de4e8-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="de4e8-234">Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.</span><span class="sxs-lookup"><span data-stu-id="de4e8-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="de4e8-235">Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="de4e8-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="de4e8-236">Spowoduje to zatrzymanie rozliczeń dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="de4e8-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="de4e8-237">Usunąć obwód</span><span class="sxs-lookup"><span data-stu-id="de4e8-237">Delete a circuit</span></span>

<span data-ttu-id="de4e8-238">Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="de4e8-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="de4e8-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de4e8-239">Next steps</span></span>
<span data-ttu-id="de4e8-240">Po utworzeniu obwodu, upewnij się, że hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de4e8-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="de4e8-241">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="de4e8-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="de4e8-242">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="de4e8-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

