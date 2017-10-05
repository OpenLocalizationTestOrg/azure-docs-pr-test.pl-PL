---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: środowiska PowerShell: klasyczny Portal Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki tworzenia i inicjowania obsługi administracyjnej obwodu usługi ExpressRoute. W tym artykule przedstawiono również sposób sprawdzania stanu, update lub delete i anulowanie zastrzeżenia obwodu."
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
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="909e0-104">Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="909e0-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="909e0-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="909e0-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="909e0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="909e0-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="909e0-107">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="909e0-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="909e0-108">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="909e0-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="909e0-109">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="909e0-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="909e0-110">W tym artykule przedstawiono kroki, aby utworzyć obwodu usługi Azure ExpressRoute przy użyciu poleceń cmdlet programu PowerShell i klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="909e0-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="909e0-111">W tym artykule przedstawiono również sposób sprawdzania stanu, update lub delete i anulowanie zastrzeżenia obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="909e0-112">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="909e0-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="909e0-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="909e0-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="909e0-114">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="909e0-114">Step 1.</span></span> <span data-ttu-id="909e0-115">Przejrzyj wymagania wstępne i artykuły przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="909e0-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="909e0-116">Upewnij się, że użytkownik przejrzał [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="909e0-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="909e0-117">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="909e0-117">Step 2.</span></span> <span data-ttu-id="909e0-118">Zainstaluj najnowsze wersje moduły programu PowerShell Azure usługi zarządzania (ko)</span><span class="sxs-lookup"><span data-stu-id="909e0-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="909e0-119">Postępuj zgodnie z instrukcjami [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) wskazówki krok po kroku dotyczące sposobu konfigurowania komputera do modułów programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="909e0-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="909e0-120">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="909e0-120">Step 3.</span></span> <span data-ttu-id="909e0-121">Zaloguj się do konta platformy Azure i wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="909e0-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="909e0-122">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="909e0-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="909e0-123">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="909e0-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="909e0-124">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="909e0-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="909e0-125">Jeśli masz więcej niż jedną subskrypcję, wybierz tę, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="909e0-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="909e0-126">Następnie użyj następującego polecenia cmdlet można dodać subskrypcji platformy Azure do środowiska PowerShell dla klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="909e0-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="909e0-127">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="909e0-128">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="909e0-128">Step 1.</span></span> <span data-ttu-id="909e0-129">Zaimportuj moduły programu PowerShell dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="909e0-130">Jeśli jeszcze nie, aby rozpocząć korzystanie z poleceń cmdlet programu ExpressRoute należy zaimportować moduły Azure i usługi ExpressRoute w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="909e0-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="909e0-131">Moduły importowania w lokalizacji, w jakiej zostały wcześniej zainstalowane na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="909e0-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="909e0-132">W zależności od metody użytej do instalowania modułów lokalizacja może być inna niż w poniższym przykładzie pokazano.</span><span class="sxs-lookup"><span data-stu-id="909e0-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="909e0-133">W razie potrzeby zmodyfikować przykładzie.</span><span class="sxs-lookup"><span data-stu-id="909e0-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="909e0-134">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="909e0-134">Step 2.</span></span> <span data-ttu-id="909e0-135">Pobierz listę obsługiwanych dostawców, lokalizacji i przepustowości</span><span class="sxs-lookup"><span data-stu-id="909e0-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="909e0-136">Przed utworzeniem obwodu usługi ExpressRoute, należy listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.</span><span class="sxs-lookup"><span data-stu-id="909e0-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="909e0-137">Polecenia cmdlet programu PowerShell `Get-AzureDedicatedCircuitServiceProvider` zwraca informację, która będzie używana w dalszych krokach:</span><span class="sxs-lookup"><span data-stu-id="909e0-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="909e0-138">Sprawdź, czy dostawca połączenia znajduje się tam.</span><span class="sxs-lookup"><span data-stu-id="909e0-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="909e0-139">Ponieważ będzie on potrzebny później podczas tworzenia obwód, zwróć uwagę następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="909e0-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="909e0-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="909e0-140">Name</span></span>
* <span data-ttu-id="909e0-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="909e0-141">PeeringLocations</span></span>
* <span data-ttu-id="909e0-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="909e0-142">BandwidthsOffered</span></span>

<span data-ttu-id="909e0-143">Teraz możesz utworzyć obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="909e0-144">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="909e0-144">Step 3.</span></span> <span data-ttu-id="909e0-145">Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="909e0-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="909e0-146">Poniższy przykład przedstawia sposób tworzenia obwodu ExpressRoute za pośrednictwem Equinix 200-MB/s w Dolinie Krzemowej.</span><span class="sxs-lookup"><span data-stu-id="909e0-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="909e0-147">Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania.</span><span class="sxs-lookup"><span data-stu-id="909e0-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="909e0-148">Od momentu jego wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="909e0-149">Upewnij się, gdy dostawca łączności jest gotowy do udostępniania obwodu podczas wykonywania tej operacji.</span><span class="sxs-lookup"><span data-stu-id="909e0-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="909e0-150">Poniżej zamieszczono przykładowe żądanie dla nowego klucza usługi:</span><span class="sxs-lookup"><span data-stu-id="909e0-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="909e0-151">Lub, jeśli chcesz utworzyć obwodu usługi ExpressRoute z dodatkiem premium, skorzystaj z następującego przykładu.</span><span class="sxs-lookup"><span data-stu-id="909e0-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="909e0-152">Zapoznaj się [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów dotyczących dodatek w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="909e0-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="909e0-153">Odpowiedź będzie zawierać klucz usługi.</span><span class="sxs-lookup"><span data-stu-id="909e0-153">The response will contain the service key.</span></span> <span data-ttu-id="909e0-154">Szczegółowy opis wszystkich parametrów można uzyskać, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="909e0-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="909e0-155">Krok 4.</span><span class="sxs-lookup"><span data-stu-id="909e0-155">Step 4.</span></span> <span data-ttu-id="909e0-156">Wyświetl listę wszystkich obwody usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="909e0-157">Można uruchomić `Get-AzureDedicatedCircuit` polecenie, aby uzyskać listę wszystkich obwody usługi ExpressRoute, które zostały utworzone:</span><span class="sxs-lookup"><span data-stu-id="909e0-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="909e0-158">Odpowiedź będzie miała podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="909e0-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="909e0-159">Te informacje w dowolnym momencie można pobrać za pomocą `Get-AzureDedicatedCircuit` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="909e0-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="909e0-160">Wywołania bez parametrów wyświetla listę wszystkich obwodów.</span><span class="sxs-lookup"><span data-stu-id="909e0-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="909e0-161">Klucz usługi będzie wyświetlane w *bindingTemplate* pola.</span><span class="sxs-lookup"><span data-stu-id="909e0-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="909e0-162">Szczegółowy opis wszystkich parametrów można uzyskać, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="909e0-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="909e0-163">Krok 5.</span><span class="sxs-lookup"><span data-stu-id="909e0-163">Step 5.</span></span> <span data-ttu-id="909e0-164">Wyślij klucz usługi do dostawcą połączenia do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="909e0-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="909e0-165">*ServiceProviderProvisioningState* zawiera informacje o bieżącym stanie inicjowania obsługi administracyjnej po stronie dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="909e0-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="909e0-166">*Stan* zapewnia stanu po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909e0-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="909e0-167">Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów zobacz [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.</span><span class="sxs-lookup"><span data-stu-id="909e0-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="909e0-168">Podczas tworzenia nowego obwodu ExpressRoute obwodu będą w następującym stanie:</span><span class="sxs-lookup"><span data-stu-id="909e0-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="909e0-169">Gdy dostawca połączenia trwa jej włączanie, obwodu przejdzie na następujący:</span><span class="sxs-lookup"><span data-stu-id="909e0-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="909e0-170">Obwodu usługi ExpressRoute musi być w następującym stanie dla Ciebie można było użyć go:</span><span class="sxs-lookup"><span data-stu-id="909e0-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="909e0-171">Krok 6.</span><span class="sxs-lookup"><span data-stu-id="909e0-171">Step 6.</span></span> <span data-ttu-id="909e0-172">Okresowo sprawdzać stan i stan klucz obwodu</span><span class="sxs-lookup"><span data-stu-id="909e0-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="909e0-173">Dzięki temu można dowiedzieć się, gdy dostawca jest włączony obwodu.</span><span class="sxs-lookup"><span data-stu-id="909e0-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="909e0-174">Po skonfigurowaniu obwodu *ServiceProviderProvisioningState* będą wyświetlane jako *obsługiwane administracyjnie* jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="909e0-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="909e0-175">Krok 7.</span><span class="sxs-lookup"><span data-stu-id="909e0-175">Step 7.</span></span> <span data-ttu-id="909e0-176">Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="909e0-176">Create your routing configuration</span></span>
<span data-ttu-id="909e0-177">Zapoznaj się [obwodu ExpressRoute konfiguracji routingu (tworzenia i modyfikowania obwodu komunikacji równorzędnych)](expressroute-howto-routing-classic.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="909e0-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="909e0-178">Te instrukcje dotyczą tylko obwody, które zostały utworzone z dostawców usług, które oferują warstwy 2 łączności usługi.</span><span class="sxs-lookup"><span data-stu-id="909e0-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="909e0-179">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="909e0-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="909e0-180">Krok 8.</span><span class="sxs-lookup"><span data-stu-id="909e0-180">Step 8.</span></span> <span data-ttu-id="909e0-181">Łączenie sieci wirtualnej z obwodem usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="909e0-182">Następnie połączyć sieć wirtualną obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="909e0-183">Zapoznaj się [łączenie obwody usługi ExpressRoute z siecią wirtualną](expressroute-howto-linkvnet-classic.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="909e0-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="909e0-184">Jeśli chcesz utworzyć sieć wirtualną przy użyciu klasycznego modelu wdrażania w przypadku połączeń ExpressRoute, zobacz [utworzyć sieć wirtualną w przypadku połączeń ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="909e0-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="909e0-185">Pobieranie stanu obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="909e0-186">Te informacje w dowolnym momencie można pobrać za pomocą `Get-AzureCircuit` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="909e0-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="909e0-187">Wywołania bez parametrów wyświetla listę wszystkich obwodów.</span><span class="sxs-lookup"><span data-stu-id="909e0-187">Making the call without any parameters lists all the circuits.</span></span>

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

<span data-ttu-id="909e0-188">Można uzyskać informacji o określonych obwodu ExpressRoute przez przekazanie klucza usługi jako parametru do wywołania.</span><span class="sxs-lookup"><span data-stu-id="909e0-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="909e0-189">Szczegółowy opis wszystkich parametrów można uzyskać, uruchamiając w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="909e0-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="909e0-190">Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="909e0-191">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="909e0-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="909e0-192">Można wykonać następujące czynności bez przestojów:</span><span class="sxs-lookup"><span data-stu-id="909e0-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="909e0-193">Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="909e0-194">Zwiększyć przepustowość obwodu ExpressRoute dostarczane na port jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="909e0-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="909e0-195">Należy pamiętać, że przepustowość obwodu zmiana wersji na starszą nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="909e0-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="909e0-196">Zmiana zliczania planu naliczane danych nieograniczone danych.</span><span class="sxs-lookup"><span data-stu-id="909e0-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="909e0-197">Należy pamiętać, że zmiana zliczania planu z dane nieograniczone naliczane danych nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="909e0-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="909e0-198">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="909e0-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="909e0-199">Zapoznaj się [ExpressRoute — często zadawane pytania](expressroute-faqs.md) Aby uzyskać więcej informacji na temat limity i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="909e0-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="909e0-200">Aby włączyć dodatek usługi ExpressRoute w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="909e0-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="909e0-201">Dodatek usługi ExpressRoute w warstwie premium dla istniejącego obwodu można włączyć za pomocą następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="909e0-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="909e0-202">Obwodu mają teraz włączonymi funkcjami dodatek premium usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="909e0-203">Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń dla funkcji dodatku premium, jak polecenie zostało pomyślnie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="909e0-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="909e0-204">Aby wyłączyć dodatek usługi ExpressRoute w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="909e0-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="909e0-205">Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla standardowych obwodu.</span><span class="sxs-lookup"><span data-stu-id="909e0-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="909e0-206">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="909e0-206">Considerations</span></span>

* <span data-ttu-id="909e0-207">Należy się upewnić, liczba sieci wirtualnych powiązany obwodu jest mniejsza niż 10, aby obniżyć z premium standard.</span><span class="sxs-lookup"><span data-stu-id="909e0-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="909e0-208">Jeśli nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem i będzie rozliczane stawki premium.</span><span class="sxs-lookup"><span data-stu-id="909e0-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="909e0-209">Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi.</span><span class="sxs-lookup"><span data-stu-id="909e0-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="909e0-210">Jeśli nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem i będzie rozliczane stawki premium.</span><span class="sxs-lookup"><span data-stu-id="909e0-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="909e0-211">Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="909e0-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="909e0-212">Jeśli rozmiar tabeli tras jest większa niż 4000 tras, sesji BGP spowoduje porzucenie i nie będzie reenabled, aż przejdzie liczby prefiksów anonsowanych poniżej 4000.</span><span class="sxs-lookup"><span data-stu-id="909e0-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="909e0-213">Wyłącz dodatek w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="909e0-213">Disable the premium add-on</span></span>
<span data-ttu-id="909e0-214">Dodatek usługi ExpressRoute w warstwie premium dla istniejącego obwodu można wyłączyć za pomocą następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="909e0-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="909e0-215">Aby zaktualizować przepustowości obwodu ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="909e0-216">Sprawdź [ExpressRoute — często zadawane pytania](expressroute-faqs.md) obsługiwane opcje przepustowości dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="909e0-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="909e0-217">Można wybrać żadnych ma rozmiar większy niż rozmiar z istniejącym obwodem tak długo, jak zezwala na fizyczny port (na którym jest tworzony obwodu).</span><span class="sxs-lookup"><span data-stu-id="909e0-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="909e0-218">Może być konieczne ponowne utworzenie obwodu usługi expressroute w przypadku niewystarczającego pojemności na istniejącego portu.</span><span class="sxs-lookup"><span data-stu-id="909e0-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="909e0-219">Nie można uaktualnić obwodu, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="909e0-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="909e0-220">Nie można zmniejszyć przepustowość obwodu usługi ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="909e0-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="909e0-221">Zmiana wersji na starszą przepustowości wymaga anulowanie zastrzeżenia obwodu ExpressRoute, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="909e0-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="909e0-222">Zmień rozmiar obwodu</span><span class="sxs-lookup"><span data-stu-id="909e0-222">Resize a circuit</span></span>

<span data-ttu-id="909e0-223">Po wybraniu rozmiar, jaki należy można Użyj następującego polecenia, aby zmienić rozmiar obwodu:</span><span class="sxs-lookup"><span data-stu-id="909e0-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="909e0-224">Obwodu będzie zostały wielkości po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909e0-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="909e0-225">Należy skontaktuj się z dostawcą połączenia można zaktualizować konfiguracji na bok odpowiadające tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="909e0-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="909e0-226">Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń można opcji przepustowości zaktualizowane z tego punktu na.</span><span class="sxs-lookup"><span data-stu-id="909e0-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="909e0-227">Jeśli zostanie wyświetlony następujący błąd podczas zwiększyć przepustowość obwodu, to pozostaje nie wystarczającą przepustowość na fizyczny port, na której jest tworzony z istniejącym obwodem.</span><span class="sxs-lookup"><span data-stu-id="909e0-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="909e0-228">Należy usunąć ten obwód i utworzyć nowy obwód rozmiaru, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="909e0-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="909e0-229">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="909e0-230">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="909e0-230">Considerations</span></span>

* <span data-ttu-id="909e0-231">Należy odłączyć wszystkie sieci wirtualne z obwodem usługi ExpressRoute, ta operacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="909e0-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="909e0-232">Sprawdź, czy masz żadnych sieci wirtualnych, które są połączone z obwodem, jeśli ta operacja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="909e0-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="909e0-233">Jeśli dostawca usługi obwodu ExpressRoute stan inicjowania obsługi jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z dostawcą usług na anulowanie zastrzeżenia obwód w bok.</span><span class="sxs-lookup"><span data-stu-id="909e0-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="909e0-234">Firma Microsoft będzie zarezerwować zasobów i obciążać Cię do czasu dostawcy usług wykonuje anulowania obsługi obwodu i powiadomienia NAS.</span><span class="sxs-lookup"><span data-stu-id="909e0-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="909e0-235">Jeśli usługodawca została anulowana obwodu (ustawiono dostawcę usługi stan inicjowania obsługi **nieudostępniane**) następnie można usunąć obwodu.</span><span class="sxs-lookup"><span data-stu-id="909e0-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="909e0-236">Spowoduje to zatrzymanie rozliczeń dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="909e0-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="909e0-237">Usunąć obwód</span><span class="sxs-lookup"><span data-stu-id="909e0-237">Delete a circuit</span></span>

<span data-ttu-id="909e0-238">Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="909e0-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="909e0-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="909e0-239">Next steps</span></span>
<span data-ttu-id="909e0-240">Po utworzeniu obwodu, upewnij się, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="909e0-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="909e0-241">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="909e0-242">Link sieci wirtualnej do obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="909e0-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

