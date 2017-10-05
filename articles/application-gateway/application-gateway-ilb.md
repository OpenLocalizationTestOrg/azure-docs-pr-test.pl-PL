---
title: "Przy użyciu bramy aplikacji Azure z wewnętrznego modułu równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące konfigurowania bramy aplikacji Azure z punktem końcowym wewnętrzny o zrównoważonym obciążeniu"
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
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="28e06-103">Tworzenie Bramy aplikacji z wewnętrznym modułem równoważenia obciążenia (ILB)</span><span class="sxs-lookup"><span data-stu-id="28e06-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="28e06-104">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="28e06-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="28e06-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="28e06-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="28e06-106">Brama aplikacji można skonfigurować internetowy wirtualnego adresu IP lub wewnętrzny punkt końcowy nie uwidoczniony w Internecie, znanej także jako punktu końcowego wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="28e06-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="28e06-107">Konfigurowanie bramy z ILB jest przydatna do wewnętrznych aplikacji biznesowych — nie są widoczne dla Internetu.</span><span class="sxs-lookup"><span data-stu-id="28e06-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="28e06-108">Jest również przydatne w przypadku warstwy aplikacji wielowarstwowych, który znajduje się w granicy zabezpieczeń nie są widoczne do Internetu, ale nadal wymagają rozkład obciążenia działanie okrężne, lepkości sesji lub kończenia żądań SSL z/usług.</span><span class="sxs-lookup"><span data-stu-id="28e06-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="28e06-109">W tym artykule przeprowadzimy Cię przez proces konfigurowania bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="28e06-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28e06-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="28e06-110">Before you begin</span></span>

1. <span data-ttu-id="28e06-111">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell, za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="28e06-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="28e06-112">Można pobrać i zainstalować najnowszą wersję ze **programu Windows PowerShell** sekcji [stronę pobierania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="28e06-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="28e06-113">Sprawdź, czy sieć wirtualną pracy z prawidłową podsieć.</span><span class="sxs-lookup"><span data-stu-id="28e06-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="28e06-114">Sprawdź, czy masz serwerów wewnętrznej bazy danych w sieci wirtualnej lub z publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="28e06-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="28e06-115">Aby utworzyć bramę aplikacji, wykonaj następujące kroki w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="28e06-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="28e06-116">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="28e06-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="28e06-117">Konfigurowanie bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="28e06-118">Ustaw konfigurację bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="28e06-119">Uruchom bramę</span><span class="sxs-lookup"><span data-stu-id="28e06-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="28e06-120">Sprawdź bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="28e06-121">Utwórz bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="28e06-121">Create an application gateway:</span></span>

<span data-ttu-id="28e06-122">**Aby utworzyć bramę**, użyj `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości własnymi.</span><span class="sxs-lookup"><span data-stu-id="28e06-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="28e06-123">Zauważ, że opłaty za bramę nie są jeszcze naliczane.</span><span class="sxs-lookup"><span data-stu-id="28e06-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="28e06-124">Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="28e06-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

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

<span data-ttu-id="28e06-125">**Aby sprawdzić poprawność** czy utworzono bramę, możesz użyć `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="28e06-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="28e06-126">W przykładzie *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="28e06-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="28e06-127">Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10.</span><span class="sxs-lookup"><span data-stu-id="28e06-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="28e06-128">Wartość domyślna parametru *GatewaySize* to Medium (Średnia).</span><span class="sxs-lookup"><span data-stu-id="28e06-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="28e06-129">Małe i duże są inne dostępne wartości.</span><span class="sxs-lookup"><span data-stu-id="28e06-129">Small and Large are other available values.</span></span> <span data-ttu-id="28e06-130">*VIP* i *DnsName* są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="28e06-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="28e06-131">Zostaną utworzone, gdy brama zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="28e06-131">These are created once the gateway is in the running state.</span></span> 

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

## <a name="configure-the-gateway"></a><span data-ttu-id="28e06-132">Konfigurowanie bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-132">Configure the gateway</span></span>
<span data-ttu-id="28e06-133">Konfiguracja bramy aplikacji składa się z wielu wartości.</span><span class="sxs-lookup"><span data-stu-id="28e06-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="28e06-134">Wartości mogą być powiązane ze sobą w celu utworzenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="28e06-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="28e06-135">Potrzebne wartości:</span><span class="sxs-lookup"><span data-stu-id="28e06-135">The values are:</span></span>

* <span data-ttu-id="28e06-136">**Pula serwerów wewnętrznej bazy danych:** listę adresów IP serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="28e06-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="28e06-137">Na liście adresów IP albo powinna należeć do podsieci sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="28e06-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="28e06-138">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="28e06-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="28e06-139">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="28e06-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="28e06-140">**Port serwera sieci Web:** ten port jest port publiczny otwarte na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28e06-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="28e06-141">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="28e06-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="28e06-142">**Odbiornik:** odbiornika ma port serwera sieci Web, protokół (Http lub Https, te jest rozróżniana wielkość liter) oraz nazwę certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="28e06-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="28e06-143">**Reguła:** reguła wiąże odbiornika i puli serwerów wewnętrznej bazy danych i definiuje puli serwerów wewnętrznej bazy danych, których ruch powinny być kierowane do, gdy trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="28e06-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="28e06-144">Obecnie jest obsługiwana tylko reguła *podstawowa*.</span><span class="sxs-lookup"><span data-stu-id="28e06-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="28e06-145">Reguła *podstawowa* to dystrybucja obciążenia z działaniem okrężnym.</span><span class="sxs-lookup"><span data-stu-id="28e06-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="28e06-146">Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub plik XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="28e06-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="28e06-147">Do utworzenia konfiguracji przy użyciu pliku XML konfiguracji, użyj przykładu poniżej.</span><span class="sxs-lookup"><span data-stu-id="28e06-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="28e06-148">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="28e06-148">Note the following:</span></span>

* <span data-ttu-id="28e06-149">*Konfiguracji IP frontonu* element opisuje zastosowanie w przypadku konfigurowania bramy aplikacji przy użyciu ILB szczegóły ILB.</span><span class="sxs-lookup"><span data-stu-id="28e06-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="28e06-150">Adres IP frontonu *typu* powinien być ustawiony na "Private"</span><span class="sxs-lookup"><span data-stu-id="28e06-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="28e06-151">*StaticIPAddress* powinien być ustawiony na żądaną wewnętrznym adresem IP, na którym Brama odbiera ruch.</span><span class="sxs-lookup"><span data-stu-id="28e06-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="28e06-152">Należy pamiętać, że *StaticIPAddress* element jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e06-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="28e06-153">Jeśli nie jest dostępny wewnętrzny adres IP z podsieci wdrożonej zestaw, jest wybierany.</span><span class="sxs-lookup"><span data-stu-id="28e06-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="28e06-154">Wartość *nazwa* elementu określonego w parametrze *elementu FrontendIPConfiguration* powinny być używane w HTTPListener *FrontendIP* element, aby odwołać się do Konfiguracja IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="28e06-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="28e06-155">**Przykładowy plik XML konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="28e06-155">**Configuration XML sample**</span></span>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="28e06-156">Ustaw konfigurację bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-156">Set the gateway configuration</span></span>
<span data-ttu-id="28e06-157">Następnie będzie Ustaw bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28e06-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="28e06-158">Można użyć `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="28e06-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-the-gateway"></a><span data-ttu-id="28e06-159">Uruchamianie bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-159">Start the gateway</span></span>

<span data-ttu-id="28e06-160">Po skonfigurowaniu bramy użyj polecenia cmdlet `Start-AzureApplicationGateway`, aby uruchomić bramę.</span><span class="sxs-lookup"><span data-stu-id="28e06-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="28e06-161">Naliczanie opłat za bramę aplikacji rozpocznie się po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="28e06-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="28e06-162">`Start-AzureApplicationGateway` Polecenie cmdlet może potrwać do 15-20 minut.</span><span class="sxs-lookup"><span data-stu-id="28e06-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
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

## <a name="verify-the-gateway-status"></a><span data-ttu-id="28e06-163">Sprawdzanie stanu bramy</span><span class="sxs-lookup"><span data-stu-id="28e06-163">Verify the gateway status</span></span>

<span data-ttu-id="28e06-164">Użyj `Get-AzureApplicationGateway` polecenia cmdlet, aby sprawdzić stan bramy.</span><span class="sxs-lookup"><span data-stu-id="28e06-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="28e06-165">Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku, powinien mieć stan *systemem*, i Vip oraz DnsName powinny mieć prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="28e06-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="28e06-166">Przykład obejmuje polecenia cmdlet w pierwszym wierszu, to po danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="28e06-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="28e06-167">W tym przykładzie brama jest uruchomiona i jest gotowa do sporządzenia ruchu.</span><span class="sxs-lookup"><span data-stu-id="28e06-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="28e06-168">Brama aplikacji jest skonfigurowana do akceptowania ruchu w skonfigurowanym punkcie końcowym ILB 10.0.0.10 w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="28e06-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="28e06-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28e06-169">Next steps</span></span>
<span data-ttu-id="28e06-170">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="28e06-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="28e06-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="28e06-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="28e06-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="28e06-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

