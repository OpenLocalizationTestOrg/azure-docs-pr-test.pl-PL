---
title: "aaaCreate niestandardowych sondowania — brama usługi aplikacji Azure — klasyczny programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate niestandardowego sondowania bramy aplikacji przy użyciu programu PowerShell w hello klasycznego modelu wdrażania"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="66f9e-103">Tworzenie niestandardowych sondowania bramy aplikacji Azure (klasyczne) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="66f9e-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="66f9e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="66f9e-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="66f9e-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="66f9e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="66f9e-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="66f9e-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="66f9e-107">W tym artykule możesz dodać niestandardowe sondowania tooan istniejących aplikacji bramy przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66f9e-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="66f9e-108">Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na powitania domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="66f9e-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66f9e-109">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66f9e-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66f9e-110">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="66f9e-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="66f9e-111">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="66f9e-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="66f9e-112">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66f9e-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="66f9e-113">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="66f9e-113">Create an application gateway</span></span>

<span data-ttu-id="66f9e-114">toocreate bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="66f9e-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="66f9e-115">Utwórz zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="66f9e-116">Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="66f9e-117">Zatwierdź toohello konfiguracji hello nowo utworzony zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="66f9e-118">Utwórz zasób bramy aplikacji z niestandardowego badania</span><span class="sxs-lookup"><span data-stu-id="66f9e-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="66f9e-119">toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="66f9e-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="66f9e-120">Karta hello bramy nie rozpoczyna się w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="66f9e-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="66f9e-121">Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="66f9e-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="66f9e-122">Witaj poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej o nazwie "testvnet1" i podsieć o nazwie "podsieć 1".</span><span class="sxs-lookup"><span data-stu-id="66f9e-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="66f9e-123">toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66f9e-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="66f9e-124">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="66f9e-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="66f9e-125">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="66f9e-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="66f9e-126">Można wybrać w małych, średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="66f9e-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="66f9e-127">*VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="66f9e-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="66f9e-128">Te wartości są tworzone po hello brama jest w hello stanu działania.</span><span class="sxs-lookup"><span data-stu-id="66f9e-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="66f9e-129">Skonfiguruj bramę aplikacji za pomocą XML</span><span class="sxs-lookup"><span data-stu-id="66f9e-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="66f9e-130">W hello poniższy przykład użyj tooconfigure pliku XML wszystkie ustawienia bramy aplikacji i je zatwierdzić zasobu bramy toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="66f9e-131">Skopiuj powitania po tooNotepad tekstu.</span><span class="sxs-lookup"><span data-stu-id="66f9e-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="66f9e-132">Edytuj wartości hello między nawiasami hello hello elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="66f9e-133">Zapisz plik hello z rozszerzeniem .xml.</span><span class="sxs-lookup"><span data-stu-id="66f9e-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="66f9e-134">Witaj poniższy przykład przedstawia sposób toouse tooset pliku konfiguracji, zapasowej tooload bramy aplikacji hello równoważenie ruchu HTTP na port publiczny 80 i Wyślij ruch sieciowy tooback-end port 80 między dwoma adresami IP przy użyciu niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="66f9e-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66f9e-135">Element protokołu Hello Http lub Https jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="66f9e-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="66f9e-136">Nowy element konfiguracji \<sondowania\> dodaniu tooconfigure sond niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="66f9e-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="66f9e-137">Parametry konfiguracji Hello są:</span><span class="sxs-lookup"><span data-stu-id="66f9e-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="66f9e-138">Parametr</span><span class="sxs-lookup"><span data-stu-id="66f9e-138">Parameter</span></span>|<span data-ttu-id="66f9e-139">Opis</span><span class="sxs-lookup"><span data-stu-id="66f9e-139">Description</span></span>|
|---|---|
|<span data-ttu-id="66f9e-140">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="66f9e-140">**Name**</span></span> |<span data-ttu-id="66f9e-141">Nazwa odwołania dla niestandardowych sondy.</span><span class="sxs-lookup"><span data-stu-id="66f9e-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="66f9e-142">* **Protokół**</span><span class="sxs-lookup"><span data-stu-id="66f9e-142">* **Protocol**</span></span> | <span data-ttu-id="66f9e-143">Protokół używany (możliwe wartości to HTTP lub HTTPS).</span><span class="sxs-lookup"><span data-stu-id="66f9e-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="66f9e-144">**Host** i **ścieżki**</span><span class="sxs-lookup"><span data-stu-id="66f9e-144">**Host** and **Path**</span></span> | <span data-ttu-id="66f9e-145">Pełną ścieżkę adresu URL, który jest wywoływany przez kondycji bramy aplikacji hello hello toodetermine hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="66f9e-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="66f9e-146">Na przykład jeśli masz http://contoso.com/ witryny sieci Web, a następnie hello sondowania niestandardowych można skonfigurować dla "http://contoso.com/path/custompath.htm" dla sondy sprawdza toohave pomyślnej odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="66f9e-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="66f9e-147">**Interwał**</span><span class="sxs-lookup"><span data-stu-id="66f9e-147">**Interval**</span></span> | <span data-ttu-id="66f9e-148">Konfiguruje testów interwał sondowania hello w sekundach.</span><span class="sxs-lookup"><span data-stu-id="66f9e-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="66f9e-149">**Limit czasu**</span><span class="sxs-lookup"><span data-stu-id="66f9e-149">**Timeout**</span></span> | <span data-ttu-id="66f9e-150">Określa limit czasu sondowania hello sprawdzanie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="66f9e-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="66f9e-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="66f9e-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="66f9e-152">Witaj liczba odpowiedzi HTTP nie powiodło się, wymagane zaplecza tooflag hello wystąpienia jako *zła*.</span><span class="sxs-lookup"><span data-stu-id="66f9e-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="66f9e-153">Nazwa sondy Hello jest przywoływany w hello \<elementu BackendHttpSettings\> tooassign konfiguracji puli zaplecza, które używa ustawień niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="66f9e-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="66f9e-154">Dodaj istniejącą bramę aplikacji niestandardowych sondowania tooan</span><span class="sxs-lookup"><span data-stu-id="66f9e-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="66f9e-155">Zmiana hello bieżącej konfiguracji bramy aplikacji wymaga trzy kroki: Get hello bieżącego pliku konfiguracji XML, zmodyfikuj toohave niestandardowych sondowania i skonfigurować bramę aplikacji hello hello nowe ustawienia XML.</span><span class="sxs-lookup"><span data-stu-id="66f9e-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="66f9e-156">Pobierz plik XML hello przy użyciu `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="66f9e-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="66f9e-157">To polecenie cmdlet eksportuje hello konfiguracji XML toobe zmodyfikować tooadd ustawienia sondy.</span><span class="sxs-lookup"><span data-stu-id="66f9e-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="66f9e-158">Otwórz plik XML hello w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="66f9e-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="66f9e-159">Dodaj `<probe>` sekcji po `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="66f9e-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="66f9e-160">W sekcji elementu backendHttpSettings hello hello XML Dodaj nazwę sondowania hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="66f9e-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="66f9e-161">Zapisz plik XML hello.</span><span class="sxs-lookup"><span data-stu-id="66f9e-161">Save hello XML file.</span></span>

1. <span data-ttu-id="66f9e-162">Konfiguracja bramy aplikacji hello aktualizacji hello nowy plik XML przy użyciu `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="66f9e-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="66f9e-163">To polecenie cmdlet aktualizuje bramy aplikacji hello nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66f9e-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="66f9e-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="66f9e-164">Next steps</span></span>

<span data-ttu-id="66f9e-165">Jeśli tooconfigure odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="66f9e-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="66f9e-166">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="66f9e-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

