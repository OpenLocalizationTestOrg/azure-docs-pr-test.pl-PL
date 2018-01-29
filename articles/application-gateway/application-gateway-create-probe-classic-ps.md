---
title: "Tworzenie niestandardowych sondowania — brama usługi aplikacji Azure — klasyczny programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć niestandardowe sondowania bramy aplikacji przy użyciu programu PowerShell w klasycznym modelu wdrażania"
services: application-gateway
documentationcenter: na
author: davidmu1
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
ms.author: davidmu
ms.openlocfilehash: b167a0584740a4e583a35bd6d44ec5d616ba04f7
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Tworzenie niestandardowych sondowania bramy aplikacji Azure (klasyczne) przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-probe-ps.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-probe-classic-ps.md)

W tym artykule możesz dodać niestandardowe sondowania istniejącą bramę aplikacji przy użyciu programu PowerShell. Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na domyślnej aplikacji sieci web.

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia. Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager. Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Aby utworzyć bramę aplikacji:

1. Utwórz zasób bramy aplikacji.
2. Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.
3. Przekaż konfigurację aplikacji do nowo utworzonego zasobu bramy aplikacji.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Utwórz zasób bramy aplikacji z niestandardowego badania

Aby utworzyć bramę, użyj polecenia cmdlet `New-AzureApplicationGateway`, zastępując wartości własnymi. Opłaty za bramę nie są jeszcze naliczane. Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.

Poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej „testvnet1” i podsieci „subnet-1”.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

Aby sprawdzić, czy brama została utworzona, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10. Wartość domyślna parametru *GatewaySize* to Medium (Średnia). Można wybrać w małych, średnich i dużych.
> 
> 

Parametry *VirtualIPs* (Wirtualne adresy IP) i *DnsName* (Nazwa serwera DNS) są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona. Te wartości są tworzone, gdy brama jest w stanie uruchomienia.

### <a name="configure-an-application-gateway-by-using-xml"></a>Skonfiguruj bramę aplikacji za pomocą XML

W poniższym przykładzie używany jest plik XML, aby skonfigurować wszystkie ustawienia bramy aplikacji i zatwierdzić je w zasobie bramy aplikacji.  

Skopiuj poniższy tekst do Notatnika.

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

Edytuj zawarte w nawiasach wartości elementów konfiguracji. Zapisz plik z rozszerzeniem .xml.

Poniższy przykład przedstawia użycie pliku konfiguracji do skonfigurowania bramy aplikacji do ruchu HTTP na port publiczny 80 równoważenia obciążenia i wysyłania ruchu sieciowego do zaplecza port 80 między dwoma adresami IP przy użyciu niestandardowych sondowania.

> [!IMPORTANT]
> W elemencie Http lub Https jest rozróżniana wielkość liter.

Nowy element konfiguracji \<sondowania\> zostanie dodany do skonfigurowania niestandardowej sondy.

Parametry konfiguracji są:

|Parametr|Opis|
|---|---|
|**Nazwa** |Nazwa odwołania dla niestandardowych sondy. |
* **Protokół** | Protokół używany (możliwe wartości to HTTP lub HTTPS).|
| **Host** i **ścieżki** | Pełną ścieżkę adresu URL, który jest wywoływany przez brama aplikacji w celu określenia kondycji wystąpienia. Na przykład jeśli masz http://contoso.com/ witryny sieci Web, następnie niestandardowe sondowania można skonfigurować dla "http://contoso.com/path/custompath.htm" kontroli sondowania zostały pomyślnie odpowiedzi HTTP.|
| **Interwał** | Konfiguruje testów interwał sondowania w sekundach.|
| **Limit czasu** | Określa limit czasu sondowania sprawdzanie odpowiedzi HTTP.|
| **UnhealthyThreshold** | Liczba zakończonych niepowodzeniem odpowiedzi HTTP, konieczne jest flaga wystąpienia zaplecza jako *zła*.|

Nazwa sondy jest przywoływany w \<elementu BackendHttpSettings\> konfigurację, aby przypisać puli zaplecza, które używa ustawień niestandardowych sondowania.

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a>Dodaj niestandardowy sondy do istniejącej bramy aplikacji

Zmiana bieżącą konfigurację bramy aplikacji wymaga trzy kroki: Get bieżącego pliku konfiguracji XML, zmodyfikuj ma niestandardowy sondowania i skonfigurować bramę aplikacji przy użyciu nowych ustawień XML.

1. Pobierz plik XML przy użyciu `Get-AzureApplicationGatewayConfig`. To polecenie cmdlet eksportuje konfigurację XML można zmodyfikować, aby dodać ustawienie sondy.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. Otwórz plik XML w edytorze tekstów. Dodaj `<probe>` sekcji po `<frontendport>`.

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

  W sekcji elementu backendHttpSettings XML Dodaj nazwę sondowania, jak pokazano w poniższym przykładzie:

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

  Zapisz plik XML.

1. Zaktualizuj konfigurację bramy aplikacji z nowym plikiem XML przy użyciu `Set-AzureApplicationGatewayConfig`. To polecenie cmdlet aktualizacji bramy aplikacji przy użyciu nowej konfiguracji.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a>Kolejne kroki

Jeśli chcesz skonfigurować odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).

Jeśli chcesz skonfigurować bramę aplikacji do użycia z wewnętrznym modułem równoważenia obciążenia, zobacz artykuł [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Tworzenie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia).

