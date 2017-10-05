---
title: "Połączenie wirtualnej sieci z wieloma lokacjami przy użyciu bramy sieci VPN i programu PowerShell: klasycznym | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano podłączania wielu lokacji lokalnej lokalnego do sieci wirtualnej dla klasycznym modelu wdrażania przy użyciu bramy sieci VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: bb3129f70f5eeed99d5889226aa6727f675b6217
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="26fb0-103">Dodaj połączenie lokacja-lokacja z sieci wirtualnej z istniejącego połączenia bramy sieci VPN (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="26fb0-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26fb0-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="26fb0-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="26fb0-105">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="26fb0-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="26fb0-106">Ten artykuł przeprowadzi Cię przez dodawanie połączeń lokacja-lokacja (S2S) do bramy sieci VPN, który ma istniejącego połączenia przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26fb0-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="26fb0-107">Połączenia tego typu jest często określany jako "obejmujący wiele lokacji" konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="26fb0-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="26fb0-108">Kroki opisane w tym artykule dotyczą sieci wirtualnych utworzonych przy użyciu klasycznego modelu wdrażania (znanej także jako Service Management).</span><span class="sxs-lookup"><span data-stu-id="26fb0-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="26fb0-109">Te kroki nie dotyczą konfiguracji połączenia ważnych ExpressRoute/lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="26fb0-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="26fb0-110">Modele i metody wdrażania</span><span class="sxs-lookup"><span data-stu-id="26fb0-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="26fb0-111">Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="26fb0-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="26fb0-112">Po udostępnieniu artykułu możemy link bezpośrednio do niego z tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="26fb0-112">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="26fb0-113">O łączeniu</span><span class="sxs-lookup"><span data-stu-id="26fb0-113">About connecting</span></span>

<span data-ttu-id="26fb0-114">Można połączyć wiele lokacji lokalnej do jednej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-114">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="26fb0-115">Jest to szczególnie atrakcyjne tworzenie hybrydowych rozwiązań w chmurze.</span><span class="sxs-lookup"><span data-stu-id="26fb0-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="26fb0-116">Tworzenie obejmujący wiele lokacji połączenie bramy sieci wirtualnej platformy Azure jest podobny do tworzenia innych połączeń lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="26fb0-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="26fb0-117">W rzeczywistości, można użyć istniejącej bramy sieci VPN platformy Azure, tak długo, jak bramy jest dynamiczny (opartej na trasach).</span><span class="sxs-lookup"><span data-stu-id="26fb0-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="26fb0-118">Jeśli masz już podłączony do sieci wirtualnej bramy statyczne, można zmienić typu bramy na dynamiczny, bez konieczności odbudować sieci wirtualnej, aby zmieścił się w wielu lokacjach.</span><span class="sxs-lookup"><span data-stu-id="26fb0-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="26fb0-119">Przed zmianą typu routingu, upewnij się, że bramy sieci VPN, lokalnymi obsługuje konfiguracje sieci VPN opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="26fb0-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="26fb0-120">![diagram obejmujący wiele lokacji](./media/vpn-gateway-multi-site/multisite.png "obejmujący wiele lokacji")</span><span class="sxs-lookup"><span data-stu-id="26fb0-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="26fb0-121">Kwestie do rozważenia</span><span class="sxs-lookup"><span data-stu-id="26fb0-121">Points to consider</span></span>

<span data-ttu-id="26fb0-122">**Nie można korzystać z portalu, aby wprowadzić zmiany w tej sieci wirtualnej.**</span><span class="sxs-lookup"><span data-stu-id="26fb0-122">**You won't be able to use the portal to make changes to this virtual network.**</span></span> <span data-ttu-id="26fb0-123">Należy wprowadzić zmiany w pliku konfiguracji sieci, zamiast korzystać z portalu.</span><span class="sxs-lookup"><span data-stu-id="26fb0-123">You need to make changes to the network configuration file instead of using the portal.</span></span> <span data-ttu-id="26fb0-124">Jeśli wprowadzisz zmiany w portalu zastępują ustawienia odwołania obejmujący wiele lokacji w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="26fb0-125">Uważasz doświadczenia, do czasu zakończenia procedury obejmujący wiele lokacji przy użyciu pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="26fb0-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="26fb0-126">Jednak jeśli masz wiele osób pracuje w konfiguracji sieci, należy upewnij się, że wszyscy zna tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="26fb0-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="26fb0-127">To nie oznacza, że nie możesz użyć portalu w ogóle.</span><span class="sxs-lookup"><span data-stu-id="26fb0-127">This doesn't mean that you can't use the portal at all.</span></span> <span data-ttu-id="26fb0-128">Można go dla wszystkich innych urządzeń, z wyjątkiem zmiany konfiguracji tej określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="26fb0-129">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="26fb0-129">Before you begin</span></span>

<span data-ttu-id="26fb0-130">Przed rozpoczęciem konfigurowania należy sprawdzić, czy następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="26fb0-130">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="26fb0-131">Zgodny sprzęt sieci VPN dla każdej lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="26fb0-132">Sprawdź [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md) Aby sprawdzić, czy urządzenie, którego chcesz użyć czegoś, co jest uznany za zgodny.</span><span class="sxs-lookup"><span data-stu-id="26fb0-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="26fb0-133">Zewnętrznie połączonej publiczny adres IPv4 dla każdego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="26fb0-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="26fb0-134">Adres IP nie może znajdować się za urządzeniem NAT</span><span class="sxs-lookup"><span data-stu-id="26fb0-134">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="26fb0-135">To wymaganie.</span><span class="sxs-lookup"><span data-stu-id="26fb0-135">This is requirement.</span></span>
* <span data-ttu-id="26fb0-136">Niezbędne jest zainstalowanie najnowszej wersji poleceń cmdlet programu Azure PowerShell. </span><span class="sxs-lookup"><span data-stu-id="26fb0-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="26fb0-137">Upewnij się, że oprócz wersji usługi Resource Manager w wersji usługi zarządzania (ko).</span><span class="sxs-lookup"><span data-stu-id="26fb0-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span></span> <span data-ttu-id="26fb0-138">Zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="26fb0-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="26fb0-139">Osoby, która jest wykorzystać Konfigurowanie sprzętu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="26fb0-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="26fb0-140">Będzie konieczne silne wiedzę jak skonfigurować urządzenie sieci VPN lub pracować z osobą, która jest.</span><span class="sxs-lookup"><span data-stu-id="26fb0-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="26fb0-141">Zakresy adresów IP, które ma być używany dla sieci wirtualnej (jeśli jeszcze nie utworzono jeden).</span><span class="sxs-lookup"><span data-stu-id="26fb0-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="26fb0-142">Zakresy adresów IP dla każdej lokacji sieci lokalnej, które będą łączyć się z.</span><span class="sxs-lookup"><span data-stu-id="26fb0-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="26fb0-143">Należy się upewnić, czy zakresy adresów IP dla każdej lokacji sieci lokalnej, które chcesz się połączyć, aby nie pokrywają się.</span><span class="sxs-lookup"><span data-stu-id="26fb0-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="26fb0-144">W przeciwnym razie konfiguracja przekazywanych spowoduje odrzucenie portalu lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="26fb0-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span></span><br><span data-ttu-id="26fb0-145">Na przykład jeśli masz dwie lokacje sieci lokalnej, czy zawierają 10.2.3.0/24 zakres adresów IP i czy masz pakiet o docelowy adres 10.2.3.3 Azure nie wiadomo, witryn, które chcesz wysyłać pakietów do, ponieważ nakładają się na zakresy adresów.</span><span class="sxs-lookup"><span data-stu-id="26fb0-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="26fb0-146">Aby zapobiec problemom routingu, Azure nie zezwala na przekazywanie pliku konfiguracji, który ma nakładające się zakresy.</span><span class="sxs-lookup"><span data-stu-id="26fb0-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="26fb0-147">1. Tworzenie sieci VPN typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="26fb0-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="26fb0-148">Jeśli masz już sieć VPN lokacja-lokacja z bramą routingu dynamicznego ponosić!</span><span class="sxs-lookup"><span data-stu-id="26fb0-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="26fb0-149">Możesz przejść do [Eksportuj ustawienia konfiguracji sieci wirtualnej](#export).</span><span class="sxs-lookup"><span data-stu-id="26fb0-149">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="26fb0-150">Jeśli nie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="26fb0-150">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="26fb0-151">Jeśli masz już sieć wirtualną do lokacji, ale nie statyczne bramy routingu (na podstawie zasad):</span><span class="sxs-lookup"><span data-stu-id="26fb0-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="26fb0-152">Należy zmienić typ bramy do routingu dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="26fb0-152">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="26fb0-153">Obejmujący wiele lokacji sieci VPN wymaga dynamicznej bramy routingu (znanej także jako opartej na trasach).</span><span class="sxs-lookup"><span data-stu-id="26fb0-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="26fb0-154">Aby zmienić typ bramy, musisz najpierw usunąć istniejącą bramę, a następnie utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="26fb0-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span> <span data-ttu-id="26fb0-155">Aby uzyskać instrukcje, zobacz [jak zmienić typ routingu sieci VPN dla bramy](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="26fb0-155">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="26fb0-156">Konfigurowanie nowej bramy i utworzyć tunel sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="26fb0-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="26fb0-157">Aby uzyskać instrukcje, zobacz [Brama sieci VPN w klasycznym portalu Azure](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="26fb0-157">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="26fb0-158">Najpierw należy zmienić typ bramy do routingu dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="26fb0-158">First, change your gateway type to dynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="26fb0-159">Jeśli nie masz lokacja-lokacja sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="26fb0-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="26fb0-160">Tworzenie sieci wirtualnej lokacja-lokacja, korzystając z tych instrukcji: [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja-lokacja w klasycznym portalu Azure](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="26fb0-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="26fb0-161">Należy skonfigurować bramę routingu dynamicznego przy użyciu tych instrukcji: [Brama sieci VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="26fb0-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="26fb0-162">Należy wybrać **routingu dynamicznego** dla danego typu bramy.</span><span class="sxs-lookup"><span data-stu-id="26fb0-162">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="26fb0-163"><a name="export"></a>2. Eksportowanie plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="26fb0-163"><a name="export"></a>2. Export the network configuration file</span></span>
<span data-ttu-id="26fb0-164">Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="26fb0-164">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="26fb0-165">Możesz zmienić lokalizację pliku, aby wyeksportować ją w innej lokalizacji, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="26fb0-165">You can change the location of the file to export to a different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="26fb0-166">3. Otwórz plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="26fb0-166">3. Open the network configuration file</span></span>
<span data-ttu-id="26fb0-167">Otwórz plik konfiguracji sieci, który został pobrany w ostatnim kroku.</span><span class="sxs-lookup"><span data-stu-id="26fb0-167">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="26fb0-168">Użyj dowolnego edytora xml, który chcesz.</span><span class="sxs-lookup"><span data-stu-id="26fb0-168">Use any xml editor that you like.</span></span> <span data-ttu-id="26fb0-169">Plik powinien wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="26fb0-169">The file should look similar to the following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="26fb0-170">4. Dodawanie odwołania do wielu lokacji</span><span class="sxs-lookup"><span data-stu-id="26fb0-170">4. Add multiple site references</span></span>
<span data-ttu-id="26fb0-171">Po dodaniu lub usunięciu informacji o lokacji odniesienia, będzie wprowadzać zmian konfiguracji do ConnectionsToLocalNetwork/elementu LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="26fb0-171">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="26fb0-172">Dodawanie nowych powoduje odwołanie lokacji lokalnej platformy Azure w celu utworzenia nowego tunelu.</span><span class="sxs-lookup"><span data-stu-id="26fb0-172">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="26fb0-173">W poniższym przykładzie konfiguracja sieci jest połączenia pojedynczej lokacji.</span><span class="sxs-lookup"><span data-stu-id="26fb0-173">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="26fb0-174">Zapisz plik, po zakończeniu wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="26fb0-174">Save the file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="26fb0-175">Aby dodać odwołania do dodatkowej lokacji (Tworzenie konfiguracji wielu lokacji), po prostu dodaj dodatkowe wiersze "Elementu LocalNetworkSiteRef", jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="26fb0-175">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="26fb0-176">5. Importowanie pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="26fb0-176">5. Import the network configuration file</span></span>
<span data-ttu-id="26fb0-177">Zaimportuj plik konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="26fb0-177">Import the network configuration file.</span></span> <span data-ttu-id="26fb0-178">Podczas importowania tego pliku ze zmianami, zostaną dodane nowe tuneli.</span><span class="sxs-lookup"><span data-stu-id="26fb0-178">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="26fb0-179">Tunele użyje bramy dynamiczne utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-179">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="26fb0-180">Możesz użyć klasycznego portalu lub programu PowerShell do zaimportowania pliku.</span><span class="sxs-lookup"><span data-stu-id="26fb0-180">You can either use the classic portal, or PowerShell to import the file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="26fb0-181">6. Pobierz kluczy</span><span class="sxs-lookup"><span data-stu-id="26fb0-181">6. Download keys</span></span>
<span data-ttu-id="26fb0-182">Po dodaniu Twoje nowe tuneli, użyj polecenia cmdlet programu PowerShell "Get-AzureVNetGatewayKey", aby pobrać kluczy wstępnych IPsec i IKE dla każdego tunelu.</span><span class="sxs-lookup"><span data-stu-id="26fb0-182">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="26fb0-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="26fb0-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="26fb0-184">Jeśli wolisz, można również użyć *uzyskać wirtualnych sieci bramy klucz wstępny* interfejsu API REST w celu uzyskania kluczy wstępnych.</span><span class="sxs-lookup"><span data-stu-id="26fb0-184">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="26fb0-185">7. Sprawdź połączenia</span><span class="sxs-lookup"><span data-stu-id="26fb0-185">7. Verify your connections</span></span>
<span data-ttu-id="26fb0-186">Sprawdź stan tunelu obejmujący wiele lokacji.</span><span class="sxs-lookup"><span data-stu-id="26fb0-186">Check the multi-site tunnel status.</span></span> <span data-ttu-id="26fb0-187">Po pobraniu kluczy dla każdego tunelu, należy sprawdzić połączenia.</span><span class="sxs-lookup"><span data-stu-id="26fb0-187">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="26fb0-188">Użyj "Get-AzureVnetConnection", aby uzyskać listę tuneli sieci wirtualnej, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="26fb0-188">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="26fb0-189">VNet1 jest nazwą sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fb0-189">VNet1 is the name of the VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="26fb0-190">Przykład zwrotu:</span><span class="sxs-lookup"><span data-stu-id="26fb0-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="26fb0-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26fb0-191">Next steps</span></span>

<span data-ttu-id="26fb0-192">Aby dowiedzieć się więcej na temat bram sieci VPN, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="26fb0-192">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
