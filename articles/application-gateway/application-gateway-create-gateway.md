---
title: Tworzenie, uruchamianie i usuwanie bramy aplikacji | Microsoft Docs
description: "Ta strona zawiera instrukcje dotyczące tworzenia, konfigurowania, uruchamiania i usuwania bramy aplikacji na platformie Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: c4932096229b1941e0966e7f3e97de39c6931392
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="4db2d-103">Tworzenie, uruchamianie i usuwanie bramy aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4db2d-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4db2d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4db2d-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="4db2d-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4db2d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="4db2d-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4db2d-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="4db2d-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4db2d-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="4db2d-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4db2d-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="4db2d-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="4db2d-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="4db2d-110">Udostępnia tryb failover, oparty na wydajności routing żądań HTTP między różnymi serwerami — w chmurze i lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="4db2d-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="4db2d-111">Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="4db2d-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="4db2d-112">Aby uzyskać pełną listę obsługiwanych funkcji, odwiedź stronę [Application Gateway — omówienie](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4db2d-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="4db2d-113">W tym artykule przedstawiono kroki umożliwiające tworzenie, konfigurowanie, uruchamianie i usuwanie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4db2d-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4db2d-114">Before you begin</span></span>

1. <span data-ttu-id="4db2d-115">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4db2d-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="4db2d-116">Najnowszą wersję można pobrać i zainstalować z sekcji **Windows PowerShell** strony [Pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4db2d-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4db2d-117">Jeśli masz istniejącą sieć wirtualną, wybierz istniejącą pustą podsieć lub utwórz nową podsieć w istniejącej sieci wirtualnej wyłącznie do użytku przez tę bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="4db2d-118">Nie można wdrożyć bramy aplikacji do innej sieci wirtualnej niż sieć wirtualna zasobów, które zamierzasz wdrożyć za bramą aplikacji, chyba że są używane wirtualne sieci równorzędne.</span><span class="sxs-lookup"><span data-stu-id="4db2d-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="4db2d-119">Aby dowiedzieć się więcej, odwiedź stronę [Wirtualne sieci równorzędne](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4db2d-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="4db2d-120">Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią.</span><span class="sxs-lookup"><span data-stu-id="4db2d-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="4db2d-121">Upewnij się, że z podsieci nie korzystają żadne maszyny wirtualne ani wdrożenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4db2d-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="4db2d-122">Brama aplikacji musi znajdować się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4db2d-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="4db2d-123">Serwery konfigurowane do używania bramy aplikacji muszą być umieszczone w sieci wirtualnej lub z przypisanym adresem IP/VIP lub mieć w niej utworzone punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="4db2d-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="4db2d-124">Co jest wymagane do utworzenia bramy aplikacji?</span><span class="sxs-lookup"><span data-stu-id="4db2d-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="4db2d-125">W momencie użycia polecenia `New-AzureApplicationGateway` w celu utworzenia bramy aplikacji nic nie jest jeszcze skonfigurowane i nowo utworzony zasób musi zostać skonfigurowany przy użyciu kodu XML lub obiektu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="4db2d-126">Potrzebne wartości:</span><span class="sxs-lookup"><span data-stu-id="4db2d-126">The values are:</span></span>

* <span data-ttu-id="4db2d-127">**Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4db2d-128">Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.</span><span class="sxs-lookup"><span data-stu-id="4db2d-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4db2d-129">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="4db2d-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4db2d-130">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="4db2d-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4db2d-131">**Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4db2d-132">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4db2d-133">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="4db2d-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4db2d-134">**Reguła:** reguła wiąże odbiornik z pulą serwerów zaplecza i umożliwia zdefiniowanie, do której puli serwerów zaplecza ma być przekierowywany ruch w przypadku trafienia do określonego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="4db2d-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="4db2d-135">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4db2d-135">Create an application gateway</span></span>

<span data-ttu-id="4db2d-136">Aby utworzyć bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4db2d-136">To create an application gateway:</span></span>

1. <span data-ttu-id="4db2d-137">Utwórz zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="4db2d-138">Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="4db2d-139">Przekaż konfigurację aplikacji do nowo utworzonego zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2d-140">Jeśli musisz skonfigurować niestandardową sondę bramy aplikacji, zobacz artykuł [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md) (Tworzenie bramy aplikacji z sondami niestandardowymi przy użyciu programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4db2d-140">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="4db2d-141">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4db2d-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Przykładowy scenariusz][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="4db2d-143">Tworzenie zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4db2d-143">Create an application gateway resource</span></span>

<span data-ttu-id="4db2d-144">Aby utworzyć bramę, użyj polecenia cmdlet `New-AzureApplicationGateway`, zastępując wartości własnymi.</span><span class="sxs-lookup"><span data-stu-id="4db2d-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="4db2d-145">Opłaty za bramę nie są jeszcze naliczane.</span><span class="sxs-lookup"><span data-stu-id="4db2d-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="4db2d-146">Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="4db2d-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="4db2d-147">W poniższym przykładzie utworzono bramę aplikacji przy użyciu sieci wirtualnej „testvnet1” i podsieci „subnet-1”:</span><span class="sxs-lookup"><span data-stu-id="4db2d-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="4db2d-148">Parametry *Description* (opis), *InstanceCount* (Liczba wystąpień) i *GatewaySize* (Rozmiar bramy) są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="4db2d-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="4db2d-149">Aby sprawdzić, czy brama została utworzona, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4db2d-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="4db2d-150">Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10.</span><span class="sxs-lookup"><span data-stu-id="4db2d-150">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4db2d-151">Wartość domyślna parametru *GatewaySize* to Medium (Średnia).</span><span class="sxs-lookup"><span data-stu-id="4db2d-151">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4db2d-152">Do wyboru są wartości Small (Mała), Medium (Średnia) i Large (Duża).</span><span class="sxs-lookup"><span data-stu-id="4db2d-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="4db2d-153">Parametry *VirtualIPs* (Wirtualne adresy IP) i *DnsName* (Nazwa serwera DNS) są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4db2d-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="4db2d-154">Zostaną utworzone, gdy brama zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="4db2d-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="4db2d-155">Konfigurowanie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4db2d-155">Configure the application gateway</span></span>

<span data-ttu-id="4db2d-156">Bramę aplikacji możesz skonfigurować za pomocą pliku XML lub obiektu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="4db2d-157">Konfigurowanie bramy aplikacji za pomocą pliku XML</span><span class="sxs-lookup"><span data-stu-id="4db2d-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="4db2d-158">W poniższym przykładzie używany jest plik XML, aby skonfigurować wszystkie ustawienia bramy aplikacji i zatwierdzić je w zasobie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="4db2d-159">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4db2d-159">Step 1</span></span>

<span data-ttu-id="4db2d-160">Skopiuj poniższy tekst do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="4db2d-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="4db2d-161">Edytuj zawarte w nawiasach wartości elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="4db2d-162">Zapisz plik z rozszerzeniem .xml.</span><span class="sxs-lookup"><span data-stu-id="4db2d-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4db2d-163">W elemencie Http lub Https jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="4db2d-163">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="4db2d-164">Poniższy przykład przedstawia sposób konfigurowania bramy aplikacji przy użyciu pliku konfiguracyjnego.</span><span class="sxs-lookup"><span data-stu-id="4db2d-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="4db2d-165">W tym przykładzie równoważone jest obciążenie ruchu HTTP na publicznym porcie 80, a ruch sieciowy jest rozsyłany do portu 80 zaplecza między dwoma adresami IP.</span><span class="sxs-lookup"><span data-stu-id="4db2d-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="4db2d-166">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4db2d-166">Step 2</span></span>

<span data-ttu-id="4db2d-167">Następnym etapem jest skonfigurowanie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-167">Next, set the application gateway.</span></span> <span data-ttu-id="4db2d-168">Użyj polecenia cmdlet `Set-AzureApplicationGatewayConfig` z plikiem konfiguracyjnym XML.</span><span class="sxs-lookup"><span data-stu-id="4db2d-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="4db2d-169">Skonfiguruj bramę aplikacji za pomocą obiektu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="4db2d-170">Poniższy przykład przedstawia sposób konfigurowania bramy aplikacji przy użyciu obiektów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="4db2d-171">Wszystkie elementy konfiguracji muszą być skonfigurowane indywidualnie, a następnie dodane do obiektu konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="4db2d-172">Po utworzeniu obiektu konfiguracji użyte zostanie polecenie cmdlet `Set-AzureApplicationGateway`, aby zatwierdzić konfigurację we wcześniej utworzonym zasobie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2d-173">Przed przypisaniem wartości do poszczególnych obiektów konfiguracji trzeba zadeklarować rodzaj obiektu używanego przez program PowerShell jako magazyn.</span><span class="sxs-lookup"><span data-stu-id="4db2d-173">Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="4db2d-174">Pierwszy krok procesu tworzenia elementów polega na zdefiniowaniu elementów `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` do użycia.</span><span class="sxs-lookup"><span data-stu-id="4db2d-174">The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="4db2d-175">Krok 1</span><span class="sxs-lookup"><span data-stu-id="4db2d-175">Step 1</span></span>

<span data-ttu-id="4db2d-176">Utwórz wszystkie poszczególne elementy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4db2d-176">Create all individual configuration items.</span></span>

<span data-ttu-id="4db2d-177">Utwórz adres IP frontonu, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4db2d-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="4db2d-178">Utwórz port frontonu, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4db2d-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="4db2d-179">Utwórz pulę serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-179">Create the back-end server pool.</span></span>

<span data-ttu-id="4db2d-180">Zdefiniuj adresy IP, które zostaną dodane do puli serwerów zaplecza, jak pokazano w następnym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4db2d-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="4db2d-181">Użyj obiektu $server, aby dodać wartości do obiektu puli zaplecza ($pool).</span><span class="sxs-lookup"><span data-stu-id="4db2d-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="4db2d-182">Utwórz ustawienie puli serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="4db2d-183">Utwórz odbiornik.</span><span class="sxs-lookup"><span data-stu-id="4db2d-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="4db2d-184">Utwórz regułę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="4db2d-185">Krok 2</span><span class="sxs-lookup"><span data-stu-id="4db2d-185">Step 2</span></span>

<span data-ttu-id="4db2d-186">Przypisz wszystkie poszczególne elementy konfiguracji do obiektu konfiguracji bramy aplikacji ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="4db2d-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="4db2d-187">Dodaj do konfiguracji adres IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="4db2d-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="4db2d-188">Dodaj do konfiguracji port frontonu.</span><span class="sxs-lookup"><span data-stu-id="4db2d-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="4db2d-189">Dodaj do konfiguracji pulę serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="4db2d-190">Dodaj do konfiguracji ustawienia puli serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4db2d-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="4db2d-191">Dodaj do konfiguracji odbiornik.</span><span class="sxs-lookup"><span data-stu-id="4db2d-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="4db2d-192">Dodaj do konfiguracji regułę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="4db2d-193">Krok 3</span><span class="sxs-lookup"><span data-stu-id="4db2d-193">Step 3</span></span>
<span data-ttu-id="4db2d-194">Przekaż obiekt konfiguracji do zasobu bramy aplikacji za pomocą polecenia cmdlet `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="4db2d-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="4db2d-195">Uruchamianie bramy</span><span class="sxs-lookup"><span data-stu-id="4db2d-195">Start the gateway</span></span>

<span data-ttu-id="4db2d-196">Po skonfigurowaniu bramy użyj polecenia cmdlet `Start-AzureApplicationGateway`, aby uruchomić bramę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="4db2d-197">Naliczanie opłat za bramę aplikacji rozpocznie się po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="4db2d-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2d-198">Wykonanie polecenia cmdlet `Start-AzureApplicationGateway` może zająć do 15–20 minut.</span><span class="sxs-lookup"><span data-stu-id="4db2d-198">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="4db2d-199">Sprawdzanie stanu bramy</span><span class="sxs-lookup"><span data-stu-id="4db2d-199">Verify the gateway status</span></span>

<span data-ttu-id="4db2d-200">Użyj polecenia cmdlet `Get-AzureApplicationGateway`, aby sprawdzić stan bramy.</span><span class="sxs-lookup"><span data-stu-id="4db2d-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="4db2d-201">Jeśli polecenie cmdlet `Start-AzureApplicationGateway` zostało pomyślnie wykonane w poprzednim kroku, atrybut *State* (Stan) powinien mieć wartość Running (Uruchomiono), a atrybuty *Vip* (Wirtualny adres IP) i *DnsName* (Nazwa serwera DNS) powinny zawierać prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="4db2d-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="4db2d-202">W poniższym przykładzie pokazano bramę aplikacji, która jest włączona, działająca i gotowa do przyjmowania ruchu skierowanego na adres `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="4db2d-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="4db2d-203">Usuwanie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4db2d-203">Delete the application gateway</span></span>

<span data-ttu-id="4db2d-204">Aby usunąć bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4db2d-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="4db2d-205">Użyj polecenia cmdlet `Stop-AzureApplicationGateway`, aby zatrzymać bramę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="4db2d-206">Użyj polecenia cmdlet `Remove-AzureApplicationGateway`, aby usunąć bramę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="4db2d-207">Aby sprawdzić, czy brama została usunięta, użyj polecenia cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4db2d-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="4db2d-208">W poniższym przykładzie pierwszy wiersz zawiera polecenie cmdlet `Stop-AzureApplicationGateway`, a kolejne wiersze zawierają dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4db2d-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="4db2d-209">Po zatrzymaniu bramy aplikacji użyj polecenia cmdlet `Remove-AzureApplicationGateway`, aby usunąć usługę.</span><span class="sxs-lookup"><span data-stu-id="4db2d-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="4db2d-210">Aby sprawdzić, czy usługa została usunięta, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4db2d-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="4db2d-211">Ten krok nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="4db2d-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="4db2d-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4db2d-212">Next steps</span></span>

<span data-ttu-id="4db2d-213">Jeśli chcesz skonfigurować odciążanie protokołu SSL, zobacz artykuł [Configure an application gateway for SSL offload](application-gateway-ssl.md) (Konfigurowanie bramy aplikacji na potrzeby odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="4db2d-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="4db2d-214">Jeśli chcesz skonfigurować bramę aplikacji do użycia z wewnętrznym modułem równoważenia obciążenia, zobacz artykuł [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Tworzenie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="4db2d-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4db2d-215">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="4db2d-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4db2d-216">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="4db2d-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4db2d-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4db2d-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
