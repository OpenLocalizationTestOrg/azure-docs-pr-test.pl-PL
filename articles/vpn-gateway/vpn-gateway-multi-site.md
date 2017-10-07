---
title: "Połącz lokacji toomultiple sieci wirtualnej przy użyciu bramy sieci VPN i programu PowerShell: klasycznym | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomoże łączenia wielu lokalnych witryn tooa wirtualnej sieci lokalnej dla hello klasycznego modelu wdrażania przy użyciu bramy sieci VPN."
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
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="ae185-103">Dodaj tooa połączenia lokacja-lokacja sieci wirtualnej z istniejącego połączenia bramy sieci VPN (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="ae185-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae185-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae185-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ae185-105">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="ae185-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="ae185-106">W tym artykule przedstawiono przy użyciu programu PowerShell tooadd lokacja-lokacja (S2S) połączeń tooa bramy sieci VPN z istniejącego połączenia.</span><span class="sxs-lookup"><span data-stu-id="ae185-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="ae185-107">Ten typ połączenia jest często tooas określonej konfiguracji "obejmujący wiele lokacji".</span><span class="sxs-lookup"><span data-stu-id="ae185-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="ae185-108">Hello czynności w tym artykule dotyczą sieci toovirtual utworzone za pomocą hello klasycznego modelu wdrażania (znanej także jako Service Management).</span><span class="sxs-lookup"><span data-stu-id="ae185-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="ae185-109">Te kroki należy stosować konfiguracje połączenia ważnych tooExpressRoute/lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ae185-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="ae185-110">Modele i metody wdrażania</span><span class="sxs-lookup"><span data-stu-id="ae185-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="ae185-111">Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ae185-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="ae185-112">Artykuł jest dostępny, możemy połączyć bezpośrednio tooit z tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="ae185-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="ae185-113">O łączeniu</span><span class="sxs-lookup"><span data-stu-id="ae185-113">About connecting</span></span>

<span data-ttu-id="ae185-114">Można połączyć wiele lokalnej lokacji tooa jednej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ae185-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="ae185-115">Jest to szczególnie atrakcyjne tworzenie hybrydowych rozwiązań w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ae185-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="ae185-116">Tworzenie bramy sieci wirtualnej platformy Azure tooyour połączenia z wieloma lokacjami jest podobne toocreating innych połączeń lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ae185-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="ae185-117">W rzeczywistości, można użyć istniejącej bramy sieci VPN platformy Azure, tak długo, jak bramy hello jest dynamiczny (opartej na trasach).</span><span class="sxs-lookup"><span data-stu-id="ae185-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="ae185-118">Jeśli masz już statycznych bramy sieci wirtualnej podłączonej tooyour, można zmienić bez konieczności w kolejności tooaccommodate obejmujący wiele lokacji sieci wirtualnej hello toorebuild toodynamic typu bramy hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="ae185-119">Przed zmianą typu routingu hello, upewnij się, że bramy sieci VPN, lokalnymi obsługuje konfiguracje sieci VPN opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="ae185-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="ae185-120">![diagram obejmujący wiele lokacji](./media/vpn-gateway-multi-site/multisite.png "obejmujący wiele lokacji")</span><span class="sxs-lookup"><span data-stu-id="ae185-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="ae185-121">Punkty tooconsider</span><span class="sxs-lookup"><span data-stu-id="ae185-121">Points tooconsider</span></span>

<span data-ttu-id="ae185-122">**Nie będzie możliwe toouse hello portalu toomake zmiany toothis wirtualnej sieci.**</span><span class="sxs-lookup"><span data-stu-id="ae185-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="ae185-123">Należy toomake pliku konfiguracji sieci toohello zmiany zamiast hello portalu.</span><span class="sxs-lookup"><span data-stu-id="ae185-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="ae185-124">Jeśli wprowadzisz zmiany w portalu hello zastępują ustawienia odwołania obejmujący wiele lokacji w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ae185-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="ae185-125">Chcesz powinno ujawnić przy użyciu pliku konfiguracji sieci hello czasu hello przeprowadzisz hello procedury obejmujący wiele lokacji.</span><span class="sxs-lookup"><span data-stu-id="ae185-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="ae185-126">Jednak jeśli masz wiele osób pracuje w konfiguracji sieci, należy toomake się, że wszyscy zna tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="ae185-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="ae185-127">To nie oznacza, że nie możesz użyć portalu hello na wszystkich.</span><span class="sxs-lookup"><span data-stu-id="ae185-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="ae185-128">Można go dla wszystkich innych urządzeń, z wyjątkiem wprowadzania konfiguracji zmiany toothis konkretnej wirtualnej sieci.</span><span class="sxs-lookup"><span data-stu-id="ae185-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae185-129">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ae185-129">Before you begin</span></span>

<span data-ttu-id="ae185-130">Przed rozpoczęciem konfigurowania należy sprawdzić, czy następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ae185-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="ae185-131">Zgodny sprzęt sieci VPN dla każdej lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ae185-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="ae185-132">Sprawdź [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md) tooverify Jeśli hello urządzenia, które mają toouse czegoś znanego toobe zgodne.</span><span class="sxs-lookup"><span data-stu-id="ae185-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="ae185-133">Zewnętrznie połączonej publiczny adres IPv4 dla każdego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ae185-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="ae185-134">adres IP Hello nie może znajdować się za urządzeniem NAT</span><span class="sxs-lookup"><span data-stu-id="ae185-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="ae185-135">To wymaganie.</span><span class="sxs-lookup"><span data-stu-id="ae185-135">This is requirement.</span></span>
* <span data-ttu-id="ae185-136">Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae185-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ae185-137">Upewnij się, że hello wersji usługi zarządzania (SM) w wersji Menedżera zasobów toohello dodanie.</span><span class="sxs-lookup"><span data-stu-id="ae185-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="ae185-138">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ae185-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="ae185-139">Osoby, która jest wykorzystać Konfigurowanie sprzętu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ae185-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="ae185-140">Będziesz mieć toohave silne znajomością działania tooconfigure urządzenia sieci VPN lub pracy z osobą, która jest.</span><span class="sxs-lookup"><span data-stu-id="ae185-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="ae185-141">zakresy adresów IP Hello mają toouse dla sieci wirtualnej (jeśli jeszcze nie utworzono jeden).</span><span class="sxs-lookup"><span data-stu-id="ae185-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="ae185-142">Witaj zakresów adresów IP dla każdej lokacji sieci lokalnej hello, które będą łączyć się z.</span><span class="sxs-lookup"><span data-stu-id="ae185-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="ae185-143">Należy się upewnić, że hello zakresy adresów IP każdego hello lokacji sieci lokalnej, które mają toodo tooconnect nie nakładają się na siebie toomake.</span><span class="sxs-lookup"><span data-stu-id="ae185-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="ae185-144">W przeciwnym razie konfiguracji hello przekazywanych spowoduje odrzucenie portalu hello lub hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="ae185-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="ae185-145">Na przykład jeśli masz dwie lokacje sieci lokalnej, czy zawierają 10.2.3.0/24 zakres adresów IP hello i czy masz pakiet o docelowy adres 10.2.3.3 Azure nie wiedzieć lokacji, do której ma się zakresów adresów hello toobecause toosend hello pakietu nakładające się.</span><span class="sxs-lookup"><span data-stu-id="ae185-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="ae185-146">problemy z routingu tooprevent Azure nie zezwala tooupload pliku konfiguracji, który ma nakładające się zakresy.</span><span class="sxs-lookup"><span data-stu-id="ae185-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="ae185-147">1. Tworzenie sieci VPN typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="ae185-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="ae185-148">Jeśli masz już sieć VPN lokacja-lokacja z bramą routingu dynamicznego ponosić!</span><span class="sxs-lookup"><span data-stu-id="ae185-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="ae185-149">Możesz przejść za[Eksportuj ustawienia konfiguracji sieci wirtualnej hello](#export).</span><span class="sxs-lookup"><span data-stu-id="ae185-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="ae185-150">Jeśli nie, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ae185-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="ae185-151">Jeśli masz już sieć wirtualną do lokacji, ale nie statyczne bramy routingu (na podstawie zasad):</span><span class="sxs-lookup"><span data-stu-id="ae185-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="ae185-152">Zmień Twoje bramy typu toodynamic routingu.</span><span class="sxs-lookup"><span data-stu-id="ae185-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="ae185-153">Obejmujący wiele lokacji sieci VPN wymaga dynamicznej bramy routingu (znanej także jako opartej na trasach).</span><span class="sxs-lookup"><span data-stu-id="ae185-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="ae185-154">Typ bramy toochange, użytkownik będzie toofirst delete hello istniejącą bramę, a następnie utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="ae185-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="ae185-155">Aby uzyskać instrukcje, zobacz [jak toochange hello routingu typ sieci VPN dla bramy](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ae185-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="ae185-156">Konfigurowanie nowej bramy i utworzyć tunel sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ae185-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="ae185-157">Aby uzyskać instrukcje, zobacz [Brama sieci VPN w hello klasycznego portalu Azure](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ae185-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="ae185-158">Najpierw zmień Twoje bramy typu toodynamic routingu.</span><span class="sxs-lookup"><span data-stu-id="ae185-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="ae185-159">Jeśli nie masz lokacja-lokacja sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ae185-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="ae185-160">Tworzenie sieci wirtualnej lokacja-lokacja, korzystając z tych instrukcji: [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja-lokacja w hello klasycznego portalu Azure](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="ae185-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="ae185-161">Należy skonfigurować bramę routingu dynamicznego przy użyciu tych instrukcji: [Brama sieci VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ae185-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="ae185-162">Należy się tooselect **routingu dynamicznego** dla danego typu bramy.</span><span class="sxs-lookup"><span data-stu-id="ae185-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="ae185-163"><a name="export"></a>2. Plik konfiguracji sieci hello eksportu</span><span class="sxs-lookup"><span data-stu-id="ae185-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="ae185-164">Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="ae185-165">Możesz zmienić lokalizację hello hello pliku tooexport tooa różnych lokalizacji, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="ae185-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="ae185-166">3. Plik konfiguracji sieci Otwórz hello</span><span class="sxs-lookup"><span data-stu-id="ae185-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="ae185-167">Otwórz plik konfiguracji sieci hello, który został pobrany w ostatnim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="ae185-168">Użyj dowolnego edytora xml, który chcesz.</span><span class="sxs-lookup"><span data-stu-id="ae185-168">Use any xml editor that you like.</span></span> <span data-ttu-id="ae185-169">Plik Hello powinien wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="ae185-169">hello file should look similar toohello following:</span></span>

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

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="ae185-170">4. Dodawanie odwołania do wielu lokacji</span><span class="sxs-lookup"><span data-stu-id="ae185-170">4. Add multiple site references</span></span>
<span data-ttu-id="ae185-171">Po dodaniu lub usunięciu informacji o lokacji odniesienia, będzie wprowadzać zmian konfiguracji toohello ConnectionsToLocalNetwork/elementu LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="ae185-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="ae185-172">Dodawanie nowego odwołania do lokacji lokalnej wyzwala Azure toocreate nowe tunelu.</span><span class="sxs-lookup"><span data-stu-id="ae185-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="ae185-173">W poniższym przykładzie hello konfiguracja sieci hello jest połączenia pojedynczej lokacji.</span><span class="sxs-lookup"><span data-stu-id="ae185-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="ae185-174">Zapisz plik hello, po zakończeniu wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="ae185-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="ae185-175">tooadd dodatkowe odsyłacze do witryn (Tworzenie konfiguracji wielu lokacji), po prostu dodaj dodatkowe "elementu LocalNetworkSiteRef" wierszy, jak pokazano w poniższym przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="ae185-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="ae185-176">5. Plik konfiguracji sieci hello importu</span><span class="sxs-lookup"><span data-stu-id="ae185-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="ae185-177">Importowanie pliku konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-177">Import hello network configuration file.</span></span> <span data-ttu-id="ae185-178">Podczas importowania tego pliku ze zmianami hello hello nowych tuneli zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="ae185-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="ae185-179">tunele Hello użyje hello bramy dynamiczne utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ae185-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="ae185-180">Możesz użyć hello klasycznego portalu lub plik hello tooimport programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae185-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="ae185-181">6. Pobierz kluczy</span><span class="sxs-lookup"><span data-stu-id="ae185-181">6. Download keys</span></span>
<span data-ttu-id="ae185-182">Po dodaniu Twoje nowe tuneli klawisze hello PowerShell polecenia cmdlet "Get-AzureVNetGatewayKey" tooget hello IPsec i IKE wstępnego dla każdego tunelu.</span><span class="sxs-lookup"><span data-stu-id="ae185-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="ae185-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ae185-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="ae185-184">Jeśli wolisz, możesz również użyć hello *uzyskać wirtualnych sieci bramy klucz wstępny* tooget interfejsu API REST hello kluczy wstępnych.</span><span class="sxs-lookup"><span data-stu-id="ae185-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="ae185-185">7. Sprawdź połączenia</span><span class="sxs-lookup"><span data-stu-id="ae185-185">7. Verify your connections</span></span>
<span data-ttu-id="ae185-186">Sprawdź stan tunelu obejmujący wiele lokacji hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="ae185-187">Po pobraniu hello kluczy dla każdego tunelu, należy tooverify połączenia.</span><span class="sxs-lookup"><span data-stu-id="ae185-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="ae185-188">Użyj tooget "Get-AzureVnetConnection" tuneli listę sieci wirtualnej, jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="ae185-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="ae185-189">VNet1 jest nazwa hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ae185-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="ae185-190">Przykład zwrotu:</span><span class="sxs-lookup"><span data-stu-id="ae185-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
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
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="ae185-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae185-191">Next steps</span></span>

<span data-ttu-id="ae185-192">toolearn więcej informacji na temat bram sieci VPN, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ae185-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
