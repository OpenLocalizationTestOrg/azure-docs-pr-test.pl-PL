---
title: "aaaCreate, uruchomić lub usunąć bramę aplikacji | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfigurować, uruchomić i usunąć bramę aplikacji Azure"
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
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="bd040-103">Tworzenie, uruchamianie i usuwanie bramy aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd040-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd040-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd040-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="bd040-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd040-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="bd040-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd040-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="bd040-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd040-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="bd040-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bd040-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="bd040-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="bd040-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="bd040-110">Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="bd040-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="bd040-111">Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="bd040-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="bd040-112">odwiedź toofind pełną listę obsługiwanych funkcji [omówienie bramy aplikacji](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bd040-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="bd040-113">W tym artykule przedstawiono toocreate kroki hello, skonfiguruj start i usunąć bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd040-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="bd040-114">Before you begin</span></span>

1. <span data-ttu-id="bd040-115">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bd040-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="bd040-116">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bd040-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="bd040-117">Jeśli masz istniejącą sieć wirtualną, wybierz istniejącą podsieć pusty albo utwórz nową podsieć w istniejącej sieci wirtualnej wyłącznie do użytku przez bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="bd040-118">Nie można wdrożyć hello aplikacji bramy tooa innej sieci wirtualnej niż hello zasobów ma toodeploy za bramy aplikacji hello chyba że używana jest sieć wirtualną komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="bd040-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="bd040-119">toolearn więcej odwiedź [równorzędna sieci wirtualnej](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd040-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="bd040-120">Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią.</span><span class="sxs-lookup"><span data-stu-id="bd040-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="bd040-121">Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="bd040-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="bd040-122">Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd040-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="bd040-123">Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="bd040-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="bd040-124">Co to jest wymagana toocreate bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="bd040-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="bd040-125">Jeśli używasz hello `New-AzureApplicationGateway` bramy aplikacji hello toocreate polecenia, konfiguracja nie jest ustawiona na tym etapie i hello nowo utworzony zasób są skonfigurowane przy użyciu XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="bd040-126">Witaj wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="bd040-126">hello values are:</span></span>

* <span data-ttu-id="bd040-127">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="bd040-128">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="bd040-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="bd040-129">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="bd040-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="bd040-130">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="bd040-131">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="bd040-132">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="bd040-133">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="bd040-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="bd040-134">**Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="bd040-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="bd040-135">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd040-135">Create an application gateway</span></span>

<span data-ttu-id="bd040-136">toocreate bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="bd040-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="bd040-137">Utwórz zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="bd040-138">Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="bd040-139">Zatwierdź toohello konfiguracji hello nowo utworzony zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="bd040-140">Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bd040-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="bd040-141">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd040-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Przykładowy scenariusz][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="bd040-143">Tworzenie zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd040-143">Create an application gateway resource</span></span>

<span data-ttu-id="bd040-144">toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="bd040-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="bd040-145">Karta hello bramy nie rozpoczyna się w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="bd040-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="bd040-146">Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="bd040-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="bd040-147">Witaj poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej o nazwie "testvnet1" i podsieć o nazwie "podsieć 1":</span><span class="sxs-lookup"><span data-stu-id="bd040-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="bd040-148">Parametry *Description* (opis), *InstanceCount* (Liczba wystąpień) i *GatewaySize* (Rozmiar bramy) są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="bd040-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="bd040-149">toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

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
> <span data-ttu-id="bd040-150">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="bd040-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="bd040-151">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="bd040-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="bd040-152">Do wyboru są wartości Small (Mała), Medium (Średnia) i Large (Duża).</span><span class="sxs-lookup"><span data-stu-id="bd040-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="bd040-153">*VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="bd040-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="bd040-154">Są one tworzone po hello brama jest w hello stanu działania.</span><span class="sxs-lookup"><span data-stu-id="bd040-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="bd040-155">Brama aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bd040-155">Configure hello application gateway</span></span>

<span data-ttu-id="bd040-156">Brama aplikacji hello można skonfigurować za pomocą XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="bd040-157">Konfigurowanie bramy aplikacji hello za pomocą XML</span><span class="sxs-lookup"><span data-stu-id="bd040-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="bd040-158">W hello poniższy przykład użyj tooconfigure pliku XML wszystkie ustawienia bramy aplikacji i je zatwierdzić zasobu bramy toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="bd040-159">Krok 1</span><span class="sxs-lookup"><span data-stu-id="bd040-159">Step 1</span></span>

<span data-ttu-id="bd040-160">Skopiuj powitania po tooNotepad tekstu.</span><span class="sxs-lookup"><span data-stu-id="bd040-160">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="bd040-161">Edytuj wartości hello między nawiasami hello hello elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="bd040-162">Zapisz plik hello z rozszerzeniem .xml.</span><span class="sxs-lookup"><span data-stu-id="bd040-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd040-163">Element protokołu Hello Http lub Https jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bd040-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="bd040-164">Witaj poniższy przykład pokazuje, jak toouse konfiguracji pliku tooset się bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="bd040-165">obciążenia przykład Hello równoważy ruchu HTTP na port publiczny 80 i wysyła ruch sieciowy tooback-end port 80 między dwoma adresami IP.</span><span class="sxs-lookup"><span data-stu-id="bd040-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

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

#### <a name="step-2"></a><span data-ttu-id="bd040-166">Krok 2</span><span class="sxs-lookup"><span data-stu-id="bd040-166">Step 2</span></span>

<span data-ttu-id="bd040-167">Następnie ustaw hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-167">Next, set hello application gateway.</span></span> <span data-ttu-id="bd040-168">Użyj hello `Set-AzureApplicationGatewayConfig` polecenie cmdlet z pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="bd040-169">Konfigurowanie bramy aplikacji hello za pomocą obiektu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bd040-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="bd040-170">Witaj poniższy przykład pokazuje, jak tooconfigure hello bramy aplikacji przy użyciu obiektów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="bd040-171">Wszystkie elementy konfiguracji należy skonfigurować osobno i następnie dodany obiekt konfiguracji bramy aplikacji tooan.</span><span class="sxs-lookup"><span data-stu-id="bd040-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="bd040-172">Po utworzeniu obiektu konfiguracji hello używasz hello `Set-AzureApplicationGateway` polecenia toocommit hello konfiguracji toohello wcześniej utworzony zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd040-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="bd040-173">Przed przypisaniem obiekt konfiguracji tooeach wartości, należy toodeclare obiektem jakiego rodzaju PowerShell korzysta z magazynu.</span><span class="sxs-lookup"><span data-stu-id="bd040-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="bd040-174">Witaj pierwszego wiersza toocreate hello poszczególne elementy definiuje, jakie `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` są używane.</span><span class="sxs-lookup"><span data-stu-id="bd040-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="bd040-175">Krok 1</span><span class="sxs-lookup"><span data-stu-id="bd040-175">Step 1</span></span>

<span data-ttu-id="bd040-176">Utwórz wszystkie poszczególne elementy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-176">Create all individual configuration items.</span></span>

<span data-ttu-id="bd040-177">Utwórz hello IP frontonu, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="bd040-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="bd040-178">Utworzyć hello portów frontonu, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="bd040-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="bd040-179">Utwórz hello puli serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bd040-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="bd040-180">Zdefiniuj hello adresów IP, które są dodawane do puli serwerów zaplecza toohello, jak pokazano w następnym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="bd040-181">Użyj hello $server tooadd hello wartości toohello puli zaplecza dla obiektu ($pool).</span><span class="sxs-lookup"><span data-stu-id="bd040-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="bd040-182">Utwórz ustawienie puli serwera zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="bd040-183">Utwórz odbiornik hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="bd040-184">Utwórz regułę hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="bd040-185">Krok 2</span><span class="sxs-lookup"><span data-stu-id="bd040-185">Step 2</span></span>

<span data-ttu-id="bd040-186">Przypisz wszystkich konfiguracji poszczególnych elementów tooan aplikacji konfiguracji obiektu bramy ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="bd040-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="bd040-187">Dodaj hello konfiguracji IP frontonu w toohello.</span><span class="sxs-lookup"><span data-stu-id="bd040-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="bd040-188">Dodaj konfigurację toohello portów frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="bd040-189">Dodaj powitania serwera zaplecza puli toohello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd040-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="bd040-190">Dodawanie konfiguracji toohello hello puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bd040-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="bd040-191">Dodaj konfigurację toohello odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="bd040-192">Dodaj konfigurację toohello reguły hello.</span><span class="sxs-lookup"><span data-stu-id="bd040-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="bd040-193">Krok 3</span><span class="sxs-lookup"><span data-stu-id="bd040-193">Step 3</span></span>
<span data-ttu-id="bd040-194">Zatwierdź zasobu bramy aplikacji hello konfiguracji obiektu toohello przy użyciu `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="bd040-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="bd040-195">Uruchom hello bramy</span><span class="sxs-lookup"><span data-stu-id="bd040-195">Start hello gateway</span></span>

<span data-ttu-id="bd040-196">Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="bd040-197">Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy.</span><span class="sxs-lookup"><span data-stu-id="bd040-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="bd040-198">Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toofinish too15 20 minut.</span><span class="sxs-lookup"><span data-stu-id="bd040-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="bd040-199">Sprawdź stan bramy hello</span><span class="sxs-lookup"><span data-stu-id="bd040-199">Verify hello gateway status</span></span>

<span data-ttu-id="bd040-200">Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stan hello bramy.</span><span class="sxs-lookup"><span data-stu-id="bd040-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="bd040-201">Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello *stanu* powinna być uruchomiona, i *Vip* i *DnsName* powinny mieć prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="bd040-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="bd040-202">Witaj poniższy przykład przedstawia bramę aplikacji, która jest włączone, uaktywnione i gotowe tootake ruchu przeznaczony dla `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="bd040-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="bd040-203">Usuń bramę aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bd040-203">Delete hello application gateway</span></span>

<span data-ttu-id="bd040-204">Brama aplikacji hello toodelete:</span><span class="sxs-lookup"><span data-stu-id="bd040-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="bd040-205">Użyj hello `Stop-AzureApplicationGateway` bramy hello toostop polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="bd040-206">Użyj hello `Remove-AzureApplicationGateway` bramy hello tooremove polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="bd040-207">Sprawdź tej bramy hello został usunięty przy użyciu hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="bd040-208">Witaj poniższy przykład przedstawia hello `Stop-AzureApplicationGateway` polecenia cmdlet na powitania pierwszy wiersz, następuje hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bd040-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="bd040-209">Po bramy aplikacji hello jest w stanie zatrzymania, użyj hello `Remove-AzureApplicationGateway` usługi hello tooremove polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

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

<span data-ttu-id="bd040-210">tooverify, który hello usługi zostały usunięte, możesz użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd040-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="bd040-211">Ten krok nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="bd040-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="bd040-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd040-212">Next steps</span></span>

<span data-ttu-id="bd040-213">Jeśli tooconfigure odciążanie protokołu SSL, zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="bd040-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="bd040-214">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="bd040-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="bd040-215">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="bd040-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="bd040-216">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="bd040-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="bd040-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="bd040-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
