---
title: "Konfigurowanie routingu dla obwodu usługi Azure ExpressRoute: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Ten artykuł ułatwia tworzenie i przydzielanie prywatny, publiczny i obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. W tym artykule opisano również, jak aktualizować i usuwać komunikację równoległą dla obwodu oraz sprawdzać jej stan."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="3cb3b-104">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3cb3b-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="3cb3b-105">W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="3cb3b-106">Można również sprawdzić stan, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="3cb3b-107">Jeśli chcesz użyć innej metody do pracy z obwodu, wybierz artykułu z poniższej listy:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cb3b-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3cb3b-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="3cb3b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cb3b-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="3cb3b-110">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="3cb3b-111">Video - prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3cb3b-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3cb3b-112">Video - publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3cb3b-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3cb3b-113">Video - komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3cb3b-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="3cb3b-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="3cb3b-115">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3cb3b-115">Configuration prerequisites</span></span>

* <span data-ttu-id="3cb3b-116">Przed rozpoczęciem zainstaluj najnowszą wersję poleceń interfejsu wiersza polecenia (wersję 2.0 lub nowszą).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="3cb3b-117">Aby uzyskać informacje o instalowaniu poleceń interfejsu wiersza polecenia, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="3cb3b-118">Upewnij się, że użytkownik przejrzał [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływu pracy](expressroute-workflows.md) strony przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="3cb3b-119">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="3cb3b-120">Zanim przejdziesz dalej, postępuj zgodnie z instrukcjami, aby [utworzyć obwód usługi ExpressRoute](howto-circuit-cli.md), który powinien zostać włączony przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="3cb3b-121">Obwód usługi expressroute musi być w stanie elastycznie i włączona można będzie można uruchamiać polecenia w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="3cb3b-122">Te instrukcje dotyczą tylko obwodów utworzonych przy pomocy dostawców oferujących usługi łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="3cb3b-123">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="3cb3b-124">Można skonfigurować jedną, dwie lub wszystkich trzech komunikacji równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="3cb3b-125">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="3cb3b-126">Musisz jednak pamiętać, aby kończyć konfiguracje poszczególnych komunikacji równorzędnych pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="3cb3b-127">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-127">Azure private peering</span></span>

<span data-ttu-id="3cb3b-128">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="3cb3b-129">Aby utworzyć prywatną komunikację równorzędną</span><span class="sxs-lookup"><span data-stu-id="3cb3b-129">To create Azure private peering</span></span>

1. <span data-ttu-id="3cb3b-130">Zainstaluj najnowszą wersję interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3cb3b-131">Należy użyć najnowszej wersji programu Azure interfejsu wiersza polecenia (CLI). * przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3cb3b-132">Wybierz subskrypcję, w ramach której chcesz utworzyć obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3cb3b-133">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3cb3b-134">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](howto-circuit-cli.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3cb3b-135">Jeśli dostawca połączenia oferuje zarządzane usługi warstwy 3, możesz poprosić go o włączenie prywatnej komunikacji równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3cb3b-136">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3cb3b-137">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="3cb3b-138">Sprawdź obwodu ExpressRoute, aby upewnić się, jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3cb3b-139">Skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="3cb3b-140">Odpowiedź jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-140">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3cb3b-141">Skonfiguruj prywatną komunikację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="3cb3b-142">Zanim przejdziesz do następnych kroków, upewnij się, czy masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="3cb3b-143">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3cb3b-144">Podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3cb3b-145">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3cb3b-146">Podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3cb3b-147">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3cb3b-148">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3cb3b-149">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-149">AS number for peering.</span></span> <span data-ttu-id="3cb3b-150">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="3cb3b-151">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="3cb3b-152">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="3cb3b-153">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="3cb3b-154">Skorzystaj z następującego przykładu, aby skonfigurować prywatnej komunikacji równorzędnej platformy Azure dla obwodu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="3cb3b-155">Jeśli chcesz użyć skrótu MD5, skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3cb3b-156">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="3cb3b-157">Aby wyświetlić szczegóły dotyczące prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-157">To view Azure private peering details</span></span>

<span data-ttu-id="3cb3b-158">Szczegóły konfiguracji można uzyskać za pomocą w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="3cb3b-159">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-159">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="3cb3b-160">Aby zaktualizować konfigurację prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="3cb3b-161">Można aktualizować dowolną część konfiguracji, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="3cb3b-162">W tym przykładzie identyfikator sieci VLAN obwodu jest aktualizowana od 100 do 500.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="3cb3b-163">Aby usunąć prywatną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-163">To delete Azure private peering</span></span>

<span data-ttu-id="3cb3b-164">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="3cb3b-165">Należy się upewnić, że wszystkie sieci wirtualne są odłączone od obwodu ExpressRoute przed uruchomieniem w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="3cb3b-166">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-166">Azure public peering</span></span>

<span data-ttu-id="3cb3b-167">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji platformy Azure publicznej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="3cb3b-168">Aby utworzyć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-168">To create Azure public peering</span></span>

1. <span data-ttu-id="3cb3b-169">Zainstaluj najnowszą wersję interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3cb3b-170">Należy użyć najnowszej wersji programu Azure interfejsu wiersza polecenia (CLI). * przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3cb3b-171">Wybierz subskrypcję, dla której chcesz utworzyć obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3cb3b-172">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="3cb3b-173">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](howto-circuit-cli.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3cb3b-174">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, mogą żądać, czy dostawca połączenia umożliwia prywatnej komunikacji równorzędnej platformy Azure dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="3cb3b-175">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3cb3b-176">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="3cb3b-177">Sprawdź obwodu ExpressRoute, aby upewnić się, jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="3cb3b-178">Skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3cb3b-179">Odpowiedź jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-179">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3cb3b-180">Skonfiguruj publiczną konfigurację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="3cb3b-181">Upewnij się, że masz następujące informacje przed przejściem dalej.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="3cb3b-182">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3cb3b-183">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3cb3b-184">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3cb3b-185">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3cb3b-186">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3cb3b-187">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3cb3b-188">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-188">AS number for peering.</span></span> <span data-ttu-id="3cb3b-189">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3cb3b-190">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="3cb3b-191">Uruchom poniższy przykład, aby skonfigurować publicznej komunikacji równorzędnej platformy Azure dla obwodu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="3cb3b-192">Jeśli chcesz użyć skrótu MD5, skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3cb3b-193">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="3cb3b-194">Aby wyświetlić szczegóły dotyczące publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-194">To view Azure public peering details</span></span>

<span data-ttu-id="3cb3b-195">Można pobrać szczegółów konfiguracji, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="3cb3b-196">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-196">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="3cb3b-197">Aby zaktualizować konfigurację publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="3cb3b-198">Można aktualizować dowolną część konfiguracji, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="3cb3b-199">W tym przykładzie identyfikator sieci VLAN obwodu jest aktualizowana od 200 do 600.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="3cb3b-200">Aby usunąć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="3cb3b-200">To delete Azure public peering</span></span>

<span data-ttu-id="3cb3b-201">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="3cb3b-202">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-202">Microsoft peering</span></span>

<span data-ttu-id="3cb3b-203">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cb3b-204">Z obwody usługi ExpressRoute, które zostały skonfigurowane przed 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft ma wszystkie prefiksy usługi anonsowane przez firmę Microsoft, zaglądanie, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="3cb3b-205">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane do momentu filtr tras jest dołączony do obwodu.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="3cb3b-206">Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="3cb3b-207">Aby utworzyć komunikację równorzędną Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="3cb3b-208">Zainstaluj najnowszą wersję interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3cb3b-209">Korzystanie z najnowszej wersji programu Azure interfejsu wiersza polecenia (CLI). * przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3cb3b-210">Wybierz subskrypcję, dla której chcesz utworzyć obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3cb3b-211">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3cb3b-212">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](howto-circuit-cli.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3cb3b-213">Jeśli dostawca połączenia oferuje zarządzane usługi warstwy 3, możesz poprosić go o włączenie prywatnej komunikacji równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3cb3b-214">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3cb3b-215">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="3cb3b-216">Sprawdź obwodu ExpressRoute, aby upewnić się, jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3cb3b-217">Skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3cb3b-218">Odpowiedź jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-218">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="3cb3b-219">Skonfiguruj komunikację równorzędną Microsoft dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="3cb3b-220">Zanim przejdziesz dalej, upewnij się, że masz poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="3cb3b-221">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3cb3b-222">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3cb3b-223">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3cb3b-224">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3cb3b-225">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3cb3b-226">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3cb3b-227">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-227">AS number for peering.</span></span> <span data-ttu-id="3cb3b-228">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3cb3b-229">Anonsowane prefiksy: musisz podać listę wszystkich prefiksów, które planujesz anonsować za pośrednictwem sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="3cb3b-230">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="3cb3b-231">Jeśli planujesz wysłać zestaw prefiksy, możesz wysłać rozdzielana przecinkami lista.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="3cb3b-232">Prefiksy te muszą być zarejestrowane na Ciebie w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="3cb3b-233">**Opcjonalne -** klienta ASN: jeśli prefiksy reklamy, które nie zostały zarejestrowane do komunikacji równorzędnej jako numer, można określić numer AS, z którym są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="3cb3b-234">Nazwa rejestru routingu: możesz określić RIR/IRR, względem którego rejestrowany jest numer AS i prefiksy.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="3cb3b-235">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="3cb3b-236">Uruchom poniższy przykład, aby skonfigurować komunikacji równorzędnej dla obwodu firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="3cb3b-237">Aby pobrać szczegóły dotyczące komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-237">To get Microsoft peering details</span></span>

<span data-ttu-id="3cb3b-238">Szczegóły konfiguracji można uzyskać za pomocą w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="3cb3b-239">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-239">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="3cb3b-240">Aby zaktualizować konfigurację komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="3cb3b-241">Można aktualizować dowolną część konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3cb3b-241">You can update any part of the configuration.</span></span> <span data-ttu-id="3cb3b-242">Anonsowane prefiksy obwodu są aktualizowane z 123.1.0.0/24 do 124.1.0.0/24 w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="3cb3b-243">Aby usunąć komunikację równorzędną firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3cb3b-243">To delete Microsoft peering</span></span>

<span data-ttu-id="3cb3b-244">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3cb3b-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="3cb3b-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3cb3b-245">Next steps</span></span>

<span data-ttu-id="3cb3b-246">Następny krok: [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md) (Łączenie sieci wirtualnej z obwodem usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="3cb3b-247">Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="3cb3b-248">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="3cb3b-249">Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="3cb3b-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>