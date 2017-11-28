---
title: "Połącz tooAzure klasycznych sieci wirtualnych Menedżera zasobów sieci wirtualnych: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate połączenia sieci VPN między klasycznych sieci wirtualnych i sieci wirtualnych Menedżera zasobów przy użyciu bramy sieci VPN i programu PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="ffa13-103">Łączenie sieci wirtualnych z różnych modeli wdrażania za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa13-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="ffa13-104">W tym artykule opisano, jak tooconnect klasycznych sieci wirtualnych tooResource tooallow Menedżera sieci wirtualnych hello zasobów znajdujących się w hello oddzielne wdrażania modeli toocommunicate ze sobą.</span><span class="sxs-lookup"><span data-stu-id="ffa13-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="ffa13-105">Hello opisanych w tym artykule przy użyciu programu PowerShell, ale można również utworzyć tę konfigurację za pomocą hello portalu Azure, wybierając hello artykułu z tej listy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffa13-106">Portal</span><span class="sxs-lookup"><span data-stu-id="ffa13-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="ffa13-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa13-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="ffa13-108">Łączenie klasycznego tooa sieci wirtualnej Menedżera zasobów w sieci wirtualnej jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji.</span><span class="sxs-lookup"><span data-stu-id="ffa13-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="ffa13-109">Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu.</span><span class="sxs-lookup"><span data-stu-id="ffa13-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="ffa13-110">Można utworzyć połączenia między sieciami wirtualnymi, które są w różnych subskrypcji i w różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="ffa13-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="ffa13-111">Można też połączyć sieci wirtualnych, która jeszcze połączenia lokalnego tooon sieci, tak długo, jak jest hello bramy, które zostały skonfigurowane z dynamicznego lub oparte na trasach.</span><span class="sxs-lookup"><span data-stu-id="ffa13-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="ffa13-112">Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ffa13-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="ffa13-113">Jeśli hello Twojej sieci wirtualnych tego samego regionu, można wziąć pod uwagę tooinstead, łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="ffa13-114">W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ffa13-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="ffa13-115">Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffa13-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="ffa13-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ffa13-116">Before beginning</span></span>

<span data-ttu-id="ffa13-117">Witaj poniższe kroki przeprowadzi użytkownika przez proces tooconfigure niezbędne ustawienia hello bramy dynamiczne lub oparte na trasach dla każdej sieci wirtualnej i Utwórz połączenie sieci VPN między bramami hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="ffa13-118">Ta konfiguracja nie obsługuje bramy statyczne lub oparte na zasadach.</span><span class="sxs-lookup"><span data-stu-id="ffa13-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ffa13-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ffa13-119">Prerequisites</span></span>

* <span data-ttu-id="ffa13-120">Obie sieci wirtualne zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="ffa13-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="ffa13-121">Hello zakresy adresów dla hello sieci wirtualnych nie pokrywają się ze sobą, ani nie nakładają się ze wszystkimi hello zakresów dla innych połączeń, które hello bramy może być połączone.</span><span class="sxs-lookup"><span data-stu-id="ffa13-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="ffa13-122">Zainstalowano hello najnowszych poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa13-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="ffa13-123">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ffa13-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="ffa13-124">Upewnij się, że należy zainstalować zarówno hello usługi zarządzania (ko), jak i hello poleceń cmdlet Menedżera zasobów (RM).</span><span class="sxs-lookup"><span data-stu-id="ffa13-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="ffa13-125"><a name="exampleref"></a>Przykładowe ustawienia</span><span class="sxs-lookup"><span data-stu-id="ffa13-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="ffa13-126">Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ffa13-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="ffa13-127">**Klasycznych ustawień sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="ffa13-127">**Classic VNet settings**</span></span>

<span data-ttu-id="ffa13-128">Nazwa sieci wirtualnej = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="ffa13-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="ffa13-129">Lokalizacja = zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="ffa13-129">Location = West US</span></span> <br>
<span data-ttu-id="ffa13-130">Przestrzeniami adresów sieci wirtualnej = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ffa13-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="ffa13-131">Podsieć 1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="ffa13-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="ffa13-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="ffa13-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="ffa13-133">Nazwa sieci lokalnej = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="ffa13-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="ffa13-134">Elementu GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="ffa13-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="ffa13-135">**Ustawienia Menedżera zasobów w sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="ffa13-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="ffa13-136">Nazwa sieci wirtualnej = RMVNet</span><span class="sxs-lookup"><span data-stu-id="ffa13-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="ffa13-137">Grupa zasobów = RG1</span><span class="sxs-lookup"><span data-stu-id="ffa13-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="ffa13-138">Przestrzeni adresów IP sieci wirtualnej = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ffa13-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="ffa13-139">Podsieć 1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="ffa13-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="ffa13-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="ffa13-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="ffa13-141">Lokalizacja = wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="ffa13-141">Location = East US</span></span> <br>
<span data-ttu-id="ffa13-142">Nazwa publicznego adresu IP bramy = gwpip</span><span class="sxs-lookup"><span data-stu-id="ffa13-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="ffa13-143">Brama sieci lokalnej = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="ffa13-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="ffa13-144">Nazwa bramy sieci wirtualnej = RMGateway</span><span class="sxs-lookup"><span data-stu-id="ffa13-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="ffa13-145">Konfiguracja adresów IP bramy = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="ffa13-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="ffa13-146"><a name="createsmgw"></a>Sekcja 1 — Konfigurowanie hello klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ffa13-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="ffa13-147">Część 1 - pobierania pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="ffa13-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="ffa13-148">Zaloguj się za tooyour konto platformy Azure w konsoli programu PowerShell hello z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="ffa13-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="ffa13-149">Witaj następujące polecenie cmdlet monituje o hello poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa13-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="ffa13-150">Po zalogowaniu pobraniu ustawienia konta, aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa13-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="ffa13-151">Użyj hello toocomplete poleceń cmdlet programu PowerShell SM ta część hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ffa13-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="ffa13-152">Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="ffa13-153">Możesz zmienić lokalizację hello hello pliku tooexport tooa różnych lokalizacji, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="ffa13-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="ffa13-154">Witaj Otwórz plik XML został pobrany tooedit go.</span><span class="sxs-lookup"><span data-stu-id="ffa13-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="ffa13-155">Na przykład pliku konfiguracji sieci hello Zobacz hello [schemat konfiguracji sieci](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffa13-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="ffa13-156">Część 2 - Sprawdź hello podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="ffa13-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="ffa13-157">W hello **VirtualNetworkSites** elementu, Dodaj tooyour podsieci bramy sieci wirtualnej, jeśli nie została jeszcze utworzona.</span><span class="sxs-lookup"><span data-stu-id="ffa13-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="ffa13-158">Podczas pracy z pliku konfiguracji sieci hello, hello podsieć bramy musi mieć nazwę "GatewaySubnet" lub Azure nie może rozpoznać i używać go jako podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="ffa13-159">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="ffa13-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="ffa13-160">Część 3 — Dodawanie hello lokacji sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="ffa13-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="ffa13-161">Hello lokację sieci lokalnej, które można dodać reprezentuje hello ma tooconnect toowhich RM sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="ffa13-162">Dodaj **LocalNetworkSites** pliku toohello elementu, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ffa13-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="ffa13-163">W tym momencie w konfiguracji hello hello VPNGatewayAddress może być dowolnym prawidłowego publicznego adresu IP, ponieważ możemy jeszcze nie utworzono bramę hello hello Menedżera zasobów w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="ffa13-164">Po utworzymy hello bramy możemy zastąpić ten adres IP — symbol zastępczy hello poprawne publiczny adres IP przypisany toohello RM bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="ffa13-165">Część 4 - hello skojarzenia sieci wirtualnej z lokacją sieci lokalnej hello</span><span class="sxs-lookup"><span data-stu-id="ffa13-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="ffa13-166">W tej sekcji określono hello lokacji sieci lokalnej, które mają tooconnect hello sieci wirtualnej do.</span><span class="sxs-lookup"><span data-stu-id="ffa13-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="ffa13-167">W takim przypadku jest hello odwołanie do wcześniej sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="ffa13-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="ffa13-168">Upewnij się, że nazwy hello zgodne.</span><span class="sxs-lookup"><span data-stu-id="ffa13-168">Make sure hello names match.</span></span> <span data-ttu-id="ffa13-169">Ten krok nie powoduje utworzenia bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-169">This step does not create a gateway.</span></span> <span data-ttu-id="ffa13-170">Określa hello sieci lokalnej hello bramy połączy się.</span><span class="sxs-lookup"><span data-stu-id="ffa13-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="ffa13-171">Część 5 - Zapisz plik hello oraz przekazywania</span><span class="sxs-lookup"><span data-stu-id="ffa13-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="ffa13-172">Zapisz plik hello, a następnie zaimportuj go tooAzure, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="ffa13-173">Upewnij się, że w przypadku zmiany ścieżki pliku hello jako wymaganych w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="ffa13-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="ffa13-174">Widoczny będzie podobny wynik pokazujący, że importowanie hello zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ffa13-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="ffa13-175">Część 6 - Tworzenie hello bramy</span><span class="sxs-lookup"><span data-stu-id="ffa13-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="ffa13-176">Przed uruchomieniem w tym przykładzie należy odwoływać się toohello toosee oczekuje pobranego hello dokładnej nazwy tego Azure pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="ffa13-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="ffa13-177">plik konfiguracji sieci Hello zawiera wartości hello klasyczne sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ffa13-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="ffa13-178">Czasami nazwy hello klasycznego sieci wirtualne są zmieniane w pliku konfiguracji sieci hello podczas tworzenia klasycznych ustawień sieci wirtualnej w hello portalu Azure powodu toohello różnice w hello modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ffa13-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="ffa13-179">Na przykład jeśli użyto hello Azure toocreate portalu klasycznego sieć wirtualną o nazwie "Klasycznej sieci wirtualnej" i utworzony w grupie zasobów o nazwie "ClassicRG" hello nazwę, która jest zawarta w pliku konfiguracji sieci hello jest przekonwertowanego too'Group ClassicRG klasycznej sieci wirtualnej ".</span><span class="sxs-lookup"><span data-stu-id="ffa13-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="ffa13-180">Podczas określania nazwy hello sieci wirtualnej, która zawiera spacje, użyj hello wartości w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="ffa13-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="ffa13-181">Użyj powitania po toocreate przykładzie brama routingu dynamicznego:</span><span class="sxs-lookup"><span data-stu-id="ffa13-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="ffa13-182">Istnieje możliwość sprawdzenia stanu hello hello bramy przy użyciu hello **Get-AzureVNetGateway** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ffa13-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="ffa13-183"><a name="creatermgw"></a>Sekcja 2: Konfigurowanie hello bramy sieci wirtualnej RM</span><span class="sxs-lookup"><span data-stu-id="ffa13-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="ffa13-184">toocreate Brama sieci VPN dla hello RM sieci wirtualnej, postępuj zgodnie z instrukcjami hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="ffa13-185">Po pobraniu hello publicznego adresu IP dla bramy wirtualnej klasycznego hello hello kroki, dopóki nie należy uruchamiać.</span><span class="sxs-lookup"><span data-stu-id="ffa13-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="ffa13-186">Zaloguj się za tooyour konto platformy Azure w konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="ffa13-187">Witaj następujące polecenie cmdlet monituje o hello poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa13-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="ffa13-188">Po zalogowaniu ustawienia konta są pobierane, tak aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa13-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="ffa13-189">Pobierz listę subskrypcji Azure, jeśli masz więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="ffa13-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="ffa13-190">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="ffa13-191">Utwórz bramę sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-191">Create a local network gateway.</span></span> <span data-ttu-id="ffa13-192">W sieci wirtualnej bramy sieci lokalnej hello zwykle oznacza tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="ffa13-193">W takim przypadku bramy sieci lokalnej hello odwołuje się tooyour klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="ffa13-194">Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a także określić prefiks przestrzeni adresów hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="ffa13-195">Platforma Azure korzysta prefiks adresu IP hello Określ tooidentify tooyour toosend których ruch lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="ffa13-196">Jeśli później, należy tutaj informacje hello tooadjust przed utworzeniem bramy sieci można zmodyfikować wartości hello i przykładowe hello Uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="ffa13-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="ffa13-197">**-Nazwa** jest nazwą hello ma bramy sieci lokalnej toohello toorefer tooassign.</span><span class="sxs-lookup"><span data-stu-id="ffa13-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="ffa13-198">
   **-AddressPrefix** jest hello przestrzeni adresowej dla sieci wirtualnej klasycznego.</span><span class="sxs-lookup"><span data-stu-id="ffa13-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="ffa13-199">
**-GatewayIpAddress** jest hello publiczny adres IP bramy hello klasycznego VNet.</span><span class="sxs-lookup"><span data-stu-id="ffa13-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="ffa13-200">Upewnij się, że toochange hello następujące przykładowe tooreflect hello poprawny adres IP.</span><span class="sxs-lookup"><span data-stu-id="ffa13-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="ffa13-201">Żądaj publicznego adresu IP adres toobe toohello przydzielone bramę sieci wirtualnej dla hello Menedżera zasobów w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="ffa13-202">Nie można określić hello adresu IP, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="ffa13-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="ffa13-203">adres IP Hello jest dynamicznie przydzielane toohello bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="ffa13-204">Nie oznacza to jednak zmiany adresu IP hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="ffa13-205">tylko wtedy Hello zmiany adresu IP bramy sieci wirtualnej hello jest po hello bramy jest usunięty i utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="ffa13-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="ffa13-206">Nie zmienia ono całej zmiany rozmiaru, resetowanie lub innych wewnętrzny konserwacji/uaktualnień, hello bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="ffa13-207">W tym kroku będziemy również ustawić zmiennej używanej w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="ffa13-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="ffa13-208">Sprawdź, czy sieci wirtualnej ma podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="ffa13-209">Jeśli istnieje podsieć bramy, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="ffa13-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="ffa13-210">Upewnij się, że nosi nazwę podsieci bramy hello *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="ffa13-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="ffa13-211">Pobieranie podsieci hello używanym na potrzeby hello bramy, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="ffa13-212">W tym kroku będziemy również ustawić zmiennej toobe, używany w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="ffa13-213">**-Nazwa** hello nazwa sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="ffa13-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="ffa13-214">
   **-ResourceGroupName** jest hello grupa zasobów tego hello sieci wirtualnej jest skojarzony.</span><span class="sxs-lookup"><span data-stu-id="ffa13-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="ffa13-215">podsieć bramy Hello musi już istnieć dla tej sieci wirtualnej i musi mieć nazwę *GatewaySubnet* toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="ffa13-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="ffa13-216">Tworzenie konfiguracji adresów IP bramy hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="ffa13-217">Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ffa13-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="ffa13-218">Użyj następujących hello przykładowe toocreate konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="ffa13-219">W tym kroku hello **- SubnetId** i **- PublicIpAddressId** parametry muszą być przekazywane właściwość identyfikatora hello hello podsieci i obiekty adresu IP, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="ffa13-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="ffa13-220">Nie można użyć prostego ciągu.</span><span class="sxs-lookup"><span data-stu-id="ffa13-220">You can't use a simple string.</span></span> <span data-ttu-id="ffa13-221">Te zmienne są ustawiane w toorequest krok hello publicznego adresu IP i hello krok tooretrieve hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="ffa13-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="ffa13-222">Tworzenie bramy sieci wirtualnej hello Menedżera zasobów, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="ffa13-223">Witaj `-VpnType` musi być *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="ffa13-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="ffa13-224">Może upłynąć 45 minut lub więcej hello toocreate bramy.</span><span class="sxs-lookup"><span data-stu-id="ffa13-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="ffa13-225">Po utworzeniu bramy sieci VPN hello, skopiuj hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ffa13-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="ffa13-226">Można użyć podczas konfigurowania ustawień sieci lokalnej hello klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="ffa13-227">Można użyć następującego polecenia cmdlet tooretrieve hello publicznego adresu IP hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="ffa13-228">Witaj publiczny adres IP ma na liście hello zwracany jako *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="ffa13-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="ffa13-229">Sekcja 3: Modyfikowanie hello klasycznych ustawień lokalnej lokacji sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ffa13-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="ffa13-230">W tej sekcji możesz pracować z hello klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffa13-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="ffa13-231">Można zastąpić adres IP — symbol zastępczy hello używane podczas określania ustawień lokacji lokalnej hello, które będą używane tooconnect toohello bramy sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="ffa13-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="ffa13-232">Eksportowanie pliku konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="ffa13-233">Za pomocą edytora tekstu, zmodyfikuj wartość powitania dla VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="ffa13-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="ffa13-234">Zamień adres IP — symbol zastępczy hello hello publiczny adres IP bramy usługi Resource Manager hello, a następnie zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="ffa13-235">Importuj hello zmodyfikować tooAzure pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="ffa13-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="ffa13-236"><a name="connect"></a>Sekcja 4: Tworzenie połączenia między bramami hello</span><span class="sxs-lookup"><span data-stu-id="ffa13-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="ffa13-237">Tworzenie połączenia między bramami hello wymaga środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa13-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="ffa13-238">Konieczne może tooadd Twojego konta Azure toouse hello klasycznej wersji hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa13-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="ffa13-239">tak, użyj toodo **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="ffa13-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="ffa13-240">W konsoli programu PowerShell hello należy ustawić klucz udostępniony.</span><span class="sxs-lookup"><span data-stu-id="ffa13-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="ffa13-241">Przed uruchomieniem poleceń cmdlet hello, można znaleźć toohello toosee oczekuje pobranego hello dokładnej nazwy tego Azure pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="ffa13-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="ffa13-242">Podczas określania nazwy hello sieci wirtualnej, która zawiera spacje, użyj pojedynczy znaki cudzysłowu otaczające wartość hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="ffa13-243">W poniższym przykładzie **- VNetName** jest nazwą hello hello klasycznej sieci wirtualnej i **- LocalNetworkSiteName** jest nazwą hello określony dla lokacji sieci lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="ffa13-244">Witaj **- SharedKey** to Generowanie i określ wartość.</span><span class="sxs-lookup"><span data-stu-id="ffa13-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="ffa13-245">Przykład Witaj użyliśmy "abc123", ale można wygenerować i korzystać z bardziej złożonych.</span><span class="sxs-lookup"><span data-stu-id="ffa13-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="ffa13-246">Witaj ważne, czy element jest daną hello określone w tym miejscu musi być powitalne samą wartość, że zostanie w następnym kroku hello podczas tworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="ffa13-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="ffa13-247">Witaj zwracany powinien być wyświetlony **stanu: pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="ffa13-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="ffa13-248">Utwórz połączenie sieci VPN hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ffa13-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="ffa13-249">Ustaw zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="ffa13-250">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="ffa13-250">Create hello connection.</span></span> <span data-ttu-id="ffa13-251">Zwróć uwagę, że hello **- ConnectionType** jest IPsec, nie Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="ffa13-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="ffa13-252">Sekcja 5: Sprawdź połączenia</span><span class="sxs-lookup"><span data-stu-id="ffa13-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="ffa13-253">tooverify hello połączenia z klasycznym tooyour sieci wirtualnej Menedżera zasobów w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ffa13-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffa13-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa13-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="ffa13-255">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ffa13-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="ffa13-256">tooverify hello połączenia z Twojej sieci wirtualnej Resource Manager tooyour klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ffa13-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffa13-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa13-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="ffa13-258">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ffa13-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="ffa13-259"><a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="ffa13-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

