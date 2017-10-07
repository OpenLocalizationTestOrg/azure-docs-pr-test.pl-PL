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
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Tworzenie niestandardowych sondowania bramy aplikacji Azure (klasyczne) przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-probe-ps.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-probe-classic-ps.md)

W tym artykule możesz dodać niestandardowe sondowania tooan istniejących aplikacji bramy przy użyciu programu PowerShell. Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na powitania domyślnej aplikacji sieci web.

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

toocreate bramę aplikacji:

1. Utwórz zasób bramy aplikacji.
2. Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.
3. Zatwierdź toohello konfiguracji hello nowo utworzony zasób bramy aplikacji.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Utwórz zasób bramy aplikacji z niestandardowego badania

toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne. Karta hello bramy nie rozpoczyna się w tym momencie. Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.

Witaj poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej o nazwie "testvnet1" i podsieć o nazwie "podsieć 1".

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Można wybrać w małych, średnich i dużych.
> 
> 

*VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona. Te wartości są tworzone po hello brama jest w hello stanu działania.

### <a name="configure-an-application-gateway-by-using-xml"></a>Skonfiguruj bramę aplikacji za pomocą XML

W hello poniższy przykład użyj tooconfigure pliku XML wszystkie ustawienia bramy aplikacji i je zatwierdzić zasobu bramy toohello aplikacji.  

Skopiuj powitania po tooNotepad tekstu.

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

Edytuj wartości hello między nawiasami hello hello elementów konfiguracji. Zapisz plik hello z rozszerzeniem .xml.

Witaj poniższy przykład przedstawia sposób toouse tooset pliku konfiguracji, zapasowej tooload bramy aplikacji hello równoważenie ruchu HTTP na port publiczny 80 i Wyślij ruch sieciowy tooback-end port 80 między dwoma adresami IP przy użyciu niestandardowych sondowania.

> [!IMPORTANT]
> Element protokołu Hello Http lub Https jest rozróżniana wielkość liter.

Nowy element konfiguracji \<sondowania\> dodaniu tooconfigure sond niestandardowych.

Parametry konfiguracji Hello są:

|Parametr|Opis|
|---|---|
|**Nazwa** |Nazwa odwołania dla niestandardowych sondy. |
* **Protokół** | Protokół używany (możliwe wartości to HTTP lub HTTPS).|
| **Host** i **ścieżki** | Pełną ścieżkę adresu URL, który jest wywoływany przez kondycji bramy aplikacji hello hello toodetermine hello wystąpienia. Na przykład jeśli masz http://contoso.com/ witryny sieci Web, a następnie hello sondowania niestandardowych można skonfigurować dla "http://contoso.com/path/custompath.htm" dla sondy sprawdza toohave pomyślnej odpowiedzi HTTP.|
| **Interwał** | Konfiguruje testów interwał sondowania hello w sekundach.|
| **Limit czasu** | Określa limit czasu sondowania hello sprawdzanie odpowiedzi HTTP.|
| **UnhealthyThreshold** | Witaj liczba odpowiedzi HTTP nie powiodło się, wymagane zaplecza tooflag hello wystąpienia jako *zła*.|

Nazwa sondy Hello jest przywoływany w hello \<elementu BackendHttpSettings\> tooassign konfiguracji puli zaplecza, które używa ustawień niestandardowych sondowania.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Dodaj istniejącą bramę aplikacji niestandardowych sondowania tooan

Zmiana hello bieżącej konfiguracji bramy aplikacji wymaga trzy kroki: Get hello bieżącego pliku konfiguracji XML, zmodyfikuj toohave niestandardowych sondowania i skonfigurować bramę aplikacji hello hello nowe ustawienia XML.

1. Pobierz plik XML hello przy użyciu `Get-AzureApplicationGatewayConfig`. To polecenie cmdlet eksportuje hello konfiguracji XML toobe zmodyfikować tooadd ustawienia sondy.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Otwórz plik XML hello w edytorze tekstów. Dodaj `<probe>` sekcji po `<frontendport>`.

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

  W sekcji elementu backendHttpSettings hello hello XML Dodaj nazwę sondowania hello, jak pokazano w hello poniższy przykład:

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

  Zapisz plik XML hello.

1. Konfiguracja bramy aplikacji hello aktualizacji hello nowy plik XML przy użyciu `Set-AzureApplicationGatewayConfig`. To polecenie cmdlet aktualizuje bramy aplikacji hello nowej konfiguracji.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Następne kroki

Jeśli tooconfigure odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).

Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

