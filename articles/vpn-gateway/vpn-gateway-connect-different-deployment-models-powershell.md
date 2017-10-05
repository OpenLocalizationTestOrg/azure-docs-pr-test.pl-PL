---
title: "Połącz klasycznych sieci wirtualnych do sieci wirtualnych Menedżera zasobów Azure: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć połączenie sieci VPN między klasycznych sieci wirtualnych i sieci wirtualnych Menedżera zasobów przy użyciu bramy sieci VPN i programu PowerShell"
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
ms.openlocfilehash: 842a32e5304977af92706cdda464286983122247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="018bf-103">Łączenie sieci wirtualnych z różnych modeli wdrażania za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="018bf-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="018bf-104">W tym artykule przedstawiono sposób nawiązywania klasyczne sieci wirtualne sieci wirtualnych Menedżera zasobów umożliwia zasobów znajdujących się w modelach wdrażania oddzielne do komunikowania się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="018bf-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="018bf-105">Kroki opisane w tym artykule przy użyciu programu PowerShell, ale można również utworzyć w tej konfiguracji przy użyciu portalu Azure, wybierając artykułu z tej listy.</span><span class="sxs-lookup"><span data-stu-id="018bf-105">The steps in this article use PowerShell, but you can also create this configuration using the Azure portal by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="018bf-106">Portal</span><span class="sxs-lookup"><span data-stu-id="018bf-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="018bf-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="018bf-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="018bf-108">Łączenie klasycznej sieci wirtualnej z Menedżera zasobów sieci wirtualnej jest podobny do łączenia sieci wirtualnej do lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="018bf-109">Oba typy połączeń wykorzystują bramę sieci VPN, aby zapewnić bezpieczny tunel z użyciem protokołu IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="018bf-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="018bf-110">Można utworzyć połączenia między sieciami wirtualnymi, które są w różnych subskrypcji i w różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="018bf-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="018bf-111">Można również połączyć sieci wirtualnych, które mają już połączenia z sieciami lokalnymi tak długo, jak jest bramy, które zostały skonfigurowane z dynamicznego lub oparte na trasach.</span><span class="sxs-lookup"><span data-stu-id="018bf-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="018bf-112">Więcej informacji na temat połączeń między sieciami wirtualnymi znajduje się w sekcji [Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi](#faq) na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="018bf-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="018bf-113">W przypadku Twojej sieci wirtualnych w tym samym regionie, możesz zamiast tego należy rozważyć połączenie ich za pomocą sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="018bf-114">W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="018bf-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="018bf-115">Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="018bf-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="018bf-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="018bf-116">Before beginning</span></span>

<span data-ttu-id="018bf-117">W poniższych krokach objaśniono za pomocą ustawienia wymagane do skonfigurowania bramy dynamiczne lub oparte na trasach dla każdej sieci wirtualnej i Utwórz połączenie sieci VPN między bramami.</span><span class="sxs-lookup"><span data-stu-id="018bf-117">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="018bf-118">Ta konfiguracja nie obsługuje bramy statyczne lub oparte na zasadach.</span><span class="sxs-lookup"><span data-stu-id="018bf-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="018bf-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="018bf-119">Prerequisites</span></span>

* <span data-ttu-id="018bf-120">Obie sieci wirtualne zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="018bf-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="018bf-121">Zakresy adresów dla sieci wirtualne nie pokrywają się ze sobą lub pokrywają się z jednym z zakresów dla innych połączeń, które może być połączone bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-121">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="018bf-122">Zainstalowano najnowsze poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-122">You have installed the latest PowerShell cmdlets.</span></span> <span data-ttu-id="018bf-123">Zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="018bf-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="018bf-124">Upewnij się, że zostaną zainstalowane zarówno usługi zarządzania (ko), jak i poleceń cmdlet Menedżera zasobów (RM).</span><span class="sxs-lookup"><span data-stu-id="018bf-124">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="018bf-125"><a name="exampleref"></a>Przykładowe ustawienia</span><span class="sxs-lookup"><span data-stu-id="018bf-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="018bf-126">Tych wartości możesz użyć do tworzenia środowiska testowego lub odwoływać się do nich, aby lepiej zrozumieć przykłady w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="018bf-126">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="018bf-127">**Klasycznych ustawień sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="018bf-127">**Classic VNet settings**</span></span>

<span data-ttu-id="018bf-128">Nazwa sieci wirtualnej = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="018bf-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="018bf-129">Lokalizacja = zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="018bf-129">Location = West US</span></span> <br>
<span data-ttu-id="018bf-130">Przestrzeniami adresów sieci wirtualnej = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="018bf-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="018bf-131">Podsieć 1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="018bf-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="018bf-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="018bf-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="018bf-133">Nazwa sieci lokalnej = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="018bf-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="018bf-134">Elementu GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="018bf-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="018bf-135">**Ustawienia Menedżera zasobów w sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="018bf-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="018bf-136">Nazwa sieci wirtualnej = RMVNet</span><span class="sxs-lookup"><span data-stu-id="018bf-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="018bf-137">Grupa zasobów = RG1</span><span class="sxs-lookup"><span data-stu-id="018bf-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="018bf-138">Przestrzeni adresów IP sieci wirtualnej = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="018bf-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="018bf-139">Podsieć 1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="018bf-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="018bf-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="018bf-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="018bf-141">Lokalizacja = wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="018bf-141">Location = East US</span></span> <br>
<span data-ttu-id="018bf-142">Nazwa publicznego adresu IP bramy = gwpip</span><span class="sxs-lookup"><span data-stu-id="018bf-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="018bf-143">Brama sieci lokalnej = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="018bf-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="018bf-144">Nazwa bramy sieci wirtualnej = RMGateway</span><span class="sxs-lookup"><span data-stu-id="018bf-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="018bf-145">Konfiguracja adresów IP bramy = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="018bf-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="018bf-146"><a name="createsmgw"></a>Sekcja 1 — Konfigurowanie klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="018bf-146"><a name="createsmgw"></a>Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="018bf-147">Część 1 - pobierania pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="018bf-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="018bf-148">Zaloguj się do konta platformy Azure, w konsoli programu PowerShell z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="018bf-148">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="018bf-149">Następujące polecenie cmdlet monituje o poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="018bf-149">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="018bf-150">Po zalogowaniu pobiera ono ustawienia konta, aby były dostępne dla programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-150">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="018bf-151">Ukończenie tej części konfiguracji przy użyciu poleceń cmdlet programu PowerShell SM.</span><span class="sxs-lookup"><span data-stu-id="018bf-151">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="018bf-152">Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="018bf-152">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="018bf-153">Możesz zmienić lokalizację pliku, aby wyeksportować ją w innej lokalizacji, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="018bf-153">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="018bf-154">Otwórz plik XML, aby go edytować.</span><span class="sxs-lookup"><span data-stu-id="018bf-154">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="018bf-155">Na przykład pliku konfiguracji sieci, zobacz [schemat konfiguracji sieci](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="018bf-155">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="018bf-156">Część 2 - Sprawdź podsieć bramy</span><span class="sxs-lookup"><span data-stu-id="018bf-156">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="018bf-157">W **VirtualNetworkSites** elementu, Dodaj podsieć bramy sieci wirtualnej, jeśli nie została jeszcze utworzona.</span><span class="sxs-lookup"><span data-stu-id="018bf-157">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="018bf-158">Podczas pracy z pliku konfiguracji sieci, podsieć bramy musi być o nazwie "GatewaySubnet" lub Azure nie może rozpoznać i używać go jako podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-158">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="018bf-159">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="018bf-159">**Example:**</span></span>

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

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="018bf-160">Część 3 — Dodawanie lokacji sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="018bf-160">Part 3 - Add the local network site</span></span>
<span data-ttu-id="018bf-161">Lokacja sieci lokalnej, które można dodać reprezentuje RM sieci wirtualnej, z którym chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="018bf-161">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="018bf-162">Dodaj **LocalNetworkSites** elementu do pliku, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="018bf-162">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="018bf-163">W tym momencie w konfiguracji VPNGatewayAddress może być dowolnym prawidłowego publicznego adresu IP, ponieważ możemy jeszcze nie utworzono bramę sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="018bf-163">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="018bf-164">Po utworzymy bramy możemy zastąpić ten adres IP — symbol zastępczy poprawne publiczny adres IP przypisany do bramy protokołu RM.</span><span class="sxs-lookup"><span data-stu-id="018bf-164">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="018bf-165">Część 4 - skojarzenia sieci wirtualnej z lokacją sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="018bf-165">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="018bf-166">W tej sekcji możemy określić lokację sieci lokalnej, który chcesz połączyć sieć wirtualną do.</span><span class="sxs-lookup"><span data-stu-id="018bf-166">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="018bf-167">W takim przypadku jest sieć wirtualną Resource Manager, która wcześniej odwołaniu.</span><span class="sxs-lookup"><span data-stu-id="018bf-167">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="018bf-168">Upewnij się, że nazwy są zgodne.</span><span class="sxs-lookup"><span data-stu-id="018bf-168">Make sure the names match.</span></span> <span data-ttu-id="018bf-169">Ten krok nie powoduje utworzenia bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-169">This step does not create a gateway.</span></span> <span data-ttu-id="018bf-170">Określa bramy będą łączyć się z sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-170">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="018bf-171">Część 5 - Zapisz plik i przekazywania</span><span class="sxs-lookup"><span data-stu-id="018bf-171">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="018bf-172">Zapisz plik, a następnie zaimportuj go do platformy Azure, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="018bf-172">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="018bf-173">Upewnij się, że w przypadku zmiany ścieżki pliku jako wymaganych w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="018bf-173">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="018bf-174">Widoczny będzie podobny wynik pokazujący, że importowanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="018bf-174">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="018bf-175">Część 6 - Tworzenie bramy</span><span class="sxs-lookup"><span data-stu-id="018bf-175">Part 6 - Create the gateway</span></span>

<span data-ttu-id="018bf-176">Przed uruchomieniem w tym przykładzie należy odwoływać się do pobranego pliku konfiguracji sieci dla nazw dokładne Azure spodziewa się.</span><span class="sxs-lookup"><span data-stu-id="018bf-176">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="018bf-177">Plik konfiguracji sieci zawiera wartości klasyczne sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="018bf-177">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="018bf-178">Czasami nazwy dla klasyczne sieci wirtualne są zmieniane w pliku konfiguracji sieci, podczas tworzenia klasycznych ustawień sieci wirtualnej w portalu Azure, z powodu różnic w modelach wdrażania.</span><span class="sxs-lookup"><span data-stu-id="018bf-178">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="018bf-179">Na przykład jeśli używasz portalu Azure do utworzenia klasyczny sieć wirtualną o nazwie "Klasycznej sieci wirtualnej" i utworzony w grupie zasobów o nazwie "ClassicRG", nazwa, która jest zawarta w pliku konfiguracji sieci jest konwertowana na "Grupy ClassicRG klasycznej sieci wirtualnej".</span><span class="sxs-lookup"><span data-stu-id="018bf-179">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="018bf-180">Podczas określania nazwy sieci wirtualnej, która zawiera spacje, użyj wartości w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="018bf-180">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="018bf-181">Skorzystaj z następującego przykładu, aby utworzyć bramę routingu dynamicznego:</span><span class="sxs-lookup"><span data-stu-id="018bf-181">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="018bf-182">Stan bramy można sprawdzić za pomocą **Get-AzureVNetGateway** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="018bf-182">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="018bf-183"><a name="creatermgw"></a>Sekcja 2: Konfigurowanie bramy sieci wirtualnej RM</span><span class="sxs-lookup"><span data-stu-id="018bf-183"><a name="creatermgw"></a>Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="018bf-184">Aby utworzyć bramę sieci VPN RM sieci wirtualnej, wykonaj poniższe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="018bf-184">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="018bf-185">Nie uruchamiaj kroki do czasu, po pobraniu publicznego adresu IP dla bramy klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-185">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="018bf-186">Zaloguj się do konta platformy Azure, w konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-186">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="018bf-187">Następujące polecenie cmdlet monituje o poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="018bf-187">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="018bf-188">Po zalogowaniu ustawienia konta są pobierane, tak aby były dostępne dla programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-188">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="018bf-189">Pobierz listę subskrypcji Azure, jeśli masz więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="018bf-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="018bf-190">Wskaż subskrypcję, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="018bf-190">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="018bf-191">Utwórz bramę sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-191">Create a local network gateway.</span></span> <span data-ttu-id="018bf-192">W sieci wirtualnej brama sieci lokalnej zazwyczaj odwołuje się do lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-192">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="018bf-193">W takim przypadku bramy sieci lokalnej odwołuje się do klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-193">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="018bf-194">Nadaj nazwę za pomocą którego Azure można odwołuje się do niego, a także określ prefiks przestrzeni adresów.</span><span class="sxs-lookup"><span data-stu-id="018bf-194">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="018bf-195">Platforma Azure używa prefiksu adresu IP w celu określenia, który ruch danych należy skierować do lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-195">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="018bf-196">Jeśli musisz dostosować informacje w tym miejscu później, przed utworzeniem bramy sieci można zmodyfikować wartości i ponownie uruchomić próbki.</span><span class="sxs-lookup"><span data-stu-id="018bf-196">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="018bf-197">**-Nazwa** to nazwa ma zostać przypisany do odwoływania się do bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-197">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br><span data-ttu-id="018bf-198">
   **-AddressPrefix** jest klasycznej sieci wirtualnej przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="018bf-198">
   **-AddressPrefix** is the Address Space for your classic VNet.</span></span><br><span data-ttu-id="018bf-199">
**-GatewayIpAddress** jest publiczny adres IP bramy klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-199">
**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="018bf-200">Należy pamiętać o zmianie w poniższym przykładzie, aby odzwierciedlić poprawny adres IP.</span><span class="sxs-lookup"><span data-stu-id="018bf-200">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="018bf-201">Żądaj publicznego adresu IP do przydzielenia do bramy sieci wirtualnej sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="018bf-201">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="018bf-202">Nie można określić adresu IP, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="018bf-202">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="018bf-203">Adres IP jest dynamicznie przydzielane bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-203">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="018bf-204">Nie oznacza to jednak, że adres IP się zmienia.</span><span class="sxs-lookup"><span data-stu-id="018bf-204">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="018bf-205">Tylko zmiany adresu IP bramy sieci wirtualnej jest, gdy brama zostanie usunięta i utworzona ponownie.</span><span class="sxs-lookup"><span data-stu-id="018bf-205">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="018bf-206">Nie zmienia ono całej zmiany rozmiaru, resetowania lub innych wewnętrzny konserwacji/uaktualnienia bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="018bf-207">W tym kroku będziemy również ustawić zmiennej używanej w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="018bf-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="018bf-208">Sprawdź, czy sieci wirtualnej ma podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="018bf-209">Jeśli istnieje podsieć bramy, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="018bf-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="018bf-210">Upewnij się, że nosi nazwę podsieci bramy *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="018bf-210">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="018bf-211">Pobieranie w podsieci używanej bramy, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="018bf-211">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="018bf-212">W tym kroku będziemy również ustawić zmienną do użycia w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="018bf-212">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="018bf-213">**-Nazwa** jest nazwą sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="018bf-213">**-Name** is the name of your Resource Manager VNet.</span></span><br><span data-ttu-id="018bf-214">
   **-ResourceGroupName** jest to grupa zasobów skojarzonego z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-214">
**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="018bf-215">Podsieć bramy musi już istnieć dla tej sieci wirtualnej i musi mieć nazwę *GatewaySubnet* działała poprawnie.</span><span class="sxs-lookup"><span data-stu-id="018bf-215">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="018bf-216">Tworzenie konfiguracji adresów IP bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-216">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="018bf-217">W ramach konfiguracji bramy zostaje zdefiniowana podsieć i publiczny adres IP do użycia.</span><span class="sxs-lookup"><span data-stu-id="018bf-217">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="018bf-218">Poniższy przykład umożliwia utworzenie konfiguracji bramy.</span><span class="sxs-lookup"><span data-stu-id="018bf-218">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="018bf-219">W tym kroku **- SubnetId** i **- PublicIpAddressId** parametry muszą być przekazywane właściwość identyfikatora podsieci i obiekty adresu IP, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="018bf-219">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="018bf-220">Nie można użyć prostego ciągu.</span><span class="sxs-lookup"><span data-stu-id="018bf-220">You can't use a simple string.</span></span> <span data-ttu-id="018bf-221">Te zmienne są ustawiane w kroku żądanie publicznego adresu IP i kroku pobrać podsieci.</span><span class="sxs-lookup"><span data-stu-id="018bf-221">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="018bf-222">Utwórz bramę sieci wirtualnej Menedżera zasobów, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="018bf-222">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="018bf-223">`-VpnType` Musi być *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="018bf-223">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="018bf-224">Może upłynąć 45 minut lub więcej bramy do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="018bf-224">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="018bf-225">Po utworzeniu bramy sieci VPN, należy skopiować publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="018bf-225">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="018bf-226">Można użyć podczas konfigurowania ustawień sieci lokalnej w klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-226">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="018bf-227">Następujące polecenie cmdlet umożliwia pobrać publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="018bf-227">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="018bf-228">Publiczny adres IP na liście jest zwracany jako *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="018bf-228">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="018bf-229">Sekcja 3: Modyfikowanie klasycznych ustawień sieci wirtualnej w lokacji lokalnej</span><span class="sxs-lookup"><span data-stu-id="018bf-229">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="018bf-230">W tej sekcji możesz pracować z klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-230">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="018bf-231">Można zastąpić adres IP symbolu zastępczego, używanego podczas określania ustawień lokacji lokalnej, które będą używane do łączenia się z bramą sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="018bf-231">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="018bf-232">Eksportowanie plików konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="018bf-232">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="018bf-233">Za pomocą edytora tekstu, zmodyfikuj wartość dla VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="018bf-233">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="018bf-234">Zastąp symbol zastępczy adres IP publiczny adres IP bramy usługi Resource Manager, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="018bf-234">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="018bf-235">Zaimportuj plik konfiguracji sieci zmodyfikowane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="018bf-235">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="018bf-236"><a name="connect"></a>Sekcja 4: Tworzenie połączenia między bramami</span><span class="sxs-lookup"><span data-stu-id="018bf-236"><a name="connect"></a>Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="018bf-237">Tworzenie połączenia między bramami wymaga środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-237">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="018bf-238">Może być konieczne dodanie konta platformy Azure, aby użyć wersji klasycznej poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018bf-238">You may need to add your Azure Account to use the classic version of the  PowerShell cmdlets.</span></span> <span data-ttu-id="018bf-239">Aby to zrobić, użyj **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="018bf-239">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="018bf-240">W konsoli programu PowerShell należy ustawić klucz udostępniony.</span><span class="sxs-lookup"><span data-stu-id="018bf-240">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="018bf-241">Przed uruchomieniem poleceń cmdlet należy odwoływać się do pobranego pliku konfiguracji sieci dla nazw dokładne Azure spodziewa się.</span><span class="sxs-lookup"><span data-stu-id="018bf-241">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="018bf-242">Podczas określania nazwy sieci wirtualnej, która zawiera spacje, użyj pojedynczy znaki cudzysłowu otaczające wartość.</span><span class="sxs-lookup"><span data-stu-id="018bf-242">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="018bf-243">W poniższym przykładzie **- VNetName** jest nazwą klasycznej sieci wirtualnej i **- LocalNetworkSiteName** jest nazwa określona dla lokacji sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="018bf-243">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="018bf-244">**- SharedKey** to Generowanie i określ wartość.</span><span class="sxs-lookup"><span data-stu-id="018bf-244">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="018bf-245">W tym przykładzie użyliśmy "abc123", ale można wygenerować i korzystać z bardziej złożonych.</span><span class="sxs-lookup"><span data-stu-id="018bf-245">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="018bf-246">Ważne jest, że wartość określone w tym miejscu musi być taka sama jak wartość zostanie w następnym kroku podczas tworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="018bf-246">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="018bf-247">Zwracany powinien być wyświetlony **stanu: pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="018bf-247">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="018bf-248">Utwórz połączenie sieci VPN, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="018bf-248">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="018bf-249">Ustaw zmienne.</span><span class="sxs-lookup"><span data-stu-id="018bf-249">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="018bf-250">Utwórz połączenie.</span><span class="sxs-lookup"><span data-stu-id="018bf-250">Create the connection.</span></span> <span data-ttu-id="018bf-251">Zwróć uwagę, że **- ConnectionType** jest IPsec, nie Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="018bf-251">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="018bf-252">Sekcja 5: Sprawdź połączenia</span><span class="sxs-lookup"><span data-stu-id="018bf-252">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="018bf-253">Aby sprawdzić połączenie z klasycznej sieci wirtualnej do sieci wirtualnej Resource Manager</span><span class="sxs-lookup"><span data-stu-id="018bf-253">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="018bf-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="018bf-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="018bf-255">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="018bf-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="018bf-256">Aby sprawdzić połączenie z sieci wirtualnej Menedżera zasobów klasycznych sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="018bf-256">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="018bf-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="018bf-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="018bf-258">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="018bf-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="018bf-259"><a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="018bf-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

