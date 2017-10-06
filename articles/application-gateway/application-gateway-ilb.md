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
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Tworzenie Bramy aplikacji z wewnętrznym modułem równoważenia obciążenia (ILB)

> [!div class="op_single_selector"]
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ilb-arm.md)

Brama aplikacji można skonfigurować internetowy wirtualnego adresu IP lub toohello wewnętrzny punkt końcowy nie widoczne internet, znanej także jako punktu końcowego wewnętrznego modułu równoważenia obciążenia (ILB). Konfigurowanie bramy hello z ILB jest przydatne w przypadku toointernet wewnętrznych aplikacji biznesowych — nie są widoczne. Jest również przydatne w przypadku warstwy aplikacji wielowarstwowych, który znajduje się w toointernet nie widoczne granic zabezpieczeń, ale nadal wymagają rozkład obciążenia działanie okrężne, lepkości sesji lub kończenia żądań SSL z/usług. W tym artykule przedstawiono hello kroki tooconfigure bramę aplikacji z ILB.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello Azure poleceń cmdlet programu PowerShell przy użyciu hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [stronę pobierania](https://azure.microsoft.com/downloads/).
2. Sprawdź, czy sieć wirtualną pracy z prawidłową podsieć.
3. Sprawdź, czy masz serwerów wewnętrznej bazy danych w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.

toocreate bramę aplikacji, wykonaj następujące kroki w podanej kolejności hello hello. 

1. [Tworzenie bramy aplikacji](#create-a-new-application-gateway)
2. [Konfigurowanie bramy hello](#configure-the-gateway)
3. [Konfiguracja bramy hello zestawu](#set-the-gateway-configuration)
4. [Uruchom hello bramy](#start-the-gateway)
5. [Sprawdź hello bramy](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Utwórz bramę aplikacji:

**Brama hello toocreate**, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne. Należy pamiętać, że rozliczeń hello bramy nie jest uruchamiana w tym momencie. Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.

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

**toovalidate** czy utworzono bramę hello, możesz użyć hello `Get-AzureApplicationGateway` polecenia cmdlet. 

W przykładowym hello *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami. Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Małe i duże są inne dostępne wartości. *VIP* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona. Są one tworzone po hello brama jest w hello stanu działania. 

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

## <a name="configure-hello-gateway"></a>Konfigurowanie bramy hello
Konfiguracja bramy aplikacji składa się z wielu wartości. mogą być związane Hello wartości konfiguracji hello tooconstruct razem.

Witaj wartości są następujące:

* **Pula serwerów wewnętrznej bazy danych:** hello listę adresów IP hello serwerów wewnętrznej bazy danych. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieci sieci wirtualnej lub powinny być publicznego adresu IP/VIP. 
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port serwera sieci Web:** ten port jest port publiczny hello otwarte na powitania bramy aplikacji. Ruch trafienia tego portu, a następnie pobiera przekierowanego tooone hello serwerów wewnętrznej bazy danych.
* **Odbiornik:** odbiornika hello ma port serwera sieci Web, protokół (Http lub Https, te jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL). 
* **Reguła:** reguła hello wiąże odbiornika hello i puli serwerów wewnętrznej bazy danych hello i określa, jaki ruch hello puli serwera wewnętrznej bazy danych ukierunkowanej toowhen trafienia w szczególności odbiornika. Obecnie tylko hello *podstawowe* reguła jest obsługiwana. Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.

Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub plik XML konfiguracji. tooconstruct konfiguracji przy użyciu pliku XML konfiguracji, użyj hello przykładowe poniżej.

Należy uwzględnić następujące hello:

* Witaj *konfiguracji IP frontonu* element opisuje hello ILB szczegółowe informacje dotyczące konfigurowania bramy aplikacji przy użyciu ILB. 
* Witaj adresu IP frontonu *typu* powinien być ustawiony too'Private "
* Witaj *StaticIPAddress* wewnętrznym adresem IP toohello żądanego na które hello bramy odbiera ruch powinien być ustawiony. Należy pamiętać, że hello *StaticIPAddress* element jest opcjonalny. Jeśli nie jest dostępny wewnętrzny adres IP z podsieci hello wdrożone zestaw, jest wybierany. 
* Witaj wartość hello *nazwa* elementu określonego w parametrze *elementu FrontendIPConfiguration* powinny być używane w hello HTTPListener *FrontendIP* toohello toorefer elementu Konfiguracja IP frontonu.
  
  **Przykładowy plik XML konfiguracji**
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


## <a name="set-hello-gateway-configuration"></a>Konfiguracja bramy hello zestawu
Następnie będzie Ustaw hello bramy aplikacji. Można użyć hello `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji. 

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

## <a name="start-hello-gateway"></a>Uruchom hello bramy

Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet. Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy. 

> [!NOTE]
> Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toocomplete too15 20 minut. 
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

## <a name="verify-hello-gateway-status"></a>Sprawdź stan bramy hello

Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stanu bramy. Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello, powinien mieć stan hello *systemem*, hello Vip i DnsName powinny mieć prawidłowe wpisy. To przykładowe przedstawiono polecenie cmdlet hello na powitania pierwszy wiersz, następuje hello danych wyjściowych. W tym przykładzie hello bramy działa i jest gotowy tootake ruchu. 

> [!NOTE]
> Brama aplikacji Hello jest skonfigurowana tooaccept ruchu na powitania skonfigurowany punkt końcowy ILB 10.0.0.10 w tym przykładzie.

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

## <a name="next-steps"></a>Następne kroki
Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

