---
title: "Tworzenie i modyfikowanie obwodu usługi Azure ExpressRoute: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="a7545-103">Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a7545-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="a7545-104">W tym artykule opisano, jak toocreate obwodu Azure ExpressRoute przy użyciu hello interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="a7545-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="a7545-105">Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu.</span><span class="sxs-lookup"><span data-stu-id="a7545-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="a7545-106">Jeśli chcesz toouse toowork inną metodę z obwody usługi ExpressRoute, można wybrać artykuł hello z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="a7545-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7545-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a7545-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="a7545-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7545-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="a7545-109">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a7545-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="a7545-110">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a7545-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="a7545-111">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="a7545-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="a7545-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a7545-112">Before you begin</span></span>

* <span data-ttu-id="a7545-113">Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="a7545-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="a7545-114">Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli) i [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7545-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="a7545-115">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="a7545-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="a7545-116">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7545-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="a7545-117">1. Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a7545-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="a7545-118">toobegin konfigurację logowania tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a7545-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="a7545-119">Użyj hello następujące przykłady toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="a7545-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="a7545-120">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="a7545-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="a7545-121">Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="a7545-122">2. Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości</span><span class="sxs-lookup"><span data-stu-id="a7545-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="a7545-123">Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.</span><span class="sxs-lookup"><span data-stu-id="a7545-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="a7545-124">Hello interfejsu wiersza polecenia polecenie "az sieci express route listy--usługodawców" zwraca informację, która będzie używana w dalszych krokach:</span><span class="sxs-lookup"><span data-stu-id="a7545-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="a7545-125">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a7545-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="a7545-126">Sprawdź hello toosee odpowiedzi, jeśli znajduje się dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="a7545-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="a7545-127">Zanotuj następujące informacje, które należy podczas tworzenia obwód hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="a7545-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a7545-128">Name</span></span>
* <span data-ttu-id="a7545-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="a7545-129">PeeringLocations</span></span>
* <span data-ttu-id="a7545-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="a7545-130">BandwidthsOffered</span></span>

<span data-ttu-id="a7545-131">Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="a7545-132">3. Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="a7545-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7545-133">Jest on rozliczany od momentu hello wygenerowaniu klucza usługi obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="a7545-134">Tę operację należy wykonać, gdy dostawca łączności hello jest gotowy tooprovision hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="a7545-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="a7545-135">Jeśli nie masz już grupę zasobów, należy go utworzyć przed utworzeniem obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="a7545-136">Można utworzyć grupę zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="a7545-137">Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej.</span><span class="sxs-lookup"><span data-stu-id="a7545-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="a7545-138">Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania.</span><span class="sxs-lookup"><span data-stu-id="a7545-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="a7545-139">Upewnij się, że określono hello prawidłowe jednostki SKU warstwy i rodzina jednostek SKU:</span><span class="sxs-lookup"><span data-stu-id="a7545-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="a7545-140">Jednostka SKU warstwy określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="a7545-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="a7545-141">Można określić "Standardowy" hello tooget standardowy SKU lub "Premium" dla hello premium dodatku.</span><span class="sxs-lookup"><span data-stu-id="a7545-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="a7545-142">Rodzina jednostek SKU Określa typ rozliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="a7545-143">"Metereddata" można określić dla planu dane naliczane i "Unlimiteddata" planu dane nieograniczone.</span><span class="sxs-lookup"><span data-stu-id="a7545-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="a7545-144">Można zmienić typu rozliczeń hello z "Metereddata"too'Unlimiteddata", ale nie można zmienić typu hello z too'Metereddata"Unlimiteddata"".</span><span class="sxs-lookup"><span data-stu-id="a7545-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="a7545-145">Jest on rozliczany od momentu hello wygenerowaniu klucza usługi obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="a7545-146">Poniższy przykład Hello jest żądaniem klucza usługi:</span><span class="sxs-lookup"><span data-stu-id="a7545-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="a7545-147">odpowiedź Hello zawiera hello klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="a7545-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="a7545-148">4. Wyświetl listę wszystkich obwody usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7545-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="a7545-149">tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone, uruchom polecenie "Lista express route sieci az" hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="a7545-150">Te informacje w dowolnym momencie można pobrać za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7545-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="a7545-151">toolist wszystkich obwodów należy hello wywołania bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="a7545-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="a7545-152">Klucz usługi ma na liście hello *bindingTemplate* pole hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a7545-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="a7545-153">Aby uzyskać szczegółowy opis wszystkich parametrów hello, uruchomione polecenie hello przy użyciu hello "-h" parametru.</span><span class="sxs-lookup"><span data-stu-id="a7545-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="a7545-154">5. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="a7545-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="a7545-155">"ServiceProviderProvisioningState" zawiera informacje o hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="a7545-156">Stan Hello zawiera stan hello na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7545-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="a7545-157">Aby uzyskać więcej informacji, zobacz hello [artykułu przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="a7545-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="a7545-158">Podczas tworzenia nowego obwodu ExpressRoute obwodu hello jest powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="a7545-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="a7545-159">następujące stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello zmiany obwodu Hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="a7545-160">Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="a7545-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="a7545-161">6. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza</span><span class="sxs-lookup"><span data-stu-id="a7545-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="a7545-162">Sprawdzanie stanu hello i stan hello hello obwodu klucza informuje o tym, gdy dostawca jest włączony obwodu.</span><span class="sxs-lookup"><span data-stu-id="a7545-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="a7545-163">Po skonfigurowaniu obwodu hello "ServiceProviderProvisioningState" pojawia się jako "Obsługiwane administracyjnie", jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a7545-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="a7545-164">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a7545-164">hello response is similar toohello following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="a7545-165">7. Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="a7545-165">7. Create your routing configuration</span></span>

<span data-ttu-id="a7545-166">Aby uzyskać instrukcje krok po kroku, zobacz hello [obwodu ExpressRoute konfiguracji routingu](howto-routing-cli.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="a7545-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7545-167">Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi.</span><span class="sxs-lookup"><span data-stu-id="a7545-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="a7545-168">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia konfiguruje i zarządza nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a7545-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="a7545-169">8. Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="a7545-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="a7545-170">Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="a7545-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a7545-171">Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](howto-linkvnet-cli.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a7545-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="a7545-172"><a name="modify"></a>Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7545-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="a7545-173">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="a7545-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="a7545-174">Możesz wprowadzić następujące zmiany bez przestojów hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="a7545-175">Można włączyć lub wyłączyć dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="a7545-176">Można zwiększyć hello przepustowości obwodu ExpressRoute, pod warunkiem na porcie hello jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="a7545-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="a7545-177">Jednak hello przepustowości obwodu zmiana wersji na starszą nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a7545-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="a7545-178">Można zmienić planu zliczania hello naliczane danych tooUnlimited danych.</span><span class="sxs-lookup"><span data-stu-id="a7545-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="a7545-179">Jednak zmiana hello pomiaru planu z tooMetered nieograniczone danych, danych nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a7545-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="a7545-180">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="a7545-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="a7545-181">Aby uzyskać więcej informacji na limity i ograniczenia, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a7545-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="a7545-182">Dodatek tooenable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="a7545-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="a7545-183">Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="a7545-184">obwód Hello ma teraz włączone hello ExpressRoute premium dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="a7545-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="a7545-185">Zaczniemy rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a7545-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="a7545-186">Dodatek toodisable ExpressRoute hello w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="a7545-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7545-187">Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="a7545-188">Przed wyłączeniem hello dodatek usługi ExpressRoute w warstwie premium, zrozumieć hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="a7545-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="a7545-189">Przed zmienią premium toostandard użytkownik musi upewnić się, że masz mniej niż 10 obwodu toohello połączone sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="a7545-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="a7545-190">Jeśli masz więcej niż 10 żądania aktualizacji zakończy się niepowodzeniem, a nas rachunku stawkami premium.</span><span class="sxs-lookup"><span data-stu-id="a7545-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="a7545-191">Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi.</span><span class="sxs-lookup"><span data-stu-id="a7545-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="a7545-192">Jeśli nie można odłączyć wszystkie sieci wirtualne, żądanie aktualizacji nie powiedzie się i NAS rachunku stawkami premium.</span><span class="sxs-lookup"><span data-stu-id="a7545-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="a7545-193">Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="a7545-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="a7545-194">Jeśli rozmiar tabeli tras jest większa niż 4000 tras, porzuca hello sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="a7545-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="a7545-195">Hello sesji nie reenabled, dopóki nie zostanie hello liczby prefiksów anonsowanych poniżej 4000.</span><span class="sxs-lookup"><span data-stu-id="a7545-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="a7545-196">Dodatek premium ExpressRoute hello dla istniejącego obwodu hello można wyłączyć za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a7545-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="a7545-197">przepustowości obwodu ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="a7545-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="a7545-198">Dla opcji przepustowości hello obsługiwane dla dostawcy, sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a7545-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="a7545-199">Można wybrać żadnych rozmiar większy niż rozmiar hello z istniejącym obwodem.</span><span class="sxs-lookup"><span data-stu-id="a7545-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7545-200">Jeśli na powitania istniejącego portu jest nieodpowiedni pojemności, może być obwodu ExpressRoute hello toorecreate.</span><span class="sxs-lookup"><span data-stu-id="a7545-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="a7545-201">Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a7545-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="a7545-202">Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="a7545-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="a7545-203">Zmiany na starszą wersję przepustowości wymaga możesz toodeprovision hello obwodu usługi expressroute, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7545-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="a7545-204">Po wybraniu rozmiar hello, należy użyć następującego polecenia tooresize hello obwodu:</span><span class="sxs-lookup"><span data-stu-id="a7545-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="a7545-205">Obwodu jest o rozmiarze po stronie firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="a7545-206">Następnie należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="a7545-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="a7545-207">Po wprowadzeniu tego powiadomienia, możemy rozpocząć rozliczeń można opcji przepustowości hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="a7545-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="a7545-208">Witaj toomove SKU z naliczane toounlimited</span><span class="sxs-lookup"><span data-stu-id="a7545-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="a7545-209">Witaj SKU obwodu ExpressRoute można zmienić za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a7545-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="a7545-210">klasycznym toohello dostępu toocontrol i środowisk usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a7545-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="a7545-211">Przejrzyj instrukcjami hello [Przenieś obwody usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a7545-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="a7545-212">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7545-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="a7545-213">toodeprovision i delete obwodu usługi ExpressRoute, upewnij się, że rozumiesz hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="a7545-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="a7545-214">Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="a7545-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="a7545-215">Jeśli ta operacja nie powiedzie się, sprawdź, czy toosee, jeśli wszystkie sieci wirtualne są połączone toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="a7545-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="a7545-216">Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie**, należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok.</span><span class="sxs-lookup"><span data-stu-id="a7545-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="a7545-217">Firma Microsoft może nadal tooreserve zasobów, a następnie obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.</span><span class="sxs-lookup"><span data-stu-id="a7545-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="a7545-218">Dostawcy usług hello została anulowana obwodu hello można usunąć obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="a7545-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="a7545-219">Gdy obwód jest anulowana, dostawcy usług hello stan inicjowania obsługi jest ustawiany za**nieudostępniane**.</span><span class="sxs-lookup"><span data-stu-id="a7545-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="a7545-220">Powoduje to zatrzymanie rozliczeń dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="a7545-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="a7545-221">Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="a7545-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a7545-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7545-222">Next steps</span></span>

<span data-ttu-id="a7545-223">Po utworzeniu obwodu, upewnij się, że hello następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="a7545-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="a7545-224">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7545-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="a7545-225">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="a7545-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
