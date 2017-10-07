---
title: "aaaConfigure SSL odciążania klasycznego środowiska PowerShell — brama usługi aplikacji Azure — | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu hello Azure klasycznego modelu wdrażania."
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
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="5e5ce-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="5e5ce-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e5ce-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5e5ce-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="5e5ce-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e5ce-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="5e5ce-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e5ce-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="5e5ce-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5e5ce-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="5e5ce-108">Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="5e5ce-109">Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5e5ce-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5e5ce-110">Before you begin</span></span>

1. <span data-ttu-id="5e5ce-111">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="5e5ce-112">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5e5ce-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5e5ce-113">Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="5e5ce-114">Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="5e5ce-115">Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="5e5ce-116">Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="5e5ce-117">tooconfigure SSL odciążenia na bramę aplikacji, hello następujące kroki w podanej kolejności hello:</span><span class="sxs-lookup"><span data-stu-id="5e5ce-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="5e5ce-118">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e5ce-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="5e5ce-119">Przekaż certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="5e5ce-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="5e5ce-120">Konfigurowanie bramy hello</span><span class="sxs-lookup"><span data-stu-id="5e5ce-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="5e5ce-121">Konfiguracja bramy hello zestawu</span><span class="sxs-lookup"><span data-stu-id="5e5ce-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="5e5ce-122">Uruchom hello bramy</span><span class="sxs-lookup"><span data-stu-id="5e5ce-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="5e5ce-123">Sprawdź stan bramy hello</span><span class="sxs-lookup"><span data-stu-id="5e5ce-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="5e5ce-124">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e5ce-124">Create an application gateway</span></span>

<span data-ttu-id="5e5ce-125">toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="5e5ce-126">Karta hello bramy nie rozpoczyna się w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="5e5ce-127">Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="5e5ce-128">toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="5e5ce-129">W przykładowym hello *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="5e5ce-130">Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5e5ce-131">Witaj wartości domyślnej dla *GatewaySize* to średni.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5e5ce-132">Małe i duże są inne dostępne wartości.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-132">Small and Large are other available values.</span></span> <span data-ttu-id="5e5ce-133">*VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="5e5ce-134">Te wartości są tworzone po hello brama jest w hello stanu działania.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="5e5ce-135">Przekaż certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="5e5ce-135">Upload SSL certificates</span></span>

<span data-ttu-id="5e5ce-136">Użyj `Add-AzureApplicationGatewaySslCertificate` certyfikatu serwera hello tooupload w *pfx* brama aplikacji w formacie toohello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="5e5ce-137">Nazwa certyfikatu Hello jest nazwą wybranych przez użytkownika i muszą być unikatowe w ramach bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="5e5ce-138">Ten certyfikat jest określony tooby tej nazwy we wszystkich operacjach zarządzania certyfikatu dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="5e5ce-139">Ta poniższy przykład przedstawia hello polecenia cmdlet, Zamień hello wartości w próbce hello własne.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="5e5ce-140">Następnie sprawdź poprawność hello przekazywanie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="5e5ce-141">Użyj hello `Get-AzureApplicationGatewayCertificate` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="5e5ce-142">To przykładowe przedstawiono polecenie cmdlet hello na powitania pierwszy wiersz, następuje hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

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
> <span data-ttu-id="5e5ce-143">Hasło certyfikatu Hello ma toobe między 4 znaki too12, liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="5e5ce-144">Znaki specjalne nie są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="5e5ce-145">Konfigurowanie bramy hello</span><span class="sxs-lookup"><span data-stu-id="5e5ce-145">Configure hello gateway</span></span>

<span data-ttu-id="5e5ce-146">Konfiguracja bramy aplikacji składa się z wielu wartości.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="5e5ce-147">mogą być związane Hello wartości konfiguracji hello tooconstruct razem.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="5e5ce-148">Witaj wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="5e5ce-148">hello values are:</span></span>

* <span data-ttu-id="5e5ce-149">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="5e5ce-150">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="5e5ce-151">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5e5ce-152">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="5e5ce-153">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="5e5ce-154">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="5e5ce-155">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="5e5ce-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="5e5ce-156">**Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="5e5ce-157">Obecnie tylko hello *podstawowe* reguła jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="5e5ce-158">Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="5e5ce-159">**Uwagi dotyczące konfiguracji dodatkowych**</span><span class="sxs-lookup"><span data-stu-id="5e5ce-159">**Additional configuration notes**</span></span>

<span data-ttu-id="5e5ce-160">Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="5e5ce-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="5e5ce-161">Witaj **SslCert** zbyt dodany element**HttpListener** z hello wartość toohello takie same nazwy w powyższej sekcji certyfikaty SSL przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="5e5ce-162">port frontonu Hello powinien być zaktualizowany too443.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="5e5ce-163">**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="5e5ce-164">W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="5e5ce-165">Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="5e5ce-166">Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub przy użyciu pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="5e5ce-167">Użyj konfiguracji przy użyciu pliku XML konfiguracji tooconstruct hello następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="5e5ce-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="5e5ce-168">**Przykładowy plik XML konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="5e5ce-168">**Configuration XML sample**</span></span>

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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="5e5ce-169">Konfiguracja bramy hello zestawu</span><span class="sxs-lookup"><span data-stu-id="5e5ce-169">Set hello gateway configuration</span></span>

<span data-ttu-id="5e5ce-170">Następnie należy ustawić bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="5e5ce-171">Można użyć hello `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="5e5ce-172">Uruchom hello bramy</span><span class="sxs-lookup"><span data-stu-id="5e5ce-172">Start hello gateway</span></span>

<span data-ttu-id="5e5ce-173">Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="5e5ce-174">Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="5e5ce-175">Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toofinish too15 20 minut.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="5e5ce-176">Sprawdź stan bramy hello</span><span class="sxs-lookup"><span data-stu-id="5e5ce-176">Verify hello gateway status</span></span>

<span data-ttu-id="5e5ce-177">Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stan hello bramy.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="5e5ce-178">Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello *stanu* powinna być uruchomiona, i *VirtualIPs* i *DnsName* powinny mieć prawidłowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="5e5ce-179">W tym przykładzie pokazano bramę aplikacji, który, uruchomione i jest gotowy tootake ruchu.</span><span class="sxs-lookup"><span data-stu-id="5e5ce-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5e5ce-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e5ce-180">Next steps</span></span>

<span data-ttu-id="5e5ce-181">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="5e5ce-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5e5ce-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5e5ce-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5e5ce-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5e5ce-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

