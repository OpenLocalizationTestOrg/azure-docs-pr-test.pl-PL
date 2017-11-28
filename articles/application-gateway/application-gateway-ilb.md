---
title: "aaaUsing bramy aplikacji Azure z wewnętrznego modułu równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje tooconfigure bramę aplikacji Azure z punktem końcowym wewnętrzny o zrównoważonym obciążeniu"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="2a934-103">Tworzenie Bramy aplikacji z wewnętrznym modułem równoważenia obciążenia (ILB)</span><span class="sxs-lookup"><span data-stu-id="2a934-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a934-104">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a934-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="2a934-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a934-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="2a934-106">Brama aplikacji można skonfigurować internetowy wirtualnego adresu IP lub toohello wewnętrzny punkt końcowy nie widoczne internet, znanej także jako punktu końcowego wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="2a934-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="2a934-107">Konfigurowanie bramy hello z ILB jest przydatne w przypadku toointernet wewnętrznych aplikacji biznesowych — nie są widoczne.</span><span class="sxs-lookup"><span data-stu-id="2a934-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="2a934-108">Jest również przydatne w przypadku warstwy aplikacji wielowarstwowych, który znajduje się w toointernet nie widoczne granic zabezpieczeń, ale nadal wymagają rozkład obciążenia działanie okrężne, lepkości sesji lub kończenia żądań SSL z/usług.</span><span class="sxs-lookup"><span data-stu-id="2a934-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="2a934-109">W tym artykule przedstawiono hello kroki tooconfigure bramę aplikacji z ILB.</span><span class="sxs-lookup"><span data-stu-id="2a934-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a934-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2a934-110">Before you begin</span></span>

1. <span data-ttu-id="2a934-111">Zainstaluj najnowszą wersję hello Azure poleceń cmdlet programu PowerShell przy użyciu hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2a934-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="2a934-112">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [stronę pobierania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2a934-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="2a934-113">Sprawdź, czy sieć wirtualną pracy z prawidłową podsieć.</span><span class="sxs-lookup"><span data-stu-id="2a934-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="2a934-114">Sprawdź, czy masz serwerów wewnętrznej bazy danych w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="2a934-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="2a934-115">toocreate bramę aplikacji, wykonaj następujące kroki w podanej kolejności hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a934-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="2a934-116">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="2a934-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="2a934-117">Konfigurowanie bramy hello</span><span class="sxs-lookup"><span data-stu-id="2a934-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="2a934-118">Konfiguracja bramy hello zestawu</span><span class="sxs-lookup"><span data-stu-id="2a934-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="2a934-119">Uruchom hello bramy</span><span class="sxs-lookup"><span data-stu-id="2a934-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="2a934-120">Sprawdź hello bramy</span><span class="sxs-lookup"><span data-stu-id="2a934-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="2a934-121">Utwórz bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="2a934-121">Create an application gateway:</span></span>

<span data-ttu-id="2a934-122">**Brama hello toocreate**, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="2a934-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="2a934-123">Należy pamiętać, że rozliczeń hello bramy nie jest uruchamiana w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="2a934-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="2a934-124">Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2a934-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="2a934-125">**toovalidate** czy utworzono bramę hello, możesz użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a934-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="2a934-126">W przykładowym hello *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="2a934-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="2a934-127">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="2a934-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="2a934-128">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="2a934-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="2a934-129">Małe i duże są inne dostępne wartości.</span><span class="sxs-lookup"><span data-stu-id="2a934-129">Small and Large are other available values.</span></span> <span data-ttu-id="2a934-130">*VIP* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2a934-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="2a934-131">Są one tworzone po hello brama jest w hello stanu działania.</span><span class="sxs-lookup"><span data-stu-id="2a934-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="2a934-132">Konfigurowanie bramy hello</span><span class="sxs-lookup"><span data-stu-id="2a934-132">Configure hello gateway</span></span>
<span data-ttu-id="2a934-133">Konfiguracja bramy aplikacji składa się z wielu wartości.</span><span class="sxs-lookup"><span data-stu-id="2a934-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="2a934-134">mogą być związane Hello wartości konfiguracji hello tooconstruct razem.</span><span class="sxs-lookup"><span data-stu-id="2a934-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="2a934-135">Witaj wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="2a934-135">hello values are:</span></span>

* <span data-ttu-id="2a934-136">**Pula serwerów wewnętrznej bazy danych:** hello listę adresów IP hello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2a934-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="2a934-137">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieci sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="2a934-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="2a934-138">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="2a934-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="2a934-139">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="2a934-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="2a934-140">**Port serwera sieci Web:** ten port jest port publiczny hello otwarte na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2a934-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="2a934-141">Ruch trafienia tego portu, a następnie pobiera przekierowanego tooone hello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2a934-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="2a934-142">**Odbiornik:** odbiornika hello ma port serwera sieci Web, protokół (Http lub Https, te jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="2a934-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="2a934-143">**Reguła:** reguła hello wiąże odbiornika hello i puli serwerów wewnętrznej bazy danych hello i określa, jaki ruch hello puli serwera wewnętrznej bazy danych ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="2a934-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="2a934-144">Obecnie tylko hello *podstawowe* reguła jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="2a934-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="2a934-145">Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.</span><span class="sxs-lookup"><span data-stu-id="2a934-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="2a934-146">Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub plik XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2a934-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="2a934-147">tooconstruct konfiguracji przy użyciu pliku XML konfiguracji, użyj hello przykładowe poniżej.</span><span class="sxs-lookup"><span data-stu-id="2a934-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="2a934-148">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2a934-148">Note hello following:</span></span>

* <span data-ttu-id="2a934-149">Witaj *konfiguracji IP frontonu* element opisuje hello ILB szczegółowe informacje dotyczące konfigurowania bramy aplikacji przy użyciu ILB.</span><span class="sxs-lookup"><span data-stu-id="2a934-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="2a934-150">Witaj adresu IP frontonu *typu* powinien być ustawiony too'Private "</span><span class="sxs-lookup"><span data-stu-id="2a934-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="2a934-151">Witaj *StaticIPAddress* wewnętrznym adresem IP toohello żądanego na które hello bramy odbiera ruch powinien być ustawiony.</span><span class="sxs-lookup"><span data-stu-id="2a934-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="2a934-152">Należy pamiętać, że hello *StaticIPAddress* element jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2a934-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="2a934-153">Jeśli nie jest dostępny wewnętrzny adres IP z podsieci hello wdrożone zestaw, jest wybierany.</span><span class="sxs-lookup"><span data-stu-id="2a934-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="2a934-154">Witaj wartość hello *nazwa* elementu określonego w parametrze *elementu FrontendIPConfiguration* powinny być używane w hello HTTPListener *FrontendIP* toohello toorefer elementu Konfiguracja IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="2a934-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="2a934-155">**Przykładowy plik XML konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="2a934-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="2a934-156">Konfiguracja bramy hello zestawu</span><span class="sxs-lookup"><span data-stu-id="2a934-156">Set hello gateway configuration</span></span>
<span data-ttu-id="2a934-157">Następnie będzie Ustaw hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2a934-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="2a934-158">Można użyć hello `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2a934-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="2a934-159">Uruchom hello bramy</span><span class="sxs-lookup"><span data-stu-id="2a934-159">Start hello gateway</span></span>

<span data-ttu-id="2a934-160">Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a934-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="2a934-161">Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy.</span><span class="sxs-lookup"><span data-stu-id="2a934-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="2a934-162">Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toocomplete too15 20 minut.</span><span class="sxs-lookup"><span data-stu-id="2a934-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="2a934-163">Sprawdź stan bramy hello</span><span class="sxs-lookup"><span data-stu-id="2a934-163">Verify hello gateway status</span></span>

<span data-ttu-id="2a934-164">Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stanu bramy.</span><span class="sxs-lookup"><span data-stu-id="2a934-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="2a934-165">Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello, powinien mieć stan hello *systemem*, hello Vip i DnsName powinny mieć prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="2a934-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="2a934-166">To przykładowe przedstawiono polecenie cmdlet hello na powitania pierwszy wiersz, następuje hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2a934-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="2a934-167">W tym przykładzie hello bramy działa i jest gotowy tootake ruchu.</span><span class="sxs-lookup"><span data-stu-id="2a934-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="2a934-168">Brama aplikacji Hello jest skonfigurowana tooaccept ruchu na powitania skonfigurowany punkt końcowy ILB 10.0.0.10 w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="2a934-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="2a934-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2a934-169">Next steps</span></span>
<span data-ttu-id="2a934-170">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="2a934-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="2a934-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="2a934-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="2a934-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2a934-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

