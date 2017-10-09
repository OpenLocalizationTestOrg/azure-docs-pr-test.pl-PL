---
title: "aaaConfigure SSL odciążania — brama usługi aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="db588-103">Konfigurowanie bramy aplikacji na potrzeby odciążania protokołu SSL przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db588-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="db588-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="db588-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="db588-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="db588-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="db588-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="db588-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="db588-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="db588-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="db588-108">Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="db588-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="db588-109">Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="db588-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="db588-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="db588-110">Before you begin</span></span>

1. <span data-ttu-id="db588-111">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="db588-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="db588-112">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="db588-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="db588-113">Możesz utworzyć sieć wirtualną i podsieć bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="db588-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="db588-114">Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="db588-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="db588-115">Usługa Application Gateway musi sama znajdować się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="db588-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="db588-116">serwery Hello konfigurowania bramy aplikacji hello toouse musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="db588-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="db588-117">Co to jest wymagana toocreate bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="db588-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="db588-118">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="db588-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="db588-119">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="db588-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="db588-120">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="db588-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="db588-121">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="db588-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="db588-122">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="db588-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="db588-123">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="db588-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="db588-124">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te ustawienia są z uwzględnieniem wielkości liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="db588-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="db588-125">**Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="db588-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="db588-126">Obecnie tylko hello *podstawowe* reguła jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="db588-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="db588-127">Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.</span><span class="sxs-lookup"><span data-stu-id="db588-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="db588-128">**Uwagi dotyczące konfiguracji dodatkowych**</span><span class="sxs-lookup"><span data-stu-id="db588-128">**Additional configuration notes**</span></span>

<span data-ttu-id="db588-129">Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="db588-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="db588-130">Witaj **SslCertificate** zbyt dodany element**HttpListener** z wartości zmiennej hello skonfigurowanej dla certyfikatu SSL hello.</span><span class="sxs-lookup"><span data-stu-id="db588-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="db588-131">port frontonu Hello powinien być zaktualizowany too443.</span><span class="sxs-lookup"><span data-stu-id="db588-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="db588-132">**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="db588-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="db588-133">W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="db588-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="db588-134">Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.</span><span class="sxs-lookup"><span data-stu-id="db588-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="db588-135">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="db588-135">Create an application gateway</span></span>

<span data-ttu-id="db588-136">Różnica Hello przy użyciu hello Azure klasycznego modelu wdrażania i usługi Azure Resource Manager jest kolejności hello tworzenie aplikacji bramy i hello elementy toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="db588-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="db588-137">Usługa Resource Manager wszystkie składniki bramy aplikacji są konfigurowane osobno, a następnie przekaż razem toocreate zasobów bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="db588-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="db588-138">Oto toocreate kroki niezbędne hello bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db588-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="db588-139">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db588-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="db588-140">Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="db588-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="db588-141">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="db588-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="db588-142">Tworzenie zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="db588-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="db588-143">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db588-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="db588-144">Upewnij się, że przełącznika poleceń cmdlet programu PowerShell tryb toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db588-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="db588-145">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="db588-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="db588-146">Krok 1</span><span class="sxs-lookup"><span data-stu-id="db588-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="db588-147">Krok 2</span><span class="sxs-lookup"><span data-stu-id="db588-147">Step 2</span></span>

<span data-ttu-id="db588-148">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="db588-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="db588-149">Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="db588-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="db588-150">Krok 3</span><span class="sxs-lookup"><span data-stu-id="db588-150">Step 3</span></span>

<span data-ttu-id="db588-151">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db588-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="db588-152">Krok 4</span><span class="sxs-lookup"><span data-stu-id="db588-152">Step 4</span></span>

<span data-ttu-id="db588-153">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="db588-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="db588-154">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="db588-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="db588-155">To ustawienie jest używane jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="db588-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="db588-156">Upewnij się, że wszystkie toocreate polecenia używa bramy aplikacji hello same grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="db588-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="db588-157">W powyższym przykładzie hello, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** i lokalizację **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="db588-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="db588-158">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="db588-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="db588-159">powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="db588-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="db588-160">Krok 1</span><span class="sxs-lookup"><span data-stu-id="db588-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="db588-161">W tym przykładzie przypisuje hello adres zakresu 10.0.0.0/24 tooa podsieci zmiennej toobe używane toocreate sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="db588-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="db588-162">Krok 2</span><span class="sxs-lookup"><span data-stu-id="db588-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="db588-163">Ten przykład tworzy sieć wirtualną o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="db588-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="db588-164">Krok 3</span><span class="sxs-lookup"><span data-stu-id="db588-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="db588-165">W tym przykładzie przypisuje hello podsieci obiektu toovariable $subnet hello dalsze czynności.</span><span class="sxs-lookup"><span data-stu-id="db588-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="db588-166">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="db588-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="db588-167">Ten przykład tworzy zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="db588-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="db588-168">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="db588-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="db588-169">Krok 1</span><span class="sxs-lookup"><span data-stu-id="db588-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="db588-170">Ten przykład tworzy konfigurację IP bramy dla aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="db588-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="db588-171">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="db588-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="db588-172">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="db588-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="db588-173">Krok 2</span><span class="sxs-lookup"><span data-stu-id="db588-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="db588-174">Ten przykład konfiguruje hello zaplecza puli adresów IP o nazwie **pool01** z adresami IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="db588-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="db588-175">Te wartości są adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="db588-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="db588-176">Zastąp hello adresów IP z hello poprzedzających przykład z adresami IP hello punktów końcowych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="db588-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="db588-177">Krok 3</span><span class="sxs-lookup"><span data-stu-id="db588-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="db588-178">Ten przykład konfiguruje ustawienia bramy aplikacji **poolsetting01** zrównoważonym tooload ruchu sieciowego w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="db588-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="db588-179">Krok 4</span><span class="sxs-lookup"><span data-stu-id="db588-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="db588-180">Ten przykład konfiguruje hello frontonu portu IP o nazwie **frontendport01** dla punktu końcowego hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="db588-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="db588-181">Krok 5</span><span class="sxs-lookup"><span data-stu-id="db588-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="db588-182">Ten przykład konfiguruje hello certyfikatu używanego na potrzeby połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="db588-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="db588-183">certyfikat Hello musi toobe w formacie pfx, a hello hasło musi zawierać od 4 znaki too12.</span><span class="sxs-lookup"><span data-stu-id="db588-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="db588-184">Krok 6</span><span class="sxs-lookup"><span data-stu-id="db588-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="db588-185">Ten przykład tworzy hello frontonu konfiguracji IP o nazwie **fipconfig01** i publicznego adresu IP z konfiguracji IP frontonu hello hello współpracowników.</span><span class="sxs-lookup"><span data-stu-id="db588-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="db588-186">Krok 7</span><span class="sxs-lookup"><span data-stu-id="db588-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="db588-187">Ten przykład tworzy nazwę odbiornika hello **listener01** i skojarzone hello konfiguracji IP frontonu toohello portów frontonu i certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="db588-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="db588-188">Krok 8</span><span class="sxs-lookup"><span data-stu-id="db588-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="db588-189">Ten przykład tworzy hello reguły modułu równoważenia obciążenia routingu o nazwie **rule01** który konfiguruje zachowanie usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="db588-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="db588-190">Krok 9</span><span class="sxs-lookup"><span data-stu-id="db588-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="db588-191">Ten przykład konfiguruje hello rozmiar wystąpienia bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="db588-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="db588-192">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="db588-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="db588-193">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="db588-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="db588-194">Możesz wybrać następujące wartości: Standard_Small, Standard_Medium i Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="db588-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="db588-195">Krok 10</span><span class="sxs-lookup"><span data-stu-id="db588-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="db588-196">W tym kroku definiowana toouse zasad SSL hello na bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="db588-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="db588-197">Odwiedź stronę [skonfigurować protokół SSL wersje zasad i mechanizmów szyfrowania w bramie aplikacji](application-gateway-configure-ssl-policy-powershell.md) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="db588-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="db588-198">Tworzenie bramy aplikacji przy użyciu polecenia New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="db588-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="db588-199">Ten przykład tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="db588-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="db588-200">Przykład Witaj bramy aplikacji hello nosi nazwę **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="db588-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="db588-201">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="db588-201">Get application gateway DNS name</span></span>

<span data-ttu-id="db588-202">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="db588-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="db588-203">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="db588-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="db588-204">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="db588-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="db588-205">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db588-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="db588-206">toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="db588-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="db588-207">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="db588-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="db588-208">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="db588-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="db588-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db588-209">Next steps</span></span>

<span data-ttu-id="db588-210">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB), zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="db588-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="db588-211">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="db588-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="db588-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="db588-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="db588-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="db588-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

