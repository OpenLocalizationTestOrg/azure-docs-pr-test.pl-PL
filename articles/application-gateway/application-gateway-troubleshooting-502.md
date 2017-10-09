---
title: "błędy nieprawidłowych brama bramy aplikacji Azure (502) aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tootroubleshoot 502 bramy aplikacji"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Rozwiązywanie problemów z błędami Zła brama bramy aplikacji

Dowiedz się, jak tootroubleshoot zły bramy (502) błędy odebrane podczas korzystania z bramy aplikacji.

## <a name="overview"></a>Omówienie

Po skonfigurowaniu bramy aplikacji, jeden z użytkowników mogą wystąpić błędy hello jest "Błąd serwera: 502 — Serwer sieci Web odebrał nieprawidłową odpowiedź działając jako brama lub serwer proxy". Ten błąd może się tak zdarzyć powodu toohello następujących powodów:

* Azure bramy aplikacji [puli zaplecza nie jest skonfigurowany lub pusty](#empty-backendaddresspool).
* Brak maszyn wirtualnych hello lub wystąpień w [zestawu skali maszyny Wirtualnej są w dobrej kondycji](#unhealthy-instances-in-backendaddresspool).
* Maszyny wirtualne zaplecza lub wystąpienia zestawu skali maszyny Wirtualnej są [nie odpowiada toohello domyślnej funkcji badania kondycji](#problems-with-default-health-probe.md).
* Nieprawidłowy lub niewłaściwego [konfiguracji sondy kondycji niestandardowych](#problems-with-custom-health-probe.md).
* [Żądania limitu czasu lub problemów z łącznością](#request-time-out) z żądania użytkownika.

## <a name="empty-backendaddresspool"></a>Pusty BackendAddressPool

### <a name="cause"></a>Przyczyna

Jeśli hello bramy aplikacji nie ma żadnych maszyn wirtualnych lub zestawu skali maszyny Wirtualnej skonfigurowana w puli adresów zaplecza hello, nie można przekierować wszystkie żądania klienta i zgłasza błąd zły bramy.

### <a name="solution"></a>Rozwiązanie

Upewnij się, czy pula adresów zaplecza hello nie jest pusta. Można to zrobić za pośrednictwem programu PowerShell, interfejsu wiersza polecenia lub portalu.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

dane wyjściowe Hello hello poprzedzających polecenia cmdlet powinny zawierać puli adresów zaplecza niepusty. Poniżej przedstawiono przykładowy, w których dwie pule są zwracane które są skonfigurowane przy użyciu nazwy FQDN lub adresów IP dla maszyn wirtualnych w wewnętrznej bazie danych. Witaj stan inicjowania obsługi administracyjnej hello BackendAddressPool musi mieć wartość "Succeeded".

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Zła wystąpień w BackendAddressPool

### <a name="cause"></a>Przyczyna

Jeśli wszystkie wystąpienia hello BackendAddressPool jest zła, następnie bramy aplikacji nie będzie zawierało wszystkie żądania użytkownika tooroute zaplecza w celu. Przyczyną może być również przypadku hello wystąpień zaplecza są w dobrej kondycji, ale nie ma wdrożonych aplikacji hello wymagane.

### <a name="solution"></a>Rozwiązanie

Sprawdź, czy wystąpienia hello są w dobrej kondycji i aplikacja hello jest skonfigurowana prawidłowo. Sprawdź stanie toorespond tooa ping z inną maszynę Wirtualną w przypadku wystąpień zaplecza hello hello tej samej sieci wirtualnej. Skonfigurowano publiczny punkt końcowy, upewnij się, że aplikacja sieci web toohello żądanie przeglądarki jest obsługiwanych.

## <a name="problems-with-default-health-probe"></a>Problemy z domyślnej funkcji badania kondycji

### <a name="cause"></a>Przyczyna

błędy 502 można też częste wskaźników, które hello domyślnej funkcji badania kondycji jest nie jest w stanie tooreach zaplecza maszyn wirtualnych. Po zainicjowaniu obsługi wystąpienia bramy aplikacji, automatycznie konfiguruje domyślne tooeach sondy kondycji BackendAddressPool przy użyciu właściwości hello BackendHttpSetting. Nie danych wprowadzonych przez użytkownika jest wymagana tooset sonda. W szczególności w przypadku skonfigurowania reguły równoważenia obciążenia, skojarzenie jest nawiązywane pomiędzy BackendHttpSetting i BackendAddressPool. Dla każdego z tych skojarzenia i inicjuje brama aplikacji w wystąpieniu okresowego sprawdzania połączenia tooeach w hello BackendAddressPool portu hello określony w elemencie BackendHttpSetting hello skonfigurowano domyślnego badania. Poniższa tabela zawiera listę wartości hello skojarzone z hello domyślnej funkcji badania kondycji.

| Właściwość sondy | Wartość | Opis |
| --- | --- | --- |
| Sonda adresu URL |http://127.0.0.1/ |Ścieżka adresu URL |
| Interwał |30 |Interwał sondowania w sekundach |
| Limit czasu |30 |Sonda limitu czasu w sekundach |
| Próg złej kondycji |3 |Badania liczby ponownych prób. serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji. |

### <a name="solution"></a>Rozwiązanie

* Upewnij się, że domyślna witryna jest skonfigurowana i prowadzi nasłuchiwanie na 127.0.0.1.
* Jeśli BackendHttpSetting Określa port inny niż 80, hello domyślnej witryny powinny być skonfigurowane toolisten na tym porcie.
* Witaj toohttp://127.0.0.1:port wywołania powinna zwrócić kod wyniku protokołu HTTP 200. To powinien być zwracany w hello 30 sekund limitu czasu.
* Upewnij się, że skonfigurowany port jest otwarty i czy nie ma żadnych reguł zapory lub grup zabezpieczeń sieci Azure, która zablokować przychodzący lub wychodzący ruch na porcie hello skonfigurowane.
* Jeśli klasyczne maszyny wirtualne platformy Azure lub usługi w chmurze jest używana z nazwy FQDN lub publicznego adresu IP, upewnij się, hello odpowiadającego [punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) jest otwarty.
* Jeśli hello maszyna wirtualna jest skonfigurowana za pośrednictwem usługi Azure Resource Manager i znajduje się poza hello sieci wirtualnej, w której wdrażana jest aplikacja bramy, [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) musi być skonfigurowany dostęp tooallow na powitania żądany port.

## <a name="problems-with-custom-health-probe"></a>Problemy z sondy kondycji niestandardowych

### <a name="cause"></a>Przyczyna

Sondy kondycji niestandardowe umożliwiają sondowanie zachowanie domyślne toohello dodatkowa elastyczność. Podczas korzystania z niestandardowego sond, użytkownicy mogą skonfigurować interwał sondowania powitania, hello adres URL i tootest ścieżkę oraz ile tooaccept odpowiedzi nie powiodło się przed oznaczeniem wystąpienia puli zaplecza hello swój stan jako niezdrowy. dodano następujące dodatkowe właściwości Hello.

| Właściwość sondy | Opis |
| --- | --- |
| Nazwa |Nazwa sondy hello. Ta nazwa jest sonda toohello toorefer używane ustawienia HTTP zaplecza. |
| Protokół |Protokół używany toosend hello sondowania. Sonda Hello używa protokołu hello zdefiniowanego w ustawieniach protokołu HTTP zaplecza hello |
| Host |Sonda hello toosend nazwy hosta. Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji. To jest inna niż nazwa hosta maszyny Wirtualnej. |
| Ścieżka |Ścieżka względna hello sondy. prawidłowa ścieżka Hello rozpoczyna się od '/'. Sonda Hello są wysyłane za\<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\> |
| Interwał |Interwał sondy w sekundach. Jest to hello odstęp czasu między dwa kolejne sondy. |
| Limit czasu |Badania limitu czasu w sekundach. Jeśli w tym czasie limitu czasu nie odebrano prawidłowej odpowiedzi, hello sondowania jest oznaczony jako nie powiodło się. |
| Próg złej kondycji |Badania liczby ponownych prób. serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji. |

### <a name="solution"></a>Rozwiązanie

Sprawdź poprawność tego powitalne sondy kondycji niestandardowy jest poprawnie skonfigurowany jako hello powyższej tabeli. Ponadto toohello powyższych czynności, upewnij się również hello następujące:

* Upewnij się, że sonda hello została poprawnie określona zgodnie z harmonogramem hello [przewodnik](application-gateway-create-probe-ps.md).
* Jeśli skonfigurowano brama aplikacji w jednej lokacji, przez domyślny hello hosta należy określać nazwy jako "127.0.0.1", chyba że w przeciwnym razie skonfigurowane w niestandardowych sondowania.
* Upewnij się, że toohttp wywołania: / /\<hosta\>:\<portu\>\<ścieżki\> zwraca kod wyniku protokołu HTTP 200.
* Upewnij się, czy interwału limitu czasu i UnhealtyThreshold znajduje się w dopuszczalnych zakresach hello.
* Jeśli sondowania przy użyciu protokołu HTTPS, upewnij się, że ten powitania serwera wewnętrznej bazy danych nie wymaga SNI przez skonfigurowanie certyfikat fallback na powitania serwera wewnętrznej bazy danych, sama. 
* Upewnij się, czy interwał limitu czasu i UnhealtyThreshold znajduje się w dopuszczalnych zakresach hello.

## <a name="request-time-out"></a>Upłynął limit czasu żądania

### <a name="cause"></a>Przyczyna

Po odebraniu żądania użytkownika bramy aplikacji stosuje hello skonfigurowane reguły toohello żądania i kieruje je tooa puli zaplecza wystąpienia. Oczekuje na można skonfigurować interwał czasu odpowiedzi z hello zaplecza wystąpienia. Domyślnie jest to interwał **30 sekund**. Jeśli bramy aplikacji nie otrzymują odpowiedź z zaplecza aplikacji w tym interwał, zobaczyć 502 Błąd żądania użytkownika.

### <a name="solution"></a>Rozwiązanie

Brama aplikacji w umożliwia użytkownikom tooconfigure ustawienie BackendHttpSetting, który może być, a następnie zastosować toodifferent pule. Różnych pul zaplecza może mieć różne BackendHttpSetting i skonfigurowany limit czasu dlatego innego żądania.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Następne kroki

Jeśli hello powyższych kroków nie rozwiąże problemu hello, otwórz [obsługuje biletu](https://azure.microsoft.com/support/options/).

