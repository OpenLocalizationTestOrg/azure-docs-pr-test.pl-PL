---
title: "aaaConfigure zakończenia tooend SSL z bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure kończyć tooend SSL z bramy aplikacji przy użyciu programu PowerShell usługi Azure Resource Manager"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="1967d-103">Skonfiguruj tooend końcowych SSL z bramy aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1967d-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="1967d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1967d-104">Overview</span></span>

<span data-ttu-id="1967d-105">Aplikacja obsługuje bramy końcowy tooend szyfrowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="1967d-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="1967d-106">Brama aplikacji w następującym cechom zakończenie połączenia SSL hello na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="1967d-107">Witaj bramy następnie stosuje hello reguły routingu ruchu toohello ponownie szyfruje pakietów hello i przekazuje hello pakietów toohello odpowiedniej wewnętrznej bazy danych na podstawie reguł routingu hello zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="1967d-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="1967d-108">Odpowiedzi z serwera sieci web hello przechodzi przez hello tego samego procesu wstecz toohello użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="1967d-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="1967d-109">Inna funkcja tej bramy aplikacji obsługuje Określanie niestandardowych opcji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="1967d-110">Brama aplikacji umożliwia wyłączenie powitania po wersji protokołu; **TLSv1.0**, **TLSv1.1**, i **TLSv1.2** również definiowanie hello, który szyfrowania mechanizmy toouse i hello według priorytetu.</span><span class="sxs-lookup"><span data-stu-id="1967d-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="1967d-111">toolearn więcej informacji na temat opcji SSL można skonfigurować, odwiedź stronę [Przegląd zasad SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1967d-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1967d-112">Protokół SSL 2.0 i 3.0 protokołu SSL są domyślnie wyłączone i nie można włączyć.</span><span class="sxs-lookup"><span data-stu-id="1967d-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="1967d-113">One są uważane za niebezpieczne i nie są toobe można używać z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![Scenariusz obrazu][scenario]

## <a name="scenario"></a><span data-ttu-id="1967d-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="1967d-115">Scenario</span></span>

<span data-ttu-id="1967d-116">W tym scenariuszu dowiesz się, jak bramy aplikacji przy użyciu toocreate kończyć tooend SSL przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1967d-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="1967d-117">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="1967d-117">This scenario will:</span></span>

* <span data-ttu-id="1967d-118">Utwórz grupę zasobów o nazwie **zarządcy zasobów appgw**</span><span class="sxs-lookup"><span data-stu-id="1967d-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="1967d-119">Tworzenie sieci wirtualnej o nazwie **appgwvnet** z 10.0.0.0/16 przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="1967d-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="1967d-120">Utwórz dwie podsieci o nazwie **appgwsubnet** i **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="1967d-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="1967d-121">Tworzenie aplikacji małych bramy obsługi zakończenia tooend szyfrowania SSL tej wersji protokołów SSL limity i mechanizmów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1967d-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1967d-122">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1967d-122">Before you begin</span></span>

<span data-ttu-id="1967d-123">tooconfigure zakończenia tooend SSL z bramy aplikacji, certyfikat jest wymagany dla bramy hello i certyfikaty są wymagane do hello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1967d-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="1967d-124">certyfikat bramy Hello jest używany tooencrypt i odszyfrowywania hello ruch wysyłany tooit przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="1967d-125">certyfikat bramy Hello musi toobe Format Wymiana informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="1967d-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="1967d-126">Tego formatu pliku umożliwia dla hello prywatnego klucza toobe wyeksportowane wymaganych przez hello aplikacji bramy tooperform hello szyfrowania i odszyfrowywania ruchu.</span><span class="sxs-lookup"><span data-stu-id="1967d-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="1967d-127">W celu tooend protokołu SSL szyfrowania hello wewnętrznej bazy danych musi być białej z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="1967d-128">Jest to realizowane przez przekazywanie certyfikatu publicznego hello hello zapleczy toohello aplikacji bramy.</span><span class="sxs-lookup"><span data-stu-id="1967d-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="1967d-129">Dzięki temu tej bramy aplikacji hello komunikuje się tylko z wystąpieniami znane wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1967d-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="1967d-130">To dodatkowe zabezpiecza komunikację tooend hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="1967d-131">Ten proces został opisany w hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1967d-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="1967d-132">Utwórz hello grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="1967d-132">Create hello Resource Group</span></span>

<span data-ttu-id="1967d-133">Ta sekcja przeprowadzi Cię przez proces tworzenia grupy zasobów, zawierającą hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="1967d-134">Krok 1</span><span class="sxs-lookup"><span data-stu-id="1967d-134">Step 1</span></span>

<span data-ttu-id="1967d-135">Zaloguj się za tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1967d-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="1967d-136">Krok 2</span><span class="sxs-lookup"><span data-stu-id="1967d-136">Step 2</span></span>

<span data-ttu-id="1967d-137">Wybierz hello toouse subskrypcji dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="1967d-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="1967d-138">Krok 3</span><span class="sxs-lookup"><span data-stu-id="1967d-138">Step 3</span></span>

<span data-ttu-id="1967d-139">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="1967d-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="1967d-140">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1967d-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="1967d-141">Witaj poniższy przykład tworzy sieć wirtualną z dwoma podsieciami.</span><span class="sxs-lookup"><span data-stu-id="1967d-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="1967d-142">Podsieć jest bramy aplikacji hello toohold używane.</span><span class="sxs-lookup"><span data-stu-id="1967d-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="1967d-143">Witaj innych podsieci jest używana dla aplikacji sieci web hello hostingu zapleczy hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="1967d-144">Krok 1</span><span class="sxs-lookup"><span data-stu-id="1967d-144">Step 1</span></span>

<span data-ttu-id="1967d-145">Przypisz zakres adresów dla podsieci hello można użyć dla hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="1967d-146">Podsieci skonfigurowane dla bramy aplikacji należy ustalać poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1967d-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="1967d-147">Brama aplikacji można skonfigurować dla się too10 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="1967d-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="1967d-148">Każde wystąpienie ma jeden adres IP z podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="1967d-149">Zbyt małe podsieci może niekorzystnie wpłynąć na skalowanie w poziomie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="1967d-150">Krok 2</span><span class="sxs-lookup"><span data-stu-id="1967d-150">Step 2</span></span>

<span data-ttu-id="1967d-151">Przypisz adres toobe zakres używany do hello puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1967d-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="1967d-152">Krok 3</span><span class="sxs-lookup"><span data-stu-id="1967d-152">Step 3</span></span>

<span data-ttu-id="1967d-153">Tworzenie sieci wirtualnej z podsieciami hello zdefiniowany w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="1967d-154">Krok 4</span><span class="sxs-lookup"><span data-stu-id="1967d-154">Step 4</span></span>

<span data-ttu-id="1967d-155">Pobrać hello sieci wirtualnej zasobów i podsieć zasobów toobe używane w hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1967d-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="1967d-156">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="1967d-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="1967d-157">Utwórz publiczny toobe zasobów adresu IP, używana przez bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="1967d-158">Ten publiczny adres IP jest używany następujący krok.</span><span class="sxs-lookup"><span data-stu-id="1967d-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="1967d-159">Brama aplikacji nie obsługuje użycia hello utworzony ze zdefiniowaną etykietą domeny publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="1967d-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="1967d-160">Obsługiwane jest tylko publiczny adres IP z etykietą utworzony dynamicznie domeny.</span><span class="sxs-lookup"><span data-stu-id="1967d-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="1967d-161">Jeśli potrzebujesz nazwy dns przyjazną dla bramy aplikacji hello, zaleca się zarejestrować toouse rekordu CNAME jako alias.</span><span class="sxs-lookup"><span data-stu-id="1967d-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="1967d-162">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1967d-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="1967d-163">Wszystkie elementy konfiguracji są ustawiane przed utworzeniem bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="1967d-164">Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="1967d-165">Krok 1</span><span class="sxs-lookup"><span data-stu-id="1967d-165">Step 1</span></span>

<span data-ttu-id="1967d-166">Utwórz konfigurację IP bramy aplikacji, to ustawienie określa, jakie podsieci hello aplikacja używa bramy.</span><span class="sxs-lookup"><span data-stu-id="1967d-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="1967d-167">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i kieruje adresy IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="1967d-168">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="1967d-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="1967d-169">Krok 2</span><span class="sxs-lookup"><span data-stu-id="1967d-169">Step 2</span></span>

<span data-ttu-id="1967d-170">Tworzenie konfiguracji IP frontonu, to ustawienie mapuje ip prywatny lub publiczny adres toohello frontonu bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="1967d-171">powitania po kroku kojarzy hello publicznego adresu IP w hello poprzedzających krok konfiguracji IP frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="1967d-172">Krok 3</span><span class="sxs-lookup"><span data-stu-id="1967d-172">Step 3</span></span>

<span data-ttu-id="1967d-173">Skonfiguruj pulę adresów IP zaplecza hello hello adresy IP serwerów sieci web zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="1967d-174">Te adresy IP są adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="1967d-175">Zastąp powitania po tooadd adresy IP własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="1967d-176">W pełni kwalifikowaną nazwą domeny (FQDN) jest również prawidłową wartość zamiast adresu ip dla serwerów zaplecza hello za pomocą przełącznika - BackendFqdns hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="1967d-177">Krok 4</span><span class="sxs-lookup"><span data-stu-id="1967d-177">Step 4</span></span>

<span data-ttu-id="1967d-178">Skonfiguruj hello frontonu portu IP dla punktu końcowego hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="1967d-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="1967d-179">Jest to port hello użytkownicy połączenie.</span><span class="sxs-lookup"><span data-stu-id="1967d-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="1967d-180">Krok 5</span><span class="sxs-lookup"><span data-stu-id="1967d-180">Step 5</span></span>

<span data-ttu-id="1967d-181">Konfigurowanie certyfikatu hello hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="1967d-182">Ten certyfikat jest używany toodecrypt i Szyfruj ponownie ruch hello na bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="1967d-183">Ten przykład konfiguruje hello certyfikatu używanego na potrzeby połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="1967d-184">certyfikat Hello musi toobe w formacie pfx, a hello hasło musi zawierać od 4 znaki too12.</span><span class="sxs-lookup"><span data-stu-id="1967d-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="1967d-185">Krok 6</span><span class="sxs-lookup"><span data-stu-id="1967d-185">Step 6</span></span>

<span data-ttu-id="1967d-186">Utwórz odbiornik HTTP hello hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="1967d-187">Przypisz hello konfiguracji ip frontonu, port i toouse certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="1967d-188">Krok 7</span><span class="sxs-lookup"><span data-stu-id="1967d-188">Step 7</span></span>

<span data-ttu-id="1967d-189">Przekaż certyfikat hello z obsługą toobe używane na powitania SSL zasobów puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1967d-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="1967d-190">Witaj domyślnego badania pobiera hello klucza publicznego z hello **domyślne** powiązanie SSL na powitania zaplecza na adres IP i porównuje hello wartość klucza publicznego odbiera wartość klucza z publicznego toohello podanych tutaj.</span><span class="sxs-lookup"><span data-stu-id="1967d-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="1967d-191">Witaj pobrany publiczny klucz może nie koniecznie hello przeznaczone lokacji toowhich ruch **Jeśli** korzystasz z nagłówkami hosta i SNI na powitania zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1967d-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="1967d-192">W razie wątpliwości, odwiedź stronę https://127.0.0.1/ na powitania zapleczy tooconfirm certyfikat, który jest używany dla hello **domyślne** powiązania SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="1967d-193">W tej sekcji służą hello klucza publicznego z tym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="1967d-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="1967d-194">Jeśli korzystasz z nagłówkami hosta i SNI na powiązania HTTPS i z toohttps://127.0.0.1/ żądania ręczne przeglądarki na powitania zapleczy nie otrzymasz odpowiedź i certyfikatów, należy skonfigurować domyślne powiązanie SSL na powitania zapleczy.</span><span class="sxs-lookup"><span data-stu-id="1967d-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="1967d-195">Jeśli nie zrobisz, sondy i zaplecza hello nie jest białej.</span><span class="sxs-lookup"><span data-stu-id="1967d-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="1967d-196">certyfikat Hello opisane w tym kroku należy hello klucz publiczny certyfikatu pfx hello na powitania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1967d-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="1967d-197">Wyeksportuj certyfikat hello (nie hello certyfikatu głównego) zainstalowany na serwerze wewnętrznej bazy danych hello w. CER formatowania i używać go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="1967d-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="1967d-198">Ten krok whitelists hello zaplecza bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="1967d-199">Krok 8</span><span class="sxs-lookup"><span data-stu-id="1967d-199">Step 8</span></span>

<span data-ttu-id="1967d-200">Konfiguruj ustawienia http zaplecza bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="1967d-201">Przypisz certyfikat hello przekazany w hello poprzedzających krok toohello http ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1967d-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="1967d-202">Krok 9</span><span class="sxs-lookup"><span data-stu-id="1967d-202">Step 9</span></span>

<span data-ttu-id="1967d-203">Utwórz regułę routingu usługi równoważenia obciążenia, który konfiguruje zachowanie usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="1967d-204">W tym przykładzie jest tworzona reguła podstawowe działanie okrężne.</span><span class="sxs-lookup"><span data-stu-id="1967d-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="1967d-205">Krok 10</span><span class="sxs-lookup"><span data-stu-id="1967d-205">Step 10</span></span>

<span data-ttu-id="1967d-206">Skonfiguruj rozmiar wystąpienia hello hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="1967d-207">są dostępne rozmiary Hello **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**.</span><span class="sxs-lookup"><span data-stu-id="1967d-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="1967d-208">Pojemności, hello dostępne wartości to 1 do 10.</span><span class="sxs-lookup"><span data-stu-id="1967d-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="1967d-209">Liczba wystąpień 1 można wybrać do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="1967d-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="1967d-210">Ważne jest tooknow, że wszystkie wystąpienia liczba wystąpień w dwóch nie pasuje do żadnego hello umowy dotyczącej poziomu usług i dlatego nie zaleca się.</span><span class="sxs-lookup"><span data-stu-id="1967d-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="1967d-211">Mała bramy są toobe używane dla deweloperów testu, a nie do celów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1967d-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="1967d-212">Krok 11</span><span class="sxs-lookup"><span data-stu-id="1967d-212">Step 11</span></span>

<span data-ttu-id="1967d-213">Skonfiguruj toobe zasad SSL hello używane na powitania Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="1967d-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="1967d-214">Brama aplikacji w obsługuje hello możliwości tooset minimalnej wersji dla wersji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="1967d-215">Hello są następujące wartości listy wersji protokołów, które mogą zostać zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="1967d-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="1967d-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="1967d-216">**TLSv1_0**</span></span>
* <span data-ttu-id="1967d-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="1967d-217">**TLSv1_1**</span></span>
* <span data-ttu-id="1967d-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="1967d-218">**TLSv1_2**</span></span>

<span data-ttu-id="1967d-219">Ustawia hello wersji protocol minimalne zbyt**TLSv1_2** i umożliwia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**i **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** tylko.</span><span class="sxs-lookup"><span data-stu-id="1967d-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="1967d-220">Utwórz hello bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1967d-220">Create hello Application Gateway</span></span>

<span data-ttu-id="1967d-221">Za pomocą hello wszystkich poprzednich krokach, Utwórz hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="1967d-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="1967d-222">Tworzenie Hello bramy hello jest długo działające procesu.</span><span class="sxs-lookup"><span data-stu-id="1967d-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="1967d-223">Ograniczenia wersji protokołu SSL na istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="1967d-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="1967d-224">Witaj powyższych kroków przejście przez tworzenie aplikacji z tooend końcowych SSL i wyłączanie niektórych wersji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="1967d-225">Witaj poniższy przykład powoduje wyłączenie określone zasady SSL na istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="1967d-226">Krok 1</span><span class="sxs-lookup"><span data-stu-id="1967d-226">Step 1</span></span>

<span data-ttu-id="1967d-227">Pobrać tooupdate bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="1967d-228">Krok 2</span><span class="sxs-lookup"><span data-stu-id="1967d-228">Step 2</span></span>

<span data-ttu-id="1967d-229">Definiowanie zasad SSL.</span><span class="sxs-lookup"><span data-stu-id="1967d-229">Define an SSL policy.</span></span> <span data-ttu-id="1967d-230">W hello poniższy przykład, TLSv1.0 i TLSv1.1 są wyłączone i hello mechanizmów szyfrowania **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** są jedynymi osobami dozwolone hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="1967d-231">Krok 3</span><span class="sxs-lookup"><span data-stu-id="1967d-231">Step 3</span></span>

<span data-ttu-id="1967d-232">Na koniec zaktualizuj hello bramy.</span><span class="sxs-lookup"><span data-stu-id="1967d-232">Finally, update hello gateway.</span></span> <span data-ttu-id="1967d-233">Jest ważne toonote, że ten ostatni krok jest długo działające zadania.</span><span class="sxs-lookup"><span data-stu-id="1967d-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="1967d-234">Po zakończeniu tooend końcowych SSL jest skonfigurowany dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="1967d-235">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1967d-235">Get application gateway DNS name</span></span>

<span data-ttu-id="1967d-236">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="1967d-237">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="1967d-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="1967d-238">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1967d-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="1967d-239">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1967d-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="1967d-240">toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="1967d-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="1967d-241">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="1967d-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="1967d-242">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1967d-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1967d-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1967d-243">Next steps</span></span>

<span data-ttu-id="1967d-244">Więcej informacji na temat wzmacniania zabezpieczeń hello aplikacji sieci web z zapory aplikacji sieci Web za pośrednictwem bramy aplikacji, odwiedzając [Omówienie zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1967d-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
