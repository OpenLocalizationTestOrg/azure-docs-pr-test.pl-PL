---
title: "Jak tooconfigure routingu dla obwodu usługi Azure ExpressRoute: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Ten artykuł ułatwia tworzenie i przydzielanie hello prywatne, publiczna i obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
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
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="88fa2-104">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="88fa2-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="88fa2-105">W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="88fa2-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="88fa2-106">Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="88fa2-107">Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="88fa2-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="88fa2-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="88fa2-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="88fa2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88fa2-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="88fa2-110">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88fa2-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="88fa2-111">Video - prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="88fa2-112">Video - publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="88fa2-113">Video - komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="88fa2-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="88fa2-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="88fa2-115">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="88fa2-115">Configuration prerequisites</span></span>

* <span data-ttu-id="88fa2-116">Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="88fa2-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="88fa2-117">Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88fa2-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="88fa2-118">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływu pracy](expressroute-workflows.md) strony przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="88fa2-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="88fa2-119">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="88fa2-120">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](howto-circuit-cli.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="88fa2-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="88fa2-121">Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie toobe toorun stanie hello poleceń w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="88fa2-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="88fa2-122">Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="88fa2-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="88fa2-123">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="88fa2-124">Można skonfigurować jedną, dwie lub wszystkich trzech komunikacji równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="88fa2-125">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="88fa2-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="88fa2-126">Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="88fa2-127">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="88fa2-127">Azure private peering</span></span>

<span data-ttu-id="88fa2-128">Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="88fa2-129">toocreate Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="88fa2-130">Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa2-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="88fa2-131">Należy użyć najnowszej wersji hello hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="88fa2-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="88fa2-132">Wybierz hello subskrypcję toocreate obwodu ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="88fa2-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="88fa2-133">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="88fa2-134">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="88fa2-135">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="88fa2-136">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="88fa2-137">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="88fa2-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="88fa2-138">Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="88fa2-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="88fa2-139">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="88fa2-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="88fa2-140">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-140">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="88fa2-141">Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="88fa2-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="88fa2-142">Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:</span><span class="sxs-lookup"><span data-stu-id="88fa2-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="88fa2-143">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="88fa2-144">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88fa2-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="88fa2-145">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="88fa2-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="88fa2-146">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88fa2-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="88fa2-147">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="88fa2-148">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="88fa2-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="88fa2-149">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-149">AS number for peering.</span></span> <span data-ttu-id="88fa2-150">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="88fa2-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="88fa2-151">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="88fa2-152">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="88fa2-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="88fa2-153">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="88fa2-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="88fa2-154">Użyj powitania po tooconfigure przykład prywatnej komunikacji równorzędnej dla obwodu usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="88fa2-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="88fa2-155">Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="88fa2-156">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="88fa2-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="88fa2-157">tooview Azure prywatnej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="88fa2-157">tooview Azure private peering details</span></span>

<span data-ttu-id="88fa2-158">Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="88fa2-159">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-159">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="88fa2-160">tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88fa2-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="88fa2-161">Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="88fa2-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="88fa2-162">W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.</span><span class="sxs-lookup"><span data-stu-id="88fa2-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="88fa2-163">toodelete Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-163">toodelete Azure private peering</span></span>

<span data-ttu-id="88fa2-164">Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="88fa2-165">Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu ExpressRoute przed uruchomieniem w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="88fa2-166">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="88fa2-166">Azure public peering</span></span>

<span data-ttu-id="88fa2-167">Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="88fa2-168">toocreate Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="88fa2-169">Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa2-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="88fa2-170">Należy użyć najnowszej wersji hello hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="88fa2-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="88fa2-171">Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="88fa2-172">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="88fa2-173">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="88fa2-174">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, mogą żądać, czy dostawca połączenia umożliwia prywatnej komunikacji równorzędnej platformy Azure dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="88fa2-175">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="88fa2-176">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="88fa2-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="88fa2-177">Sprawdź tooensure obwodu ExpressRoute hello jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="88fa2-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="88fa2-178">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="88fa2-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="88fa2-179">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-179">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="88fa2-180">Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="88fa2-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="88fa2-181">Upewnij się, że masz hello następujących informacji przed przejściem dalej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="88fa2-182">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="88fa2-183">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="88fa2-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="88fa2-184">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="88fa2-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="88fa2-185">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="88fa2-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="88fa2-186">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="88fa2-187">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="88fa2-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="88fa2-188">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-188">AS number for peering.</span></span> <span data-ttu-id="88fa2-189">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="88fa2-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="88fa2-190">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="88fa2-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="88fa2-191">Uruchom powitania po tooconfigure przykład publicznej komunikacji równorzędnej dla obwodu usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="88fa2-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="88fa2-192">Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="88fa2-193">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="88fa2-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="88fa2-194">tooview Azure publicznej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="88fa2-194">tooview Azure public peering details</span></span>

<span data-ttu-id="88fa2-195">Można pobrać szczegółów konfiguracji przy użyciu hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="88fa2-196">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-196">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="88fa2-197">tooupdate Azure publicznej konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="88fa2-198">Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="88fa2-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="88fa2-199">W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 200 too600.</span><span class="sxs-lookup"><span data-stu-id="88fa2-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="88fa2-200">toodelete Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="88fa2-200">toodelete Azure public peering</span></span>

<span data-ttu-id="88fa2-201">Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="88fa2-202">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-202">Microsoft peering</span></span>

<span data-ttu-id="88fa2-203">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88fa2-204">Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="88fa2-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="88fa2-205">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="88fa2-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="88fa2-206">Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="88fa2-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="88fa2-207">toocreate komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="88fa2-208">Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa2-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="88fa2-209">Użyj hello najnowszą wersję hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="88fa2-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="88fa2-210">Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="88fa2-211">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="88fa2-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="88fa2-212">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="88fa2-213">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="88fa2-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="88fa2-214">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="88fa2-215">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="88fa2-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="88fa2-216">Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="88fa2-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="88fa2-217">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="88fa2-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="88fa2-218">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-218">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="88fa2-219">Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="88fa2-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="88fa2-220">Upewnij się, że masz hello następujących informacji, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="88fa2-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="88fa2-221">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="88fa2-222">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="88fa2-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="88fa2-223">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="88fa2-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="88fa2-224">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="88fa2-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="88fa2-225">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="88fa2-226">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="88fa2-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="88fa2-227">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="88fa2-227">AS number for peering.</span></span> <span data-ttu-id="88fa2-228">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="88fa2-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="88fa2-229">Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="88fa2-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="88fa2-230">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="88fa2-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="88fa2-231">Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="88fa2-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="88fa2-232">Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="88fa2-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="88fa2-233">**Opcjonalne -** klienta ASN: w przypadku prefiksów reklamy, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer hello można określić jako numer toowhich są zarejestrowani.</span><span class="sxs-lookup"><span data-stu-id="88fa2-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="88fa2-234">Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="88fa2-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="88fa2-235">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="88fa2-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="88fa2-236">Uruchom powitania po komunikacji równorzędnej firmy Microsoft tooconfigure przykład dla obwodu:</span><span class="sxs-lookup"><span data-stu-id="88fa2-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="88fa2-237">Szczegóły komunikacji równorzędnej tooget firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="88fa2-238">Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="88fa2-239">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-239">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="88fa2-240">konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="88fa2-241">Można aktualizować dowolną część konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="88fa2-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="88fa2-242">Witaj anonsowany prefiksy obwodu hello są aktualizowane z too124.1.0.0/24 123.1.0.0/24 w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="88fa2-243">toodelete komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="88fa2-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="88fa2-244">Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88fa2-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="88fa2-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88fa2-245">Next steps</span></span>

<span data-ttu-id="88fa2-246">Następny krok [połączyć sieć wirtualną tooan obwodu ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="88fa2-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="88fa2-247">Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="88fa2-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="88fa2-248">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="88fa2-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="88fa2-249">Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="88fa2-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>