---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Menedżer zasobów: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="368c5-104">Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="368c5-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="368c5-105">W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="368c5-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="368c5-106">Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="368c5-107">Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="368c5-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="368c5-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="368c5-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="368c5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="368c5-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="368c5-110">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="368c5-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="368c5-111">Video - prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="368c5-112">Video - publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="368c5-113">Video - komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="368c5-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="368c5-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="368c5-115">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="368c5-115">Configuration prerequisites</span></span>

* <span data-ttu-id="368c5-116">Konieczne będzie hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="368c5-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="368c5-117">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="368c5-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="368c5-118">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="368c5-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="368c5-119">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="368c5-120">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="368c5-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="368c5-121">Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie poleceń cmdlet hello stanie toorun toobe w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="368c5-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="368c5-122">Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="368c5-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="368c5-123">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="368c5-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="368c5-124">Mamy obecnie nie anonsuje skonfigurowane przez dostawców usług za pośrednictwem portalu zarządzania usługami hello komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="368c5-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="368c5-125">Pracujemy nad tym, by wkrótce włączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="368c5-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="368c5-126">Skontaktuj się z dostawcą usług przed rozpoczęciem konfigurowania komunikacji równorzędnych protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="368c5-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="368c5-127">Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="368c5-128">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="368c5-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="368c5-129">Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.</span><span class="sxs-lookup"><span data-stu-id="368c5-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="368c5-130">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="368c5-130">Azure private peering</span></span>

<span data-ttu-id="368c5-131">Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="368c5-132">toocreate Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="368c5-133">Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="368c5-134">Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="368c5-135">Należy toorun programu PowerShell jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="368c5-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="368c5-136">Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="368c5-137">Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="368c5-138">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="368c5-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="368c5-139">Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="368c5-140">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="368c5-141">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="368c5-142">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="368c5-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="368c5-143">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="368c5-144">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="368c5-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="368c5-145">Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="368c5-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="368c5-146">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="368c5-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="368c5-147">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-147">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="368c5-148">Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="368c5-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="368c5-149">Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:</span><span class="sxs-lookup"><span data-stu-id="368c5-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="368c5-150">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="368c5-151">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="368c5-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="368c5-152">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="368c5-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="368c5-153">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="368c5-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="368c5-154">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="368c5-155">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="368c5-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="368c5-156">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-156">AS number for peering.</span></span> <span data-ttu-id="368c5-157">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="368c5-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="368c5-158">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="368c5-159">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="368c5-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="368c5-160">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="368c5-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="368c5-161">Użyj powitania po tooconfigure przykład prywatnej komunikacji równorzędnej dla obwodu usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="368c5-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="368c5-162">Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="368c5-163">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="368c5-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="368c5-164">tooview Azure prywatnej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="368c5-164">tooview Azure private peering details</span></span>

<span data-ttu-id="368c5-165">Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="368c5-166">tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="368c5-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="368c5-167">Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="368c5-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="368c5-168">W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.</span><span class="sxs-lookup"><span data-stu-id="368c5-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="368c5-169">toodelete Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-169">toodelete Azure private peering</span></span>

<span data-ttu-id="368c5-170">Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="368c5-171">Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu ExpressRoute przed uruchomieniem w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="368c5-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="368c5-172">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="368c5-172">Azure public peering</span></span>

<span data-ttu-id="368c5-173">Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="368c5-174">toocreate Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="368c5-175">Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="368c5-176">Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="368c5-177">Należy toorun programu PowerShell jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="368c5-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="368c5-178">Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="368c5-179">Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="368c5-180">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="368c5-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="368c5-181">Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="368c5-182">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="368c5-183">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="368c5-184">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="368c5-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="368c5-185">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="368c5-186">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="368c5-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="368c5-187">Sprawdź tooensure obwodu ExpressRoute hello jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="368c5-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="368c5-188">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="368c5-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="368c5-189">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-189">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="368c5-190">Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="368c5-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="368c5-191">Upewnij się, że masz hello następujących informacji przed przejściem dalej.</span><span class="sxs-lookup"><span data-stu-id="368c5-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="368c5-192">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="368c5-193">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="368c5-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="368c5-194">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="368c5-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="368c5-195">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="368c5-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="368c5-196">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="368c5-197">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="368c5-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="368c5-198">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-198">AS number for peering.</span></span> <span data-ttu-id="368c5-199">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="368c5-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="368c5-200">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="368c5-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="368c5-201">Uruchom powitania po tooconfigure przykład Azure publicznej komunikacji równorzędnej dla obwodu</span><span class="sxs-lookup"><span data-stu-id="368c5-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="368c5-202">Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="368c5-203">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="368c5-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="368c5-204">tooview Azure publicznej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="368c5-204">tooview Azure public peering details</span></span>

<span data-ttu-id="368c5-205">Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="368c5-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="368c5-206">tooupdate Azure publicznej konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="368c5-207">Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="368c5-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="368c5-208">W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 200 too600.</span><span class="sxs-lookup"><span data-stu-id="368c5-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="368c5-209">toodelete Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="368c5-209">toodelete Azure public peering</span></span>

<span data-ttu-id="368c5-210">Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="368c5-211">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-211">Microsoft peering</span></span>

<span data-ttu-id="368c5-212">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="368c5-213">Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="368c5-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="368c5-214">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="368c5-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="368c5-215">Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="368c5-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="368c5-216">toocreate komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="368c5-217">Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="368c5-218">Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="368c5-219">Należy toorun programu PowerShell jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="368c5-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="368c5-220">Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="368c5-221">Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="368c5-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="368c5-222">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="368c5-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="368c5-223">Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="368c5-224">Utwórz obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="368c5-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="368c5-225">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="368c5-226">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="368c5-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="368c5-227">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="368c5-228">Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="368c5-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="368c5-229">Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona.</span><span class="sxs-lookup"><span data-stu-id="368c5-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="368c5-230">Poniższy przykład hello użycia:</span><span class="sxs-lookup"><span data-stu-id="368c5-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="368c5-231">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-231">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="368c5-232">Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="368c5-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="368c5-233">Upewnij się, że masz hello następujących informacji, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="368c5-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="368c5-234">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="368c5-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="368c5-235">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="368c5-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="368c5-236">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="368c5-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="368c5-237">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="368c5-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="368c5-238">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="368c5-239">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="368c5-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="368c5-240">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="368c5-240">AS number for peering.</span></span> <span data-ttu-id="368c5-241">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="368c5-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="368c5-242">Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="368c5-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="368c5-243">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="368c5-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="368c5-244">Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="368c5-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="368c5-245">Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="368c5-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="368c5-246">**Opcjonalne -** klienta ASN: w przypadku prefiksów reklamy, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer hello można określić jako numer toowhich są zarejestrowani.</span><span class="sxs-lookup"><span data-stu-id="368c5-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="368c5-247">Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="368c5-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="368c5-248">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="368c5-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="368c5-249">Użyj powitania po komunikacji równorzędnej firmy Microsoft tooconfigure przykład dla obwodu:</span><span class="sxs-lookup"><span data-stu-id="368c5-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="368c5-250">Szczegóły komunikacji równorzędnej tooget firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="368c5-251">Można pobrać szczegółów konfiguracji przy użyciu hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="368c5-252">konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="368c5-253">Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="368c5-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="368c5-254">toodelete komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="368c5-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="368c5-255">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="368c5-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="368c5-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="368c5-256">Next steps</span></span>

<span data-ttu-id="368c5-257">Następny krok [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="368c5-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="368c5-258">Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="368c5-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="368c5-259">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="368c5-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="368c5-260">Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="368c5-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
