---
title: "Połącz tooan komputera przy użyciu punkt-lokacja sieci wirtualnej platformy Azure i certyfikat uwierzytelniania: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Bezpiecznego łączenia z sieci wirtualnej tooyour komputera, tworząc połączenie bramy sieci VPN typu punkt-lokacja używa wstępnego uwierzytelniania certyfikatu. Ten artykuł dotyczy modelu wdrażania usługi Resource Manager toohello i korzysta z programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="314c0-104">Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="314c0-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="314c0-105">W tym artykule opisano, jak toocreate sieci wirtualnej za pomocą połączenia punkt-lokacja we wdrożeniu usługi Resource Manager hello modelu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="314c0-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="314c0-106">Ta konfiguracja korzysta z certyfikatów tooauthenticate hello połączenie klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="314c0-107">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="314c0-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="314c0-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="314c0-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="314c0-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="314c0-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="314c0-110">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="314c0-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="314c0-111">Brama sieci VPN typu punkt-lokacja (P2S) umożliwia tworzenie sieci wirtualnej tooyour bezpiecznego połączenia z pojedynczym komputerem klienckim.</span><span class="sxs-lookup"><span data-stu-id="314c0-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="314c0-112">Połączenia sieci VPN punkt-lokacja są przydatne, gdy chcesz tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takie, gdy są Niezale¿nie z domu lub konferencji.</span><span class="sxs-lookup"><span data-stu-id="314c0-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="314c0-113">P2S sieci VPN jest również toouse przydatne rozwiązanie, zamiast VPN lokacja-lokacja, jeśli istnieje tylko kilka klientów, którzy potrzebują tooa tooconnect sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="314c0-114">Używa P2S hello gniazda Tunelowanie protokołu SSTP (Secure), która jest oparta na protokole SSL protokołu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="314c0-115">Uruchamiając go z komputera klienckiego hello jest nawiązywane połączenie sieci VPN P2S.</span><span class="sxs-lookup"><span data-stu-id="314c0-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Połącz komputer tooan sieci wirtualnej Azure - diagram połączenie punkt-lokacja](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="314c0-117">Połączenia uwierzytelniania certyfikatów punkt-lokacja wymagają następujących hello:</span><span class="sxs-lookup"><span data-stu-id="314c0-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="314c0-118">Brama sieci VPN oparta na trasie.</span><span class="sxs-lookup"><span data-stu-id="314c0-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="314c0-119">Witaj klucz publiczny (plik cer) dla certyfikatu głównego, czyli tooAzure przekazane.</span><span class="sxs-lookup"><span data-stu-id="314c0-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="314c0-120">Po przekazaniu plików certyfikatów hello jest uznawany za zaufany certyfikat i jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="314c0-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="314c0-121">Certyfikat klienta, który jest generowany na podstawie certyfikatu głównego hello i zainstalowane na każdym komputerze klienckim, w którym będą łączyć toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="314c0-122">Ten certyfikat jest używany do uwierzytelniania klientów.</span><span class="sxs-lookup"><span data-stu-id="314c0-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="314c0-123">Pakiet konfiguracji klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-123">A VPN client configuration package.</span></span> <span data-ttu-id="314c0-124">Pakiet konfiguracji klienta VPN Hello zawiera hello informacji niezbędnych do powitania klienta tooconnect toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="314c0-125">Pakiet HELLO konfiguruje hello istniejącej sieci VPN klienta, który jest natywny toohello systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="314c0-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="314c0-126">Każdy klient, który łączy muszą być skonfigurowane przy użyciu hello konfiguracji pakietu.</span><span class="sxs-lookup"><span data-stu-id="314c0-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="314c0-127">Połączenia typu punkt-lokacja nie wymagają urządzenia sieci VPN ani lokalnego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="314c0-128">Witaj połączenia sieci VPN jest tworzony za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="314c0-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="314c0-129">Na powitania po stronie serwera firma Microsoft obsługuje protokół SSTP w wersji 1.0, 1.1 i 1.2.</span><span class="sxs-lookup"><span data-stu-id="314c0-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="314c0-130">powitania klienta decyduje o tym, które toouse wersji.</span><span class="sxs-lookup"><span data-stu-id="314c0-130">hello client decides which version toouse.</span></span> <span data-ttu-id="314c0-131">W przypadku systemu Windows 8.1 i nowszych protokół SSTP domyślnie używa wersji 1.2.</span><span class="sxs-lookup"><span data-stu-id="314c0-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="314c0-132">Aby uzyskać więcej informacji na temat połączenia punkt-lokacja, zobacz hello [punkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="314c0-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="314c0-133">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="314c0-133">Before beginning</span></span>

* <span data-ttu-id="314c0-134">Sprawdź, czy masz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="314c0-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="314c0-135">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="314c0-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="314c0-136">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="314c0-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="314c0-137">Aby uzyskać więcej informacji na temat instalacji poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="314c0-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="314c0-138"><a name="example"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="314c0-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="314c0-139">Można użyć hello przykładowe wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="314c0-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="314c0-140">Firma Microsoft Ustaw zmienne hello w sekcji [1](#declare) hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="314c0-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="314c0-141">Można użyć kroki hello jako przewodnika i użyj wartości hello bez konieczności ich zmieniania lub je zmienić tooreflect środowiska.</span><span class="sxs-lookup"><span data-stu-id="314c0-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="314c0-142">**Nazwa: VNet1**</span><span class="sxs-lookup"><span data-stu-id="314c0-142">**Name: VNet1**</span></span>
* <span data-ttu-id="314c0-143">**Przestrzeń adresowa: 192.168.0.0/16** i **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="314c0-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="314c0-144">W tym przykładzie używamy więcej niż jeden tooillustrate przestrzeni adresów ta konfiguracja działa wiele przestrzeni adresowych.</span><span class="sxs-lookup"><span data-stu-id="314c0-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="314c0-145">Jednak ta konfiguracja nie wymaga wielu przestrzeni adresowych.</span><span class="sxs-lookup"><span data-stu-id="314c0-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="314c0-146">**Nazwa podsieci: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="314c0-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="314c0-147">**Zakres adresów podsieci: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="314c0-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="314c0-148">**Nazwa podsieci: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="314c0-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="314c0-149">**Zakres adresów podsieci: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="314c0-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="314c0-150">**Nazwa podsieci: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="314c0-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="314c0-151">Nazwa podsieci Hello *GatewaySubnet* jest obowiązkowa w przypadku toowork bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="314c0-152">**Zakres adresów podsieci bramy: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="314c0-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="314c0-153">**Pula adresów klienta sieci VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="314c0-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="314c0-154">Klienci sieci VPN, łączący toohello sieci wirtualnej za pomocą to połączenie punkt-lokacja otrzymywać adresy IP z hello pula adresów klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="314c0-155">**Subskrypcja:** Jeśli masz więcej niż jedną subskrypcję, sprawdź, czy używasz hello właściwy.</span><span class="sxs-lookup"><span data-stu-id="314c0-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="314c0-156">**Grupa zasobów: TestRG**</span><span class="sxs-lookup"><span data-stu-id="314c0-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="314c0-157">**Lokalizacja: Wschodnie stany USA**</span><span class="sxs-lookup"><span data-stu-id="314c0-157">**Location: East US**</span></span>
* <span data-ttu-id="314c0-158">**Serwera DNS: Adres IP** powitania serwera DNS ma toouse do rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="314c0-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="314c0-159">**Nazwa bramy: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="314c0-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="314c0-160">**Nazwa publicznego adresu IP: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="314c0-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="314c0-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="314c0-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="314c0-162"><a name="declare"></a>1. Logowanie się i ustawianie zmiennych</span><span class="sxs-lookup"><span data-stu-id="314c0-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="314c0-163">W tej sekcji Zaloguj się i zadeklarować hello wartości używanych dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="314c0-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="314c0-164">Witaj zadeklarowane jako wartości są używane w hello przykładowe skrypty.</span><span class="sxs-lookup"><span data-stu-id="314c0-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="314c0-165">Zmień tooreflect wartości hello własnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="314c0-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="314c0-166">Lub użyj hello zadeklarowany wartości i wykonanie kroków hello jako wykonywania.</span><span class="sxs-lookup"><span data-stu-id="314c0-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="314c0-167">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i logowania tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="314c0-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="314c0-168">To polecenie cmdlet monituje o poświadczenia logowania hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="314c0-169">Po zalogowaniu pobraniu ustawienia konta, aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="314c0-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="314c0-170">Pobierz listę subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="314c0-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="314c0-171">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="314c0-172">Zadeklaruj zmienne hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="314c0-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="314c0-173">Użyj hello następujące przykładowe, zastępując hello własne wartości gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="314c0-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="314c0-174"><a name="ConfigureVNet"></a>2. Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="314c0-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="314c0-175">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="314c0-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="314c0-176">Utwórz hello konfiguracje podsieci sieci wirtualnej hello, ich nazewnictwa *frontonu*, *zaplecza*, i *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="314c0-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="314c0-177">Te prefiksy muszą być częścią hello przestrzeni adresowej sieci wirtualnej, która została zadeklarowana.</span><span class="sxs-lookup"><span data-stu-id="314c0-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="314c0-178">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-178">Create hello virtual network.</span></span>

  <span data-ttu-id="314c0-179">W tym przykładzie powitania serwera DNS jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="314c0-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="314c0-180">Określenie wartości nie powoduje utworzenia nowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="314c0-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="314c0-181">Witaj adres IP serwera DNS, który określisz powinna być serwera DNS, który może rozpoznawać nazwy hello hello zasoby, które są nawiązywane.</span><span class="sxs-lookup"><span data-stu-id="314c0-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="314c0-182">W tym przykładzie użyliśmy prywatnego adresu IP, ale istnieje duże prawdopodobieństwo, że nie jest hello adres IP serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="314c0-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="314c0-183">Należy się toouse własne wartości.</span><span class="sxs-lookup"><span data-stu-id="314c0-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="314c0-184">Określ zmienne hello hello sieci wirtualnej, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="314c0-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="314c0-185">Brama sieci VPN musi mieć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="314c0-186">Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="314c0-187">adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="314c0-188">Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="314c0-189">Nie można zażądać przypisania statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="314c0-190">Jednak nie oznacza, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="314c0-191">Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie.</span><span class="sxs-lookup"><span data-stu-id="314c0-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="314c0-192">Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="314c0-193">Zażądaj dynamicznie przydzielanego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="314c0-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="314c0-194"><a name="creategateway"></a>3. Tworzenie bramy sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="314c0-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="314c0-195">Skonfiguruj i Utwórz bramę sieci wirtualnej hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="314c0-196">Witaj *elementu GatewayType -* musi być **Vpn** i hello *- VpnType* musi być **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="314c0-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="314c0-197">Brama sieci VPN może potrwać too45 toocomplete minut, w zależności od hello [jednostka sku bramy](vpn-gateway-about-vpn-gateway-settings.md) wybrania.</span><span class="sxs-lookup"><span data-stu-id="314c0-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="314c0-198"><a name="addresspool"></a>4. Dodaj pulę adresów klienta sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="314c0-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="314c0-199">Po zakończeniu tworzenia bramy sieci VPN hello można dodać puli adresów klienta sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="314c0-200">Hello pula adresów klienta sieci VPN jest zakres hello, z których klienci VPN hello otrzymywać adresu IP podczas nawiązywania połączenia.</span><span class="sxs-lookup"><span data-stu-id="314c0-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="314c0-201">Użyj zakresu prywatnych adresów IP, który nie nakłada się na hello lokalizacji lokalnej, która nawiązywanie połączenia z lub hello sieci wirtualnej, który ma tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="314c0-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="314c0-202">W tym przykładzie hello pula adresów klienta sieci VPN jest zadeklarowany jako [zmiennej](#declare) w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="314c0-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="314c0-203"><a name="Certificates"></a>5. Generowanie certyfikatów klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="314c0-204">Certyfikaty są używane przez klientów sieci VPN platformy Azure tooauthenticate sieci VPN punkt-lokacja.</span><span class="sxs-lookup"><span data-stu-id="314c0-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="314c0-205">Możesz przekazać hello informacje o kluczu publicznym z tooAzure certyfikatu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="314c0-206">klucz publiczny Hello następnie jest uznawany za "zaufanych".</span><span class="sxs-lookup"><span data-stu-id="314c0-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="314c0-207">Certyfikaty klienta musi generowane na podstawie hello zaufanego certyfikatu głównego, a następnie zainstalowany na każdym komputerze klienckim w hello certyfikatów bieżącego użytkownika/osobistego magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="314c0-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="314c0-208">certyfikatu Hello jest używane tooauthenticate powitania klienta, gdy inicjują połączenia toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="314c0-209">Jeśli używasz certyfikatów z podpisem własnym, należy je utworzyć przy użyciu określonych parametrów.</span><span class="sxs-lookup"><span data-stu-id="314c0-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="314c0-210">Można utworzyć certyfikatu z podpisem własnym za pomocą instrukcji hello [środowiska PowerShell i Windows 10](vpn-gateway-certificates-point-to-site.md), lub jeśli nie masz systemu Windows 10, możesz użyć [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="314c0-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="314c0-211">Jest ważne, należy wykonać kroki hello w instrukcjach hello podczas generowania certyfikatów głównych z podpisem własnym i certyfikatów klientów.</span><span class="sxs-lookup"><span data-stu-id="314c0-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="314c0-212">W przeciwnym razie nie będzie zgodny z połączeń P2S hello certyfikaty, które można wygenerować i zostanie wyświetlony błąd połączenia.</span><span class="sxs-lookup"><span data-stu-id="314c0-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="314c0-213"><a name="cer"></a>1. Uzyskaj plik cer hello hello certyfikatu głównego</span><span class="sxs-lookup"><span data-stu-id="314c0-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="314c0-214"><a name="generate"></a>2. Generowanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="314c0-215"><a name="upload"></a>6. Przekaż hello głównego certyfikatu informacje o kluczu publicznym</span><span class="sxs-lookup"><span data-stu-id="314c0-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="314c0-216">Upewnij się, że zakończono tworzenie bramy VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="314c0-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="314c0-217">Po zakończeniu, możesz przekazać plik .cer hello, (zawierający informacje o kluczu publicznym hello) dla tooAzure certyfikatów zaufanych certyfikatów głównych.</span><span class="sxs-lookup"><span data-stu-id="314c0-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="314c0-218">Po przekazaniu pliku a.cer Azure może być używany tooauthenticate klientów, którzy zainstalowali generowane na podstawie hello zaufanego certyfikatu głównego certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="314c0-219">Możesz przekazać pliki certyfikatów zaufanych głównych - zapasowej tooa łącznie 20 - później, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="314c0-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="314c0-220">Zadeklarować zmienną hello nazwy certyfikatu, zastępując wartość hello własne.</span><span class="sxs-lookup"><span data-stu-id="314c0-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="314c0-221">Zamień na ścieżkę pliku hello własnych, a następnie uruchom polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="314c0-222">Przekaż hello tooAzure informacje o kluczu publicznym.</span><span class="sxs-lookup"><span data-stu-id="314c0-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="314c0-223">Po przekazaniu informacji o certyfikacie hello Azure uwzględnia ten toobe z zaufanym certyfikatem głównym.</span><span class="sxs-lookup"><span data-stu-id="314c0-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="314c0-224"><a name="clientconfig"></a>7. Pobierz pakiet konfiguracji klienta sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="314c0-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="314c0-225">tooa tooconnect sieci wirtualnej za pomocą sieci VPN punkt-lokacja, każdego klienta należy zainstalować pakiet konfiguracji klienta, który konfiguruje hello natywny klient VPN przy hello ustawień i plików, które są niezbędne tooconnect toohello wirtualnej sieci.</span><span class="sxs-lookup"><span data-stu-id="314c0-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="314c0-226">natywny klient VPN systemu Windows hello konfiguruje pakietu konfiguracji klienta VPN Hello, nie instaluje nowe lub inne klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="314c0-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="314c0-227">Tak długo, jak wersja hello zgodna architektura hello powitania klienta, można użyć hello pakietu tej samej konfiguracji klienta sieci VPN na każdym komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="314c0-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="314c0-228">Aby hello listę systemów operacyjnych klienta, które są obsługiwane, zobacz hello [połączeńpunkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="314c0-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="314c0-229">Po utworzeniu bramy hello, można wygenerować i pobrać pakiet konfiguracji powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="314c0-230">W tym przykładzie pliki do pobrania pakietu hello na klientach 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="314c0-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="314c0-231">Jeśli chcesz toodownload hello 32-bitowego klienta, zastąp "Amd64" "x86".</span><span class="sxs-lookup"><span data-stu-id="314c0-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="314c0-232">Możesz również pobrać powitania klienta VPN za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="314c0-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="314c0-233">Skopiuj i Wklej łącze hello jest zwracany tooa pakiet przeglądarki sieci web toodownload hello, zwracając szczególną uwagę cudzysłowy hello tooremove otaczającego hello łącza.</span><span class="sxs-lookup"><span data-stu-id="314c0-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="314c0-234">Pobierz i zainstaluj pakiet hello na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="314c0-235">Jeśli zostanie wyświetlone okno podręczne SmartScreen, kliknij pozycję **Więcej informacji**, a następnie pozycję **Uruchom mimo to**.</span><span class="sxs-lookup"><span data-stu-id="314c0-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="314c0-236">Można także zapisać tooinstall pakietu hello na innych komputerach klienckich.</span><span class="sxs-lookup"><span data-stu-id="314c0-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="314c0-237">Na komputerze klienckim hello Przejdź zbyt**ustawienia sieciowe** i kliknij przycisk **VPN**.</span><span class="sxs-lookup"><span data-stu-id="314c0-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="314c0-238">Witaj połączenia sieci VPN jest wyświetlana nazwa hello hello sieci wirtualnej, która łączy się z.</span><span class="sxs-lookup"><span data-stu-id="314c0-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="314c0-239"><a name="clientcertificate"></a>8. Instalowanie wyeksportowanego certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="314c0-240">Jeśli chcesz toocreate P2S połączenie z komputera klienckiego niż hello jeden używane certyfikaty klienta na powitania toogenerate należy tooinstall certyfikat klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="314c0-241">Podczas instalowania certyfikatu klienta, należy hello hasło, które utworzono podczas eksportowania hello certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="314c0-242">Zazwyczaj jest wystarczy dwukrotnie hello certyfikatu i instalując je.</span><span class="sxs-lookup"><span data-stu-id="314c0-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="314c0-243">Upewnij się, że certyfikat klienta na powitania została wyeksportowana do pliku PFX oraz hello całego łańcucha certyfikatów (który jest domyślnym hello).</span><span class="sxs-lookup"><span data-stu-id="314c0-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="314c0-244">W przeciwnym razie informacje o certyfikacie głównym hello nie jest obecny na komputerze klienckim hello i powitania klienta nie będzie możliwe tooauthenticate poprawnie.</span><span class="sxs-lookup"><span data-stu-id="314c0-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="314c0-245">Aby uzyskać więcej informacji, zobacz [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install) (Instalowanie wyeksportowanego certyfikatu klienta).</span><span class="sxs-lookup"><span data-stu-id="314c0-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="314c0-246"><a name="connect"></a>9. Połącz tooAzure</span><span class="sxs-lookup"><span data-stu-id="314c0-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="314c0-247">tooconnect tooyour sieci wirtualnej, na komputerze klienckim hello Przejdź tooVPN połączeń i Znajdź hello połączenia sieci VPN, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="314c0-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="314c0-248">Nazwie hello sama nazwa jak sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="314c0-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="314c0-249">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="314c0-249">Click **Connect**.</span></span> <span data-ttu-id="314c0-250">Komunikat podręczny może pojawić się odwołuje się toousing hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="314c0-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="314c0-251">Kliknij przycisk **Kontynuuj** toouse podwyższonego poziomu uprawnień.</span><span class="sxs-lookup"><span data-stu-id="314c0-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="314c0-252">Na powitania **połączenia** stan strony, kliknij przycisk **Connect** toostart hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="314c0-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="314c0-253">Jeśli widzisz **wybierz certyfikat** ekranu, sprawdź, czy powitania klienta certyfikatu przedstawiający hello jedną, które mają toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="314c0-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="314c0-254">Jeśli nie, hello strzałkę listy rozwijanej tooselect hello poprawny certyfikat, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="314c0-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![Klient sieci VPN łączy tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="314c0-256">Połączenie zostało ustanowione.</span><span class="sxs-lookup"><span data-stu-id="314c0-256">Your connection is established.</span></span>

  ![Ustanowiono połączenie](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="314c0-258">Rozwiązywanie problemów dotyczących połączeń typu punkt-lokacja</span><span class="sxs-lookup"><span data-stu-id="314c0-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="314c0-259"><a name="verify"></a>10. Weryfikowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="314c0-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="314c0-260">tooverify, że połączenie sieci VPN jest aktywne, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="314c0-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="314c0-261">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-261">View hello results.</span></span> <span data-ttu-id="314c0-262">Zauważ, że adres IP hello otrzymany jest jeden hello adresów w puli adresów klienta sieci VPN hello punkt-lokacja, określona w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="314c0-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="314c0-263">wyniki Hello są podobny przykład toothis:</span><span class="sxs-lookup"><span data-stu-id="314c0-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="314c0-264"><a name="connectVM"></a>Połącz tooa maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="314c0-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="314c0-265"><a name="addremovecert"></a>Dodawanie lub usuwanie certyfikatu głównego</span><span class="sxs-lookup"><span data-stu-id="314c0-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="314c0-266">Zaufane certyfikaty główne można dodawać do platformy Azure lub z niej usuwać.</span><span class="sxs-lookup"><span data-stu-id="314c0-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="314c0-267">Po usunięciu certyfikatu głównego, klientów, którzy mają certyfikat generowane na podstawie certyfikatu głównego hello nie mogą uwierzytelnić się i nie będzie możliwe tooconnect.</span><span class="sxs-lookup"><span data-stu-id="314c0-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="314c0-268">Jeśli mają tooauthenticate klienta i połączyć, należy tooinstall nowego certyfikatu klienta generowane na podstawie certyfikatu głównego, który jest zaufany tooAzure (przekazanego).</span><span class="sxs-lookup"><span data-stu-id="314c0-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="314c0-269"><a name="addtrustedroot"></a>tooadd zaufanego certyfikatu głównego</span><span class="sxs-lookup"><span data-stu-id="314c0-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="314c0-270">Możesz dodać zapasowej too20 głównego certyfikatu .cer pliki tooAzure.</span><span class="sxs-lookup"><span data-stu-id="314c0-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="314c0-271">następujące Hello czynności pomocy dodać certyfikat główny:</span><span class="sxs-lookup"><span data-stu-id="314c0-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="314c0-272"><a name="certmethod1"></a>Metoda 1</span><span class="sxs-lookup"><span data-stu-id="314c0-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="314c0-273">Jest to hello najbardziej efektywny metody tooupload certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="314c0-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="314c0-274">Przygotuj tooupload pliku .cer hello:</span><span class="sxs-lookup"><span data-stu-id="314c0-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="314c0-275">Przekaż plik hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-275">Upload hello file.</span></span> <span data-ttu-id="314c0-276">Jednocześnie możesz przekazać tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="314c0-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="314c0-277">tooverify przekazać ten plik certyfikatu hello:</span><span class="sxs-lookup"><span data-stu-id="314c0-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="314c0-278"><a name="certmethod2"></a>Metoda 2</span><span class="sxs-lookup"><span data-stu-id="314c0-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="314c0-279">Ta metoda jest więcej czynności niż metoda 1, ale skonfigurowano hello takiego samego wyniku.</span><span class="sxs-lookup"><span data-stu-id="314c0-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="314c0-280">Został uwzględniony w razie potrzeby tooview hello certyfikatu danych.</span><span class="sxs-lookup"><span data-stu-id="314c0-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="314c0-281">Tworzenie i przygotowanie hello tooAzure tooadd w nowego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="314c0-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="314c0-282">Wyeksportować klucz publiczny hello, ponieważ certyfikat x.509 szyfrowany algorytmem Base-64 (. CER), a następnie otwórz go w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="314c0-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="314c0-283">Skopiuj wartości hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="314c0-283">Copy hello values, as shown in hello following example:</span></span>

  ![certyfikat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="314c0-285">Kopiowanie danych certyfikatu hello, upewnij się, że możesz skopiować tekst hello jako pojedynczy wiersz ciągłego bez powrotu karetki i nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="314c0-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="314c0-286">Toomodify może być konieczne widoku w too'Show Edytor tekstu hello Symbol/Pokaż wszystkie znaki toosee hello karetki zwraca i wiersz źródła danych.</span><span class="sxs-lookup"><span data-stu-id="314c0-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="314c0-287">Określ nazwę certyfikatu hello i informacje o kluczu jako zmienną.</span><span class="sxs-lookup"><span data-stu-id="314c0-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="314c0-288">Zastąp informacje hello własny, jak pokazano na powitania w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="314c0-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="314c0-289">Dodaj nowy certyfikat główny hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-289">Add hello new root certificate.</span></span> <span data-ttu-id="314c0-290">Można dodawać tylko jeden certyfikat naraz.</span><span class="sxs-lookup"><span data-stu-id="314c0-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="314c0-291">Możesz sprawdzić, czy nowy certyfikat hello została poprawnie dodana przy użyciu hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="314c0-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="314c0-292"><a name="removerootcert"></a>tooremove certyfikatu głównego</span><span class="sxs-lookup"><span data-stu-id="314c0-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="314c0-293">Zadeklaruj zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="314c0-294">Usuń certyfikat hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="314c0-295">Użyj powitania po tooverify przykład, który hello certyfikat został pomyślnie usunięty.</span><span class="sxs-lookup"><span data-stu-id="314c0-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="314c0-296"><a name="revoke"></a>Odwoływanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="314c0-297">Certyfikaty klienta można odwołać.</span><span class="sxs-lookup"><span data-stu-id="314c0-297">You can revoke client certificates.</span></span> <span data-ttu-id="314c0-298">certyfikat Hello listy odwołania umożliwia tooselectively odmowy połączenia punkt-lokacja, w oparciu o certyfikaty klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="314c0-299">Różni się to od usuwania zaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="314c0-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="314c0-300">Jeśli usuniesz .cer certyfikatu zaufanego głównego z platformy Azure, odwołuje hello dostępu dla wszystkich certyfikatów klienta wygenerowany podpisane przez hello certyfikat główny odwołane.</span><span class="sxs-lookup"><span data-stu-id="314c0-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="314c0-301">Odwoływanie certyfikatu klienta, zamiast hello certyfikatu głównego, umożliwia hello innych certyfikatów, które zostały wygenerowane z hello głównego certyfikatu toocontinue toobe używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="314c0-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="314c0-302">Hello popularną praktyką jest toouse hello certyfikatu toomanage dostęp do konta root na poziomach zespół lub organizacja, używając cofnięte certyfikaty klienta dla szczegółowej kontroli dostępu na poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="314c0-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="314c0-303"><a name="revokeclientcert"></a>toorevoke certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="314c0-304">Pobrać hello odcisk palca certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="314c0-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="314c0-305">Aby uzyskać więcej informacji, zobacz [jak tooretrieve hello odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="314c0-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="314c0-306">Skopiuj Edytor tekstu tooa informacji hello i Usuń wszystkie spacje tak, aby ciąg.</span><span class="sxs-lookup"><span data-stu-id="314c0-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="314c0-307">Ten ciąg jest zadeklarowana jako zmienna w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="314c0-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="314c0-308">Zadeklaruj zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-308">Declare hello variables.</span></span> <span data-ttu-id="314c0-309">Upewnij się, że palca hello toodeclare, który można pobrać hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="314c0-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="314c0-310">Dodaj hello odcisk palca toohello listy odwołania certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="314c0-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="314c0-311">Po dodaniu hello odcisk palca zostanie wyświetlony "Powodzenie".</span><span class="sxs-lookup"><span data-stu-id="314c0-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="314c0-312">Sprawdź, czy że odcisk palca hello dodano listy odwołania certyfikatów toohello.</span><span class="sxs-lookup"><span data-stu-id="314c0-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="314c0-313">Po dodaniu hello odcisk palca certyfikatu hello nie można już tooconnect używane.</span><span class="sxs-lookup"><span data-stu-id="314c0-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="314c0-314">Klienci, którzy spróbuj tooconnect przy użyciu tego certyfikatu wyświetlony komunikat z informacją, że ten certyfikat hello nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="314c0-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="314c0-315"><a name="reinstateclientcert"></a>tooreinstate certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="314c0-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="314c0-316">Certyfikat klienta można przywrócić przez usunięcie hello odcisk palca z listy hello odwołanych certyfikatów klientów.</span><span class="sxs-lookup"><span data-stu-id="314c0-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="314c0-317">Zadeklaruj zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-317">Declare hello variables.</span></span> <span data-ttu-id="314c0-318">Upewnij się, że zadeklarować hello poprawne odcisk palca certyfikatu hello, które mają tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="314c0-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="314c0-319">Usuń hello odcisk palca certyfikatu z listy odwołania certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="314c0-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="314c0-320">Sprawdź, czy odcisku palca hello jest usuwany z hello odwołany listy.</span><span class="sxs-lookup"><span data-stu-id="314c0-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="314c0-321"><a name="faq"></a>Często zadawane pytania dotyczące połączeń typu punkt-lokacja</span><span class="sxs-lookup"><span data-stu-id="314c0-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="314c0-322">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="314c0-322">Next steps</span></span>
<span data-ttu-id="314c0-323">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="314c0-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="314c0-324">Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="314c0-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="314c0-325">toounderstand więcej informacji na temat sieci i maszyn wirtualnych, zobacz [omówienie sieci platformy Azure i maszyny Wirtualnej systemu Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="314c0-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
