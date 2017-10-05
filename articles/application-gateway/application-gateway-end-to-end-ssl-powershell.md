---
title: "Konfigurowanie protokołu SSL trasie do bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania kompleksowe SSL z bramy aplikacji przy użyciu programu PowerShell usługi Azure Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="37f66-103">Konfigurowanie protokołu SSL trasie do bramy aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="37f66-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="37f66-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="37f66-104">Overview</span></span>

<span data-ttu-id="37f66-105">Brama aplikacji w obsługuje pełnego szyfrowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="37f66-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="37f66-106">Polega to na tym, że usługa Application Gateway przerywa połączenie SSL na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="37f66-107">Następnie brama stosuje do ruchu reguły routingu, ponownie szyfruje pakiet i przekazuje pakiet do odpowiedniego serwera zaplecza na podstawie zdefiniowanych reguł routingu.</span><span class="sxs-lookup"><span data-stu-id="37f66-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="37f66-108">Każda odpowiedź z serwera sieci Web przechodzi przez ten sam proces z powrotem do użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="37f66-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="37f66-109">Inna funkcja tej bramy aplikacji obsługuje Określanie niestandardowych opcji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="37f66-110">Brama aplikacji w obsługuje wyłączenie Następująca wersja protokołu; **TLSv1.0**, **TLSv1.1**, i **TLSv1.2** jako również definiowanie którego mechanizmy według priorytetu i szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="37f66-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="37f66-111">Aby dowiedzieć się więcej na temat opcji SSL można skonfigurować, odwiedź stronę [Przegląd zasad SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37f66-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37f66-112">Protokół SSL 2.0 i 3.0 protokołu SSL są domyślnie wyłączone i nie można włączyć.</span><span class="sxs-lookup"><span data-stu-id="37f66-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="37f66-113">One są uważane za niebezpieczne i nie będą mogły być używane z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![Scenariusz obrazu][scenario]

## <a name="scenario"></a><span data-ttu-id="37f66-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="37f66-115">Scenario</span></span>

<span data-ttu-id="37f66-116">W tym scenariuszu Dowiedz się jak utworzyć bramę aplikacji przy użyciu pełnego protokołu SSL przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37f66-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="37f66-117">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="37f66-117">This scenario will:</span></span>

* <span data-ttu-id="37f66-118">Utwórz grupę zasobów o nazwie **zarządcy zasobów appgw**</span><span class="sxs-lookup"><span data-stu-id="37f66-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="37f66-119">Tworzenie sieci wirtualnej o nazwie **appgwvnet** z 10.0.0.0/16 przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="37f66-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="37f66-120">Utwórz dwie podsieci o nazwie **appgwsubnet** i **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="37f66-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="37f66-121">Utwórz bramę małych aplikacji obsługi pełnego szyfrowania SSL w tej wersji protokołów SSL limity i mechanizmów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="37f66-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="37f66-122">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="37f66-122">Before you begin</span></span>

<span data-ttu-id="37f66-123">Aby skonfigurować protokół SSL kompleksowe z bramy aplikacji, certyfikat jest wymagany dla bramy i certyfikaty są wymagane dla serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="37f66-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="37f66-124">Certyfikat bramy jest używany do szyfrowania i odszyfrowywania ruchu wysyłane do niego przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="37f66-125">Certyfikat bramy musi mieć format wymiana informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="37f66-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="37f66-126">Ten format pliku umożliwia klucz prywatny można wyeksportować co jest wymagane przez bramę aplikacji do szyfrowania i deszyfrowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="37f66-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="37f66-127">Do szyfrowania SSL kompleksowe wewnętrznej bazy danych musi być białej z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="37f66-128">Jest to realizowane przez przekazywanie publicznego certyfikatu zapleczy na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="37f66-129">Dzięki temu, że bramy aplikacji komunikuje się wyłącznie z wystąpień znane wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="37f66-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="37f66-130">To dodatkowe zabezpiecza komunikację pełnego.</span><span class="sxs-lookup"><span data-stu-id="37f66-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="37f66-131">Ten proces jest opisane w poniższych krokach:</span><span class="sxs-lookup"><span data-stu-id="37f66-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="37f66-132">Utwórz grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="37f66-132">Create the Resource Group</span></span>

<span data-ttu-id="37f66-133">Ta sekcja przeprowadzi Cię przez proces tworzenia grupy zasobów, zawierającą bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="37f66-134">Krok 1</span><span class="sxs-lookup"><span data-stu-id="37f66-134">Step 1</span></span>

<span data-ttu-id="37f66-135">Zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37f66-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="37f66-136">Krok 2</span><span class="sxs-lookup"><span data-stu-id="37f66-136">Step 2</span></span>

<span data-ttu-id="37f66-137">Wybierz subskrypcję do użycia na potrzeby tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="37f66-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="37f66-138">Krok 3</span><span class="sxs-lookup"><span data-stu-id="37f66-138">Step 3</span></span>

<span data-ttu-id="37f66-139">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="37f66-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="37f66-140">Tworzenie sieci wirtualnej i podsieci dla bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="37f66-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="37f66-141">Poniższy przykład tworzy sieć wirtualną z dwoma podsieciami.</span><span class="sxs-lookup"><span data-stu-id="37f66-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="37f66-142">W jednej podsieci jest używany do przechowywania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="37f66-143">Innych podsieci jest używana do zapleczy hosting aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="37f66-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="37f66-144">Krok 1</span><span class="sxs-lookup"><span data-stu-id="37f66-144">Step 1</span></span>

<span data-ttu-id="37f66-145">Przypisz zakres adresów dla tej podsieci, można użyć dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="37f66-146">Podsieci skonfigurowane dla bramy aplikacji należy ustalać poprawnie.</span><span class="sxs-lookup"><span data-stu-id="37f66-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="37f66-147">Brama aplikacji można skonfigurować dla maksymalnie 10 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="37f66-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="37f66-148">Każde wystąpienie ma jeden adres IP z podsieci.</span><span class="sxs-lookup"><span data-stu-id="37f66-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="37f66-149">Zbyt małe podsieci może niekorzystnie wpłynąć na skalowanie w poziomie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="37f66-150">Krok 2</span><span class="sxs-lookup"><span data-stu-id="37f66-150">Step 2</span></span>

<span data-ttu-id="37f66-151">Przypisz zakres adresów do użycia dla puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="37f66-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="37f66-152">Krok 3</span><span class="sxs-lookup"><span data-stu-id="37f66-152">Step 3</span></span>

<span data-ttu-id="37f66-153">Tworzenie sieci wirtualnej z podsieciami zdefiniowane w powyższych kroków.</span><span class="sxs-lookup"><span data-stu-id="37f66-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="37f66-154">Krok 4</span><span class="sxs-lookup"><span data-stu-id="37f66-154">Step 4</span></span>

<span data-ttu-id="37f66-155">Pobieranie zasobu sieci wirtualnej i zasoby podsieci do użycia w kolejnych krokach:</span><span class="sxs-lookup"><span data-stu-id="37f66-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="37f66-156">Tworzenie publicznego adresu IP dla konfiguracji frontonu</span><span class="sxs-lookup"><span data-stu-id="37f66-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="37f66-157">Utwórz zasób publicznego adresu IP do użycia dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="37f66-158">Ten publiczny adres IP jest używany następujący krok.</span><span class="sxs-lookup"><span data-stu-id="37f66-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="37f66-159">Brama aplikacji nie obsługuje korzystanie z publicznego adresu IP utworzony ze zdefiniowaną etykietą domeny.</span><span class="sxs-lookup"><span data-stu-id="37f66-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="37f66-160">Obsługiwane jest tylko publiczny adres IP z etykietą utworzony dynamicznie domeny.</span><span class="sxs-lookup"><span data-stu-id="37f66-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="37f66-161">Jeśli potrzebujesz dns przyjazną nazwę bramy aplikacji, zaleca się przy użyciu rekordu CNAME jako alias.</span><span class="sxs-lookup"><span data-stu-id="37f66-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="37f66-162">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="37f66-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="37f66-163">Wszystkie elementy konfiguracji są ustawiane przed utworzeniem bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="37f66-164">Poniższe kroki umożliwiają utworzenie elementów konfiguracji wymaganych w przypadku zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="37f66-165">Krok 1</span><span class="sxs-lookup"><span data-stu-id="37f66-165">Step 1</span></span>

<span data-ttu-id="37f66-166">Utwórz konfigurację IP bramy aplikacji, to ustawienie określa, jakie podsieci używa bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="37f66-167">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci skonfigurowane i kieruje ruchem sieciowym na adresy IP w puli adresów IP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="37f66-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="37f66-168">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="37f66-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="37f66-169">Krok 2</span><span class="sxs-lookup"><span data-stu-id="37f66-169">Step 2</span></span>

<span data-ttu-id="37f66-170">Tworzenie konfiguracji IP frontonu, to ustawienie mapuje adres prywatny lub publiczny ip frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="37f66-171">Następny krok kojarzy publicznego adresu IP w poprzednim kroku z konfiguracją IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="37f66-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="37f66-172">Krok 3</span><span class="sxs-lookup"><span data-stu-id="37f66-172">Step 3</span></span>

<span data-ttu-id="37f66-173">Skonfiguruj pulę adresów IP zaplecza z adresami IP serwerów sieci web zaplecza.</span><span class="sxs-lookup"><span data-stu-id="37f66-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="37f66-174">Będą to adresy IP odbierające ruch sieciowy pochodzący z punktu końcowego adresu IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="37f66-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="37f66-175">Można zastąpić następujące adresy IP, aby dodać własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="37f66-176">W pełni kwalifikowaną nazwą domeny (FQDN) jest również prawidłową wartość zamiast adresu ip dla serwerów zaplecza za pomocą przełącznika - BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="37f66-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="37f66-177">Krok 4</span><span class="sxs-lookup"><span data-stu-id="37f66-177">Step 4</span></span>

<span data-ttu-id="37f66-178">Skonfiguruj port IP frontonu publiczny punkt końcowy IP.</span><span class="sxs-lookup"><span data-stu-id="37f66-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="37f66-179">Jest to port, podłączoną do użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="37f66-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="37f66-180">Krok 5</span><span class="sxs-lookup"><span data-stu-id="37f66-180">Step 5</span></span>

<span data-ttu-id="37f66-181">Konfigurowanie certyfikatu dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="37f66-182">Ten certyfikat służy do odszyfrowania i Szyfruj ponownie ruch na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="37f66-183">Ten przykład umożliwia skonfigurowanie certyfikatu używanego na potrzeby połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="37f66-184">Certyfikat musi być w formacie PFX, a hasło musi składać się z 4–12 znaków.</span><span class="sxs-lookup"><span data-stu-id="37f66-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="37f66-185">Krok 6</span><span class="sxs-lookup"><span data-stu-id="37f66-185">Step 6</span></span>

<span data-ttu-id="37f66-186">Utwórz odbiornik HTTP bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="37f66-187">Przypisywanie konfiguracji ip frontonu, port i certyfikat protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="37f66-188">Krok 7</span><span class="sxs-lookup"><span data-stu-id="37f66-188">Step 7</span></span>

<span data-ttu-id="37f66-189">Przekaż certyfikat do użycia z włączonym protokołem SSL wewnętrznej bazy danych puli zasobów.</span><span class="sxs-lookup"><span data-stu-id="37f66-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="37f66-190">Domyślnego badania pobiera klucza publicznego z **domyślne** powiązanie SSL na adres IP zaplecza na i porównuje wartość klucza publicznego odbiera wartość klucza publicznego zostanie podana tutaj.</span><span class="sxs-lookup"><span data-stu-id="37f66-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="37f66-191">Pobrane klucz publiczny nie musi być planowanej lokacji, do których ruch **Jeśli** korzystasz z nagłówkami hosta i SNI na zaplecza.</span><span class="sxs-lookup"><span data-stu-id="37f66-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="37f66-192">W razie wątpliwości, odwiedź stronę https://127.0.0.1/ na zapleczy, aby potwierdzić, certyfikat, który jest używany dla **domyślne** powiązania SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="37f66-193">W tej sekcji, Użyj klucza publicznego z tym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="37f66-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="37f66-194">Jeśli korzystasz z nagłówkami hosta i SNI na powiązania HTTPS i nie otrzymasz odpowiedź i certyfikatu z żądanie przeglądarki ręczne do https://127.0.0.1/ na końcach Wstecz, należy skonfigurować domyślne powiązanie SSL na końcach Wstecz.</span><span class="sxs-lookup"><span data-stu-id="37f66-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="37f66-195">Jeśli nie zrobisz, sondy i zaplecza, nie jest białej.</span><span class="sxs-lookup"><span data-stu-id="37f66-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="37f66-196">Certyfikat w tym kroku należy klucz publiczny certyfikatu pfx na wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="37f66-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="37f66-197">Wyeksportuj certyfikat (nie certyfikatu głównego) zainstalowany na serwerze wewnętrznej bazy danych w. CER formatowania i używać go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="37f66-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="37f66-198">Ten krok whitelists zaplecza bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="37f66-199">Krok 8</span><span class="sxs-lookup"><span data-stu-id="37f66-199">Step 8</span></span>

<span data-ttu-id="37f66-200">Konfiguruj ustawienia http zaplecza bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="37f66-201">Przypisać certyfikat przekazany w poprzednim kroku w ustawieniach protokołu http.</span><span class="sxs-lookup"><span data-stu-id="37f66-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="37f66-202">Krok 9</span><span class="sxs-lookup"><span data-stu-id="37f66-202">Step 9</span></span>

<span data-ttu-id="37f66-203">Utwórz regułę routingu usługi równoważenia obciążenia, który konfiguruje zachowanie usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="37f66-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="37f66-204">W tym przykładzie jest tworzona reguła podstawowe działanie okrężne.</span><span class="sxs-lookup"><span data-stu-id="37f66-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="37f66-205">Krok 10</span><span class="sxs-lookup"><span data-stu-id="37f66-205">Step 10</span></span>

<span data-ttu-id="37f66-206">Skonfiguruj rozmiar wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="37f66-207">Dostępne rozmiary są **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**.</span><span class="sxs-lookup"><span data-stu-id="37f66-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="37f66-208">Pojemność dostępne wartości to 1 do 10.</span><span class="sxs-lookup"><span data-stu-id="37f66-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="37f66-209">Liczba wystąpień 1 można wybrać do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="37f66-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="37f66-210">Jest ważne dowiedzieć się, że dowolnej liczby wystąpień w obszarze dwa wystąpienia nie pasuje do żadnego umowy SLA i dlatego nie zaleca się.</span><span class="sxs-lookup"><span data-stu-id="37f66-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="37f66-211">Mała bramy są używane dla deweloperów testu, a nie do celów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="37f66-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="37f66-212">Krok 11</span><span class="sxs-lookup"><span data-stu-id="37f66-212">Step 11</span></span>

<span data-ttu-id="37f66-213">Skonfiguruj zasady SSL, który ma być używany dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="37f66-214">Brama aplikacji w obsługuje możliwość określenia minimalnej wersji dla wersji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="37f66-215">Listę wersji protokołów, które mogą być definiowane są następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="37f66-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="37f66-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="37f66-216">**TLSv1_0**</span></span>
* <span data-ttu-id="37f66-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="37f66-217">**TLSv1_1**</span></span>
* <span data-ttu-id="37f66-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="37f66-218">**TLSv1_2**</span></span>

<span data-ttu-id="37f66-219">Ustawia wersję protokołu minimalna **TLSv1_2** i umożliwia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** tylko.</span><span class="sxs-lookup"><span data-stu-id="37f66-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="37f66-220">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="37f66-220">Create the Application Gateway</span></span>

<span data-ttu-id="37f66-221">Przy użyciu powyższych kroków, Utwórz bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="37f66-222">Tworzenie bramy jest długo działające procesu.</span><span class="sxs-lookup"><span data-stu-id="37f66-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="37f66-223">Ograniczenia wersji protokołu SSL na istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="37f66-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="37f66-224">Powyższych kroków przejście do tworzenia aplikacji przy użyciu protokołu SSL pełnego i wyłączenie niektórych wersji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="37f66-225">Poniższy przykład powoduje wyłączenie określone zasady SSL na istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="37f66-226">Krok 1</span><span class="sxs-lookup"><span data-stu-id="37f66-226">Step 1</span></span>

<span data-ttu-id="37f66-227">Pobiera bramę aplikacji, aby zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="37f66-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="37f66-228">Krok 2</span><span class="sxs-lookup"><span data-stu-id="37f66-228">Step 2</span></span>

<span data-ttu-id="37f66-229">Definiowanie zasad SSL.</span><span class="sxs-lookup"><span data-stu-id="37f66-229">Define an SSL policy.</span></span> <span data-ttu-id="37f66-230">W poniższym przykładzie TLSv1.0 i TLSv1.1 są wyłączone i mechanizmów szyfrowania **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** są jedynymi osobami, które są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="37f66-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="37f66-231">Krok 3</span><span class="sxs-lookup"><span data-stu-id="37f66-231">Step 3</span></span>

<span data-ttu-id="37f66-232">Na koniec zaktualizuj bramy.</span><span class="sxs-lookup"><span data-stu-id="37f66-232">Finally, update the gateway.</span></span> <span data-ttu-id="37f66-233">Należy pamiętać, że ten ostatni krok jest długo działające zadania.</span><span class="sxs-lookup"><span data-stu-id="37f66-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="37f66-234">Po zakończeniu pełnego SSL jest skonfigurowany na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="37f66-235">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="37f66-235">Get application gateway DNS name</span></span>

<span data-ttu-id="37f66-236">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="37f66-237">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="37f66-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="37f66-238">Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="37f66-239">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f66-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="37f66-240">Aby to zrobić, pobierz szczegóły bramy aplikacji i skojarzony adres IP oraz nazwę DNS, używając elementu PublicIPAddress dołączonego do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="37f66-241">Nazwa DNS bramy aplikacji powinna zostać użyta w celu utworzenia rekordu CNAME, który wskazuje dwóm aplikacjom sieci Web tę nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="37f66-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="37f66-242">Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37f66-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="37f66-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37f66-243">Next steps</span></span>

<span data-ttu-id="37f66-244">Więcej informacji na temat wzmacniania zabezpieczeń aplikacji sieci web z zapory aplikacji sieci Web za pośrednictwem bramy aplikacji, odwiedzając [Omówienie zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="37f66-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
