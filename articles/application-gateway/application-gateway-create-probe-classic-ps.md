---
title: "Tworzenie niestandardowych sondowania — brama usługi aplikacji Azure — klasyczny programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć niestandardowe sondowania bramy aplikacji przy użyciu programu PowerShell w klasycznym modelu wdrażania"
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="54bde-103">Tworzenie niestandardowych sondowania bramy aplikacji Azure (klasyczne) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="54bde-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54bde-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="54bde-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="54bde-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="54bde-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="54bde-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="54bde-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="54bde-107">W tym artykule możesz dodać niestandardowe sondowania istniejącą bramę aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54bde-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="54bde-108">Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="54bde-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54bde-109">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="54bde-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="54bde-110">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="54bde-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="54bde-111">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54bde-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="54bde-112">Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="54bde-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="54bde-113">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="54bde-113">Create an application gateway</span></span>

<span data-ttu-id="54bde-114">Aby utworzyć bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="54bde-114">To create an application gateway:</span></span>

1. <span data-ttu-id="54bde-115">Utwórz zasób bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54bde-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="54bde-116">Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="54bde-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="54bde-117">Przekaż konfigurację aplikacji do nowo utworzonego zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54bde-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="54bde-118">Utwórz zasób bramy aplikacji z niestandardowego badania</span><span class="sxs-lookup"><span data-stu-id="54bde-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="54bde-119">Aby utworzyć bramę, użyj polecenia cmdlet `New-AzureApplicationGateway`, zastępując wartości własnymi.</span><span class="sxs-lookup"><span data-stu-id="54bde-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="54bde-120">Opłaty za bramę nie są jeszcze naliczane.</span><span class="sxs-lookup"><span data-stu-id="54bde-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="54bde-121">Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="54bde-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="54bde-122">Poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej „testvnet1” i podsieci „subnet-1”.</span><span class="sxs-lookup"><span data-stu-id="54bde-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="54bde-123">Aby sprawdzić, czy brama została utworzona, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="54bde-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="54bde-124">Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10.</span><span class="sxs-lookup"><span data-stu-id="54bde-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="54bde-125">Wartość domyślna parametru *GatewaySize* to Medium (Średnia).</span><span class="sxs-lookup"><span data-stu-id="54bde-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="54bde-126">Można wybrać w małych, średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="54bde-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="54bde-127">Parametry *VirtualIPs* (Wirtualne adresy IP) i *DnsName* (Nazwa serwera DNS) są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="54bde-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="54bde-128">Te wartości są tworzone, gdy brama jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="54bde-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="54bde-129">Skonfiguruj bramę aplikacji za pomocą XML</span><span class="sxs-lookup"><span data-stu-id="54bde-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="54bde-130">W poniższym przykładzie używany jest plik XML, aby skonfigurować wszystkie ustawienia bramy aplikacji i zatwierdzić je w zasobie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54bde-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="54bde-131">Skopiuj poniższy tekst do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="54bde-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="54bde-132">Edytuj zawarte w nawiasach wartości elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="54bde-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="54bde-133">Zapisz plik z rozszerzeniem .xml.</span><span class="sxs-lookup"><span data-stu-id="54bde-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="54bde-134">Poniższy przykład przedstawia użycie pliku konfiguracji do skonfigurowania bramy aplikacji do ruchu HTTP na port publiczny 80 równoważenia obciążenia i wysyłania ruchu sieciowego do zaplecza port 80 między dwoma adresami IP przy użyciu niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="54bde-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54bde-135">W elemencie Http lub Https jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="54bde-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="54bde-136">Nowy element konfiguracji \<sondowania\> zostanie dodany do skonfigurowania niestandardowej sondy.</span><span class="sxs-lookup"><span data-stu-id="54bde-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="54bde-137">Parametry konfiguracji są:</span><span class="sxs-lookup"><span data-stu-id="54bde-137">The configuration parameters are:</span></span>

|<span data-ttu-id="54bde-138">Parametr</span><span class="sxs-lookup"><span data-stu-id="54bde-138">Parameter</span></span>|<span data-ttu-id="54bde-139">Opis</span><span class="sxs-lookup"><span data-stu-id="54bde-139">Description</span></span>|
|---|---|
|<span data-ttu-id="54bde-140">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="54bde-140">**Name**</span></span> |<span data-ttu-id="54bde-141">Nazwa odwołania dla niestandardowych sondy.</span><span class="sxs-lookup"><span data-stu-id="54bde-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="54bde-142">* **Protokół**</span><span class="sxs-lookup"><span data-stu-id="54bde-142">* **Protocol**</span></span> | <span data-ttu-id="54bde-143">Protokół używany (możliwe wartości to HTTP lub HTTPS).</span><span class="sxs-lookup"><span data-stu-id="54bde-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="54bde-144">**Host** i **ścieżki**</span><span class="sxs-lookup"><span data-stu-id="54bde-144">**Host** and **Path**</span></span> | <span data-ttu-id="54bde-145">Pełną ścieżkę adresu URL, który jest wywoływany przez brama aplikacji w celu określenia kondycji wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="54bde-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="54bde-146">Na przykład jeśli masz http://contoso.com/ witryny sieci Web, następnie niestandardowe sondowania można skonfigurować dla "http://contoso.com/path/custompath.htm" kontroli sondowania zostały pomyślnie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="54bde-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="54bde-147">**Interwał**</span><span class="sxs-lookup"><span data-stu-id="54bde-147">**Interval**</span></span> | <span data-ttu-id="54bde-148">Konfiguruje testów interwał sondowania w sekundach.</span><span class="sxs-lookup"><span data-stu-id="54bde-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="54bde-149">**Limit czasu**</span><span class="sxs-lookup"><span data-stu-id="54bde-149">**Timeout**</span></span> | <span data-ttu-id="54bde-150">Określa limit czasu sondowania sprawdzanie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="54bde-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="54bde-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="54bde-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="54bde-152">Liczba zakończonych niepowodzeniem odpowiedzi HTTP, konieczne jest flaga wystąpienia zaplecza jako *zła*.</span><span class="sxs-lookup"><span data-stu-id="54bde-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="54bde-153">Nazwa sondy jest przywoływany w \<elementu BackendHttpSettings\> konfigurację, aby przypisać puli zaplecza, które używa ustawień niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="54bde-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="54bde-154">Dodaj niestandardowy sondy do istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="54bde-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="54bde-155">Zmiana bieżącą konfigurację bramy aplikacji wymaga trzy kroki: Get bieżącego pliku konfiguracji XML, zmodyfikuj ma niestandardowy sondowania i skonfigurować bramę aplikacji przy użyciu nowych ustawień XML.</span><span class="sxs-lookup"><span data-stu-id="54bde-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="54bde-156">Pobierz plik XML przy użyciu `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="54bde-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="54bde-157">To polecenie cmdlet eksportuje konfigurację XML można zmodyfikować, aby dodać ustawienie sondy.</span><span class="sxs-lookup"><span data-stu-id="54bde-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="54bde-158">Otwórz plik XML w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="54bde-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="54bde-159">Dodaj `<probe>` sekcji po `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="54bde-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="54bde-160">W sekcji elementu backendHttpSettings XML Dodaj nazwę sondowania, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="54bde-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="54bde-161">Zapisz plik XML.</span><span class="sxs-lookup"><span data-stu-id="54bde-161">Save the XML file.</span></span>

1. <span data-ttu-id="54bde-162">Zaktualizuj konfigurację bramy aplikacji z nowym plikiem XML przy użyciu `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="54bde-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="54bde-163">To polecenie cmdlet aktualizacji bramy aplikacji przy użyciu nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="54bde-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="54bde-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54bde-164">Next steps</span></span>

<span data-ttu-id="54bde-165">Jeśli chcesz skonfigurować odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="54bde-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="54bde-166">Jeśli chcesz skonfigurować bramę aplikacji do użycia z wewnętrznym modułem równoważenia obciążenia, zobacz artykuł [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Tworzenie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="54bde-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

