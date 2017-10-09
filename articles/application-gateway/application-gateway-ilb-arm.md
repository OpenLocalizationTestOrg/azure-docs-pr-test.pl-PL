---
title: "Brama aplikacji Azure z wewnętrznego modułu równoważenia obciążenia - PowerShell aaaUsing | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfigurować, uruchomić i usunąć bramę aplikacji Azure z wewnętrznego modułu równoważenia obciążenia (ILB) dla usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="4cf74-103">Tworzenie i konfigurowanie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia i usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4cf74-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cf74-104">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cf74-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="4cf74-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cf74-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="4cf74-106">Brama aplikacji w Azure można skonfigurować z adresów VIP połączonych z Internetem lub wewnętrzny punkt końcowy, który nie jest narażonych toohello Internet, znanej także jako punkt końcowy (ILB) usługi równoważenia obciążenia wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4cf74-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="4cf74-107">Konfigurowanie bramy hello z ILB jest przydatne w przypadku wewnętrznych aplikacji — biznesowych, które nie są uwidocznione toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="4cf74-108">Jest również przydatne w przypadku usług i warstwy aplikacji wielowarstwowych, które znajdują się w granicy zabezpieczeń, który nie jest narażonych toohello Internet, ale nadal wymagają okrężnego obciążenia dystrybucji, lepkości sesji lub zakończenie protokołu Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="4cf74-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="4cf74-109">W tym artykule przedstawiono hello kroki tooconfigure bramę aplikacji z ILB.</span><span class="sxs-lookup"><span data-stu-id="4cf74-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4cf74-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4cf74-110">Before you begin</span></span>

1. <span data-ttu-id="4cf74-111">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4cf74-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="4cf74-112">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4cf74-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4cf74-113">Utworzysz sieć wirtualną i podsieć dla usługi Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="4cf74-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="4cf74-114">Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="4cf74-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="4cf74-115">Usługa Application Gateway musi sama znajdować się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cf74-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="4cf74-116">Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="4cf74-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="4cf74-117">Co to jest wymagana toocreate bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="4cf74-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="4cf74-118">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="4cf74-119">Witaj wymienionych na liście adresów IP powinien albo należy toohello sieci wirtualnej, ale w innej podsieci bramy aplikacji hello lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="4cf74-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4cf74-120">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="4cf74-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4cf74-121">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="4cf74-122">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="4cf74-123">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="4cf74-124">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="4cf74-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4cf74-125">**Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="4cf74-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="4cf74-126">Obecnie tylko hello *podstawowe* reguła jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="4cf74-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="4cf74-127">Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.</span><span class="sxs-lookup"><span data-stu-id="4cf74-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="4cf74-128">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cf74-128">Create an application gateway</span></span>

<span data-ttu-id="4cf74-129">Różnica Hello przy użyciu klasycznego Azure i usługi Azure Resource Manager jest hello kolejność, w którym utworzyć bramę aplikacji hello i elementy hello toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="4cf74-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="4cf74-130">Usługa Resource Manager wszystkie elementy bramy aplikacji jest skonfigurowany oddzielnie, a następnie przekaż razem zasobu bramy aplikacji hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4cf74-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="4cf74-131">Poniżej przedstawiono kroki hello, które są potrzebne toocreate bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4cf74-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="4cf74-132">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4cf74-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="4cf74-133">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="4cf74-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="4cf74-134">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cf74-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="4cf74-135">Tworzenie zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cf74-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="4cf74-136">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4cf74-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="4cf74-137">Upewnij się, że przełącznika poleceń cmdlet programu PowerShell tryb toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4cf74-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="4cf74-138">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="4cf74-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="4cf74-139">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4cf74-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="4cf74-140">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4cf74-140">Step 2</span></span>

<span data-ttu-id="4cf74-141">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="4cf74-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4cf74-142">Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4cf74-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="4cf74-143">Krok 3</span><span class="sxs-lookup"><span data-stu-id="4cf74-143">Step 3</span></span>

<span data-ttu-id="4cf74-144">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf74-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="4cf74-145">Krok 4</span><span class="sxs-lookup"><span data-stu-id="4cf74-145">Step 4</span></span>

<span data-ttu-id="4cf74-146">Utwórz nową grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="4cf74-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="4cf74-147">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="4cf74-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4cf74-148">Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="4cf74-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="4cf74-149">Upewnij się, że wszystkie toocreate polecenia używa bramy aplikacji hello same grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4cf74-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="4cf74-150">Przykład poprzedzających hello utworzyliśmy grupę zasobów o nazwie "Zarządcy zasobów appgw" i lokalizacji "zachodnie stany USA".</span><span class="sxs-lookup"><span data-stu-id="4cf74-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="4cf74-151">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="4cf74-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="4cf74-152">powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="4cf74-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="4cf74-153">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4cf74-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="4cf74-154">Ten krok przypisuje hello adres zakresu 10.0.0.0/24 tooa podsieci zmiennej toobe używane toocreate sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cf74-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="4cf74-155">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4cf74-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="4cf74-156">Spowoduje to utworzenie sieci wirtualnej o nazwie "appgwvnet" w zasobów grupy "appgw-zarządcy zasobów" dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="4cf74-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="4cf74-157">Krok 3</span><span class="sxs-lookup"><span data-stu-id="4cf74-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="4cf74-158">Ten krok przypisuje hello podsieci obiektu toovariable $subnet hello dalsze czynności.</span><span class="sxs-lookup"><span data-stu-id="4cf74-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="4cf74-159">Tworzenie obiektu konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cf74-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="4cf74-160">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4cf74-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="4cf74-161">Spowoduje to utworzenie konfiguracji IP bramy dla aplikacji o nazwie "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="4cf74-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="4cf74-162">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="4cf74-163">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="4cf74-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="4cf74-164">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4cf74-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="4cf74-165">Ten krok obejmuje skonfigurowanie hello zaplecza puli adresów IP o nazwie "pool01" z adresem IP, adresy "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="4cf74-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="4cf74-166">Są to adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="4cf74-167">Zastąp hello poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4cf74-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="4cf74-168">Krok 3</span><span class="sxs-lookup"><span data-stu-id="4cf74-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="4cf74-169">Ten krok obejmuje skonfigurowanie ruchu sieciowego bramy ustawienie "poolsetting01" hello obciążenia zrównoważonym aplikacji w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="4cf74-170">Krok 4</span><span class="sxs-lookup"><span data-stu-id="4cf74-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="4cf74-171">Ten krok obejmuje skonfigurowanie hello o nazwie "frontendport01" hello ILB frontonu portów IP.</span><span class="sxs-lookup"><span data-stu-id="4cf74-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="4cf74-172">Krok 5</span><span class="sxs-lookup"><span data-stu-id="4cf74-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="4cf74-173">Ten krok hello frontonu konfiguracji IP o nazwie "fipconfig01" tworzy i kojarzy ją z prywatnego adresu IP z hello bieżącej podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cf74-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="4cf74-174">Krok 6</span><span class="sxs-lookup"><span data-stu-id="4cf74-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="4cf74-175">Ten krok hello odbiornik o nazwie "listener01" tworzy i kojarzy hello portów frontonu toohello frontonu konfiguracji IP.</span><span class="sxs-lookup"><span data-stu-id="4cf74-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="4cf74-176">Krok 7</span><span class="sxs-lookup"><span data-stu-id="4cf74-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="4cf74-177">Spowoduje to utworzenie hello reguły modułu równoważenia obciążenia routingu o nazwie "rule01", który konfiguruje zachowanie usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="4cf74-178">Krok 8</span><span class="sxs-lookup"><span data-stu-id="4cf74-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="4cf74-179">Ten krok obejmuje skonfigurowanie hello rozmiar wystąpienia bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4cf74-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf74-180">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="4cf74-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4cf74-181">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="4cf74-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4cf74-182">Możesz wybrać następujące wartości: Standard_Small, Standard_Medium i Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="4cf74-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="4cf74-183">Tworzenie bramy aplikacji przy użyciu polecenia New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="4cf74-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="4cf74-184">Tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="4cf74-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="4cf74-185">W tym przykładzie bramy aplikacji hello jest nazywany "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="4cf74-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="4cf74-186">Ten krok tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="4cf74-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="4cf74-187">Przykład Witaj bramy aplikacji hello jest nazywany "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="4cf74-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="4cf74-188">Usuwanie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cf74-188">Delete an application gateway</span></span>

<span data-ttu-id="4cf74-189">toodelete bramę aplikacji należy hello toodo następujące kroki w kolejności:</span><span class="sxs-lookup"><span data-stu-id="4cf74-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="4cf74-190">Użyj hello `Stop-AzureRmApplicationGateway` bramy hello toostop polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="4cf74-191">Użyj hello `Remove-AzureRmApplicationGateway` bramy hello tooremove polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="4cf74-192">Sprawdź tej bramy hello został usunięty przy użyciu hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="4cf74-193">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4cf74-193">Step 1</span></span>

<span data-ttu-id="4cf74-194">Pobierz obiekt bramy aplikacji hello i skojarz go tooa zmiennej "$getgw".</span><span class="sxs-lookup"><span data-stu-id="4cf74-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="4cf74-195">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4cf74-195">Step 2</span></span>

<span data-ttu-id="4cf74-196">Użyj `Stop-AzureRmApplicationGateway` bramy aplikacji hello toostop.</span><span class="sxs-lookup"><span data-stu-id="4cf74-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="4cf74-197">W tym przykładzie pokazano hello `Stop-AzureRmApplicationGateway` polecenia cmdlet na powitania pierwszy wiersz, następuje hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4cf74-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="4cf74-198">Po bramy aplikacji hello jest w stanie zatrzymania, użyj hello `Remove-AzureRmApplicationGateway` usługi hello tooremove polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="4cf74-199">Witaj **-force** przełącznika może być używane toosuppress hello Usuń potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="4cf74-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="4cf74-200">tooverify, który hello usługi zostały usunięte, możesz użyć hello `Get-AzureRmApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cf74-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="4cf74-201">Ten krok nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="4cf74-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="4cf74-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4cf74-202">Next steps</span></span>

<span data-ttu-id="4cf74-203">Jeśli tooconfigure odciążanie protokołu SSL, zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="4cf74-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="4cf74-204">Jeśli chcesz tooconfigure toouse bramy aplikacji z ILB, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="4cf74-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4cf74-205">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="4cf74-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4cf74-206">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="4cf74-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4cf74-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4cf74-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

