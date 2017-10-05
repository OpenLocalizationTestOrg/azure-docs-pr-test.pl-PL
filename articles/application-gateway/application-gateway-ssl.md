---
title: "Skonfiguruj klasycznego środowiska PowerShell odciążania — brama usługi aplikacji Azure — SSL | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje, aby utworzyć bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu modelu klasycznego wdrożenia usługi Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="8bb58-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="8bb58-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bb58-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8bb58-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="8bb58-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bb58-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="8bb58-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bb58-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="8bb58-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8bb58-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="8bb58-108">Usługę Azure Application Gateway można skonfigurować tak, aby przerywała sesję protokołu SSL (Secure Sockets Layer) na poziomie bramy, co pozwoli na uniknięcie wykonywania kosztownych zadań szyfrowania protokołu SSL w kolektywie serwerów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8bb58-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="8bb58-109">Odciążanie protokołu SSL upraszcza również konfigurowanie serwerów frontonu i zarządzanie aplikacją sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8bb58-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8bb58-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8bb58-110">Before you begin</span></span>

1. <span data-ttu-id="8bb58-111">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8bb58-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="8bb58-112">Najnowszą wersję można pobrać i zainstalować z sekcji **Windows PowerShell** strony [Pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8bb58-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8bb58-113">Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią.</span><span class="sxs-lookup"><span data-stu-id="8bb58-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="8bb58-114">Upewnij się, że z podsieci nie korzystają żadne maszyny wirtualne ani wdrożenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="8bb58-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="8bb58-115">Brama aplikacji musi znajdować się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8bb58-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="8bb58-116">Serwery konfigurowane do używania bramy aplikacji muszą być umieszczone w sieci wirtualnej lub z przypisanym adresem IP/VIP lub mieć w niej utworzone punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="8bb58-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="8bb58-117">Aby skonfigurować bramę aplikacji odciążanie protokołu SSL, wykonaj następujące kroki w podanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="8bb58-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="8bb58-118">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="8bb58-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="8bb58-119">Przekaż certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="8bb58-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="8bb58-120">Konfigurowanie bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="8bb58-121">Ustaw konfigurację bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="8bb58-122">Uruchom bramę</span><span class="sxs-lookup"><span data-stu-id="8bb58-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="8bb58-123">Sprawdź stan bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="8bb58-124">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="8bb58-124">Create an application gateway</span></span>

<span data-ttu-id="8bb58-125">Aby utworzyć bramę, użyj polecenia cmdlet `New-AzureApplicationGateway`, zastępując wartości własnymi.</span><span class="sxs-lookup"><span data-stu-id="8bb58-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="8bb58-126">Opłaty za bramę nie są jeszcze naliczane.</span><span class="sxs-lookup"><span data-stu-id="8bb58-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="8bb58-127">Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="8bb58-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="8bb58-128">Aby sprawdzić, czy brama została utworzona, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="8bb58-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="8bb58-129">W przykładzie *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="8bb58-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="8bb58-130">Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10.</span><span class="sxs-lookup"><span data-stu-id="8bb58-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="8bb58-131">Wartość domyślna parametru *GatewaySize* to Medium (Średnia).</span><span class="sxs-lookup"><span data-stu-id="8bb58-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="8bb58-132">Małe i duże są inne dostępne wartości.</span><span class="sxs-lookup"><span data-stu-id="8bb58-132">Small and Large are other available values.</span></span> <span data-ttu-id="8bb58-133">Parametry *VirtualIPs* (Wirtualne adresy IP) i *DnsName* (Nazwa serwera DNS) są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="8bb58-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="8bb58-134">Te wartości są tworzone, gdy brama jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8bb58-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="8bb58-135">Przekaż certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="8bb58-135">Upload SSL certificates</span></span>

<span data-ttu-id="8bb58-136">Użyj `Add-AzureApplicationGatewaySslCertificate` można przekazać certyfikatu serwera w *pfx* format na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="8bb58-137">Nazwa certyfikatu jest nazwą wybranych przez użytkownika i muszą być unikatowe w ramach bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="8bb58-138">Ten certyfikat jest określane o tej nazwie we wszystkich operacjach zarządzania certyfikatu dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="8bb58-139">To w poniższym przykładzie przedstawiono polecenie cmdlet, Zastąp wartości w próbce własnymi.</span><span class="sxs-lookup"><span data-stu-id="8bb58-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="8bb58-140">Następnie sprawdź poprawność przekazywanie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8bb58-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="8bb58-141">Użyj `Get-AzureApplicationGatewayCertificate` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8bb58-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="8bb58-142">Przykład obejmuje polecenia cmdlet w pierwszym wierszu, to po danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8bb58-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="8bb58-143">Hasło certyfikatu musi należeć do przedziału od 4 do 12 znaków, liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="8bb58-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="8bb58-144">Znaki specjalne nie są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="8bb58-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="8bb58-145">Konfigurowanie bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-145">Configure the gateway</span></span>

<span data-ttu-id="8bb58-146">Konfiguracja bramy aplikacji składa się z wielu wartości.</span><span class="sxs-lookup"><span data-stu-id="8bb58-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="8bb58-147">Wartości mogą być powiązane ze sobą w celu utworzenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="8bb58-148">Potrzebne wartości:</span><span class="sxs-lookup"><span data-stu-id="8bb58-148">The values are:</span></span>

* <span data-ttu-id="8bb58-149">**Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8bb58-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="8bb58-150">Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.</span><span class="sxs-lookup"><span data-stu-id="8bb58-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="8bb58-151">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="8bb58-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8bb58-152">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="8bb58-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="8bb58-153">**Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="8bb58-154">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8bb58-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="8bb58-155">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="8bb58-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="8bb58-156">**Reguła:** reguła wiąże odbiornik z pulą serwerów zaplecza i umożliwia zdefiniowanie, do której puli serwerów zaplecza ma być przekierowywany ruch w przypadku trafienia do określonego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="8bb58-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="8bb58-157">Obecnie jest obsługiwana tylko reguła *podstawowa*.</span><span class="sxs-lookup"><span data-stu-id="8bb58-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="8bb58-158">Reguła *podstawowa* to dystrybucja obciążenia z działaniem okrężnym.</span><span class="sxs-lookup"><span data-stu-id="8bb58-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="8bb58-159">**Uwagi dotyczące konfiguracji dodatkowych**</span><span class="sxs-lookup"><span data-stu-id="8bb58-159">**Additional configuration notes**</span></span>

<span data-ttu-id="8bb58-160">W przypadku konfiguracji certyfikatów SSL protokół w polu **HttpListener** należy zmienić na *Https* (z uwzględnieniem wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="8bb58-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="8bb58-161">**SslCert** element zostanie dodany do **HttpListener** o wartości do tej samej nazwie w przekazywania poprzedzających SSL certyfikaty sekcji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="8bb58-162">Port frontonu należy zaktualizować do 443.</span><span class="sxs-lookup"><span data-stu-id="8bb58-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="8bb58-163">**Aby włączyć koligację opartą na plikach cookie**: bramę aplikacji można skonfigurować tak, aby żądanie z sesji klienta było zawsze kierowane do tej samej maszyny wirtualnej w kolektywie serwerów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8bb58-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="8bb58-164">W tym scenariuszu należy wstrzyknąć plik cookie sesji, który umożliwi bramie prawidłowe kierowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="8bb58-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="8bb58-165">Aby włączyć koligację opartą na plikach cookie, ustaw element **CookieBasedAffinity** na wartość *Enabled* w elemencie **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="8bb58-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="8bb58-166">Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub przy użyciu pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="8bb58-167">Aby utworzyć konfigurację za pomocą pliku XML konfiguracji, skorzystaj z poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="8bb58-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="8bb58-168">**Przykładowy plik XML konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="8bb58-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="8bb58-169">Ustaw konfigurację bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-169">Set the gateway configuration</span></span>

<span data-ttu-id="8bb58-170">Następnie należy ustawić bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-170">Next, you set the application gateway.</span></span> <span data-ttu-id="8bb58-171">Można użyć `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8bb58-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="8bb58-172">Uruchamianie bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-172">Start the gateway</span></span>

<span data-ttu-id="8bb58-173">Po skonfigurowaniu bramy użyj polecenia cmdlet `Start-AzureApplicationGateway`, aby uruchomić bramę.</span><span class="sxs-lookup"><span data-stu-id="8bb58-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="8bb58-174">Naliczanie opłat za bramę aplikacji rozpocznie się po pomyślnym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="8bb58-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="8bb58-175">Wykonanie polecenia cmdlet `Start-AzureApplicationGateway` może zająć do 15–20 minut.</span><span class="sxs-lookup"><span data-stu-id="8bb58-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="8bb58-176">Sprawdzanie stanu bramy</span><span class="sxs-lookup"><span data-stu-id="8bb58-176">Verify the gateway status</span></span>

<span data-ttu-id="8bb58-177">Użyj polecenia cmdlet `Get-AzureApplicationGateway`, aby sprawdzić stan bramy.</span><span class="sxs-lookup"><span data-stu-id="8bb58-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="8bb58-178">Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku, *stanu* powinna być uruchomiona, i *VirtualIPs* i *DnsName* powinny mieć prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="8bb58-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="8bb58-179">W tym przykładzie pokazano bramę aplikacji, który, uruchomione i jest gotowa do sporządzenia ruchu.</span><span class="sxs-lookup"><span data-stu-id="8bb58-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="8bb58-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bb58-180">Next steps</span></span>

<span data-ttu-id="8bb58-181">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="8bb58-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="8bb58-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8bb58-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="8bb58-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8bb58-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

