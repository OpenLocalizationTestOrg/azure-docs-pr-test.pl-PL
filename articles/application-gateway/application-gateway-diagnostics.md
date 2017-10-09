---
title: "aaaMonitor dostęp do dzienników, Dzienniki wydajności kondycji zaplecza i metryki bramy aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable i zarządzanie nimi Dzienniki wydajności i dzienników dostępu bramy aplikacji"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Kondycji zaplecza, dzienniki diagnostyczne i metryki bramy aplikacji

Korzystając z bramy aplikacji Azure, można monitorować zasobów w hello następujące sposoby:

* [Kondycja zaplecza](#back-end-health): Application Gateway udostępnia hello możliwości toomonitor hello kondycji serwerów hello w hello pul zaplecza za pośrednictwem hello portalu Azure i przy użyciu programu PowerShell. Można również znaleźć kondycji hello hello pul zaplecza za pośrednictwem dzienników diagnostycznych hello wydajności.

* [Dzienniki](#diagnostic-logs): dzienniki umożliwić wydajności, dostęp, i inne toobe dane zapisane lub używane z zasobu do celów monitorowania.

* [Metryki](#metrics): jedna metryka ma obecnie Application Gateway. Ta metryka mierzy hello przepływność bramy aplikacji hello w bajtach na sekundę.

## <a name="back-end-health"></a>Kondycja zaplecza

Brama aplikacji w zapewnia hello możliwości toomonitor hello kondycji poszczególnych członków hello pul zaplecza za pośrednictwem portalu hello, programu PowerShell i hello interfejsu wiersza polecenia (CLI). Możesz również znaleźć zagregowane kondycji podsumowania pul zaplecza za pośrednictwem dzienników diagnostycznych hello wydajności. 

Raport o kondycji zaplecza Hello odzwierciedla dane wyjściowe hello wystąpień hello bramy aplikacji kondycji sondowania toohello zaplecza. Podczas badania zakończy się pomyślnie i Witaj ponownie zakończenia mogą odbierać dane, jest on uznawany za dobrej kondycji. W przeciwnym razie jego jest określana jako zła.

> [!IMPORTANT]
> Jeśli istnieje grupa zabezpieczeń sieci (NSG) w podsieci bramy aplikacji, otwórz zakresy portów 65503 65534 podsieci bramy aplikacji hello dla ruchu przychodzącego. Te porty są wymagane dla hello kondycji zaplecza interfejsu API toowork.


### <a name="view-back-end-health-through-hello-portal"></a>Wyświetl kondycję zaplecza za pośrednictwem portalu hello

W portalu hello kondycji zaplecza podano automatycznie. Wybierz istniejącą bramę aplikacji **monitorowanie** > **kondycji zaplecza**. 

Każdy element członkowski w puli zaplecza hello jest wymieniona na tej stronie (czy jest ona karty Sieciowej, adresu IP lub FQDN). Nazwa puli zaplecza, portu, nazwy ustawienia HTTP zaplecza i stan kondycji są wyświetlane. Prawidłowe wartości stanu kondycji to **dobra kondycja**, **niezdrowego**, i **nieznany**.

> [!NOTE]
> Jeśli zostanie wyświetlony stan kondycji zaplecza **nieznany**, upewnij się, że dostępu toohello wewnętrznej bazy nie jest blokowane przez reguły NSG, trasy zdefiniowane przez użytkownika (przez) lub niestandardowe DNS w sieci wirtualnej hello.

![Kondycja zaplecza][10]

### <a name="view-back-end-health-through-powershell"></a>Wyświetl kondycję zaplecza za pomocą programu PowerShell

Hello następującego kodu programu PowerShell pokazuje, jak hello tooview kondycji zaplecza przy użyciu `Get-AzureRmApplicationGatewayBackendHealth` polecenia cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Wyświetl kondycję zaplecza za pośrednictwem 2.0 interfejsu wiersza polecenia platformy Azure

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Wyniki

powitania po fragment kodu przedstawia przykład hello odpowiedzi:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Dzienniki diagnostyczne

Można użyć różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z bramy aplikacji. Niektóre z tych dzienników dostępne za pośrednictwem portalu hello. Wszystkie dzienniki można wyodrębnić z magazynu obiektów Blob platformy Azure i wyświetlane w różnych narzędzi, takich jak [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md), Excel i Power BI. Użytkownik może dowiedzieć się więcej o hello różne typy dzienników z następującej listy hello:

* **Dziennik aktywności**: można użyć [Dzienniki aktywności Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako dzienniki inspekcji i operacyjne dzienniki) tooview wszystkie operacje, które są przesyłane tooyour subskrypcji platformy Azure i ich stan. Wpisy dziennika aktywności są zbierane domyślnie i można je przeglądać w hello portalu Azure.
* **Dziennik dostępu**: można użyć wzorce dostępu do tego dziennika tooview bramy aplikacji i analizować i wylogowywanie ważne informacje, takie jak wywołującego hello IP żądanego adresu URL, czas oczekiwania na odpowiedź, kod powrotny i bajtów. Dziennik dostępu są gromadzone co 300 sekund. Ten dziennik zawiera jeden rekord dla każdego wystąpienia bramy aplikacji. wystąpienie bramy aplikacji Hello można zidentyfikować przez właściwość instanceId hello.
* **Dziennik wydajności**: można użyć tego tooview dziennika, jak działają wystąpieniach bramy aplikacji. Ten dziennik zawiera informacje o wydajności dla każdego wystąpienia, w tym całkowita liczba żądań obsłużonych, przepływność w bajtach, całkowita liczba żądań obsłużonych, liczba nieudanych żądań, a liczba wystąpień zaplecza dobrej kondycji i złej kondycji. Dziennik wydajności są zbierane co 60 sekund.
* **Dziennik zapory**: można użyć tego dziennika tooview hello żądań, które są rejestrowane za pośrednictwem bramy aplikacji skonfigurowanej z zapory aplikacji sieci web hello Tryb wykrywania i zapobiegania.

> [!NOTE]
> Dzienniki są dostępne tylko w przypadku wdrożono w modelu wdrażania usługi Azure Resource Manager hello zasobów. Nie można używać dzienników zasobów w hello klasycznego modelu wdrażania. Aby lepiej zrozumieć hello dwa modele, zobacz hello [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.

Są trzy opcje do przechowywania dzienników:

* **Konto magazynu**: konta magazynu są najlepiej nadaje się do dzienników podczas dzienniki są przechowywane przez dłuższy czas i sprawdzić, w razie potrzeby.
* **Centra zdarzeń**: Event hubs to doskonałe rozwiązanie dla integracji z innych informacji o zabezpieczeniach i narzędzi do zarządzania zdarzenia (SEIM) tooget alertów dotyczących zasobów.
* **Zaloguj się Analytics**: analizy dzienników najlepiej nadaje się do ogólnego monitorowania w czasie rzeczywistym aplikacji lub analizowania trendów.

### <a name="enable-logging-through-powershell"></a>Włącz rejestrowanie za pomocą programu PowerShell

Rejestrowanie aktywności jest automatycznie włączona dla każdego zasobu usługi Resource Manager. Należy włączyć dostęp i toostart rejestrowania wydajności zbierania danych hello dostępne za pośrednictwem tych dzienników. tooenable rejestrowanie użycia hello następujące kroki:

1. Należy zwrócić uwagę identyfikatorów zasobów konta magazynu, w którym są przechowywane dane dziennika hello. Ta wartość ma formę hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Storage/storageAccounts/\<nazwy konta magazynu\>. Można użyć dowolnego konta magazynu w ramach subskrypcji. Witaj toofind portalu Azure można użyć tych informacji.

    ![Portalu: identyfikator zasobu dla konta magazynu](./media/application-gateway-diagnostics/diagnostics1.png)

2. Należy pamiętać, dla którego włączono rejestrowanie identyfikator zasobu bramy aplikacji. Ta wartość ma formę hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Network/applicationGateways/\<bramy aplikacji Nazwa\>. Witaj toofind portalu można użyć tych informacji.

    ![Portalu: identyfikator zasobu bramy aplikacji](./media/application-gateway-diagnostics/diagnostics2.png)

3. Włącz rejestrowanie diagnostyczne za pomocą następującego polecenia cmdlet programu PowerShell hello:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Dzienniki aktywności nie wymagają oddzielnego konta magazynu. Użycie Hello magazynu do dostępu do rejestrowania i wydajności wiąże opłaty za usługę.

### <a name="enable-logging-through-hello-azure-portal"></a>Włącz rejestrowanie za pośrednictwem hello portalu Azure

1. Witaj portalu Azure, Znajdź zasobu i kliknij przycisk **dzienniki diagnostyczne**.

   Brama aplikacji dostępne są trzy dzienniki:

   * Dziennik dostępu
   * Dziennika wydajności
   * Dziennik zapory

2. toostart zbierania danych, kliknij przycisk **Włącz diagnostykę**.

   ![Włączanie diagnostyki][1]

3. Witaj **ustawień diagnostycznych** blok zawiera ustawienia hello hello dzienników diagnostycznych. W tym przykładzie analizy dzienników przechowuje hello dzienników. Kliknij przycisk **Konfiguruj** w obszarze **analizy dzienników** tooconfigure obszaru roboczego. Można również użyć centra zdarzeń i przechowywania konta toosave hello dzienników diagnostycznych.

   ![Uruchamia proces konfiguracji hello][2]

4. Wybierz istniejący obszar roboczy Operations Management Suite (OMS) lub Utwórz nową. W tym przykładzie użyto jednego z istniejących.

   ![Opcje dla obszarów roboczych OMS][3]

5. Potwierdź ustawienia hello, a następnie kliknij przycisk **zapisać**.

   ![Blok ustawień diagnostycznych z zaznaczenia][4]

### <a name="activity-log"></a>Dziennik aktywności

Platforma Azure generuje dziennik aktywności hello domyślnie. Dzienniki Hello są zachowywane przez 90 dni w magazynie Azure dzienniki zdarzeń hello. Dowiedz się więcej o tych dzienników, odczytując hello [wyświetlanie zdarzeń i dziennika aktywności](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.

### <a name="access-log"></a>Dziennik dostępu

Dziennik dostępu Hello jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzednich krokach hello. Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello. Każdy dostęp brama aplikacji w jest rejestrowany w formacie JSON, jak pokazano w hello poniższy przykład:


|Wartość  |Opis  |
|---------|---------|
|Identyfikator wystąpienia     | Brama aplikacji w wystąpienia tego żądania hello obsługiwane.        |
|ClientIP     | Źródłowy adres IP dla żądania hello.        |
|clientPort     | Źródłowy port hello żądania.       |
|HttpMethod     | Metoda HTTP używana przez hello żądania.       |
|requestUri     | Identyfikator URI hello odebrane żądanie.        |
|RequestQuery     | **Serwer routingu**: Wysłano żądanie hello wystąpienie puli zaplecza. </br> **X-AzureApplicationGateway-dziennika-ID**: Identyfikator korelacji jest używany dla hello żądania. Może być używane tootroubleshoot problemy ruchu na serwerach wewnętrznych hello. </br>**Stan serwera**: kod odpowiedzi HTTP bramy aplikacji otrzymane z wewnętrznego hello.       |
|Agent użytkownika     | Agent użytkownika z nagłówka żądania hello HTTP.        |
|httpStatus     | Kod stanu HTTP zwrócony toohello klienta z bramy aplikacji.       |
|Wersja_http     | Wersja hello żądania HTTP.        |
|ReceivedBytes     | Rozmiar pakietów otrzymanych w bajtach.        |
|SentBytes| Rozmiar pakietu wysłane w bajtach.|
|Właściwość timeTaken| Długość czasu (w milisekundach), który zajmuje toobe żądania, przetwarzane i jego toobe odpowiedzi wysyłane. Jest on obliczany jako interwał powitania od czasu powitania po bramy aplikacji odbiera pierwszy bajt hello czas toohello żądania HTTP podczas odpowiedź hello wysyłania zakończenie operacji. Jest ważne toonote, który zazwyczaj hello Time-Taken pole zawiera czas hello podróży za pośrednictwem sieci hello pakietów hello żądań i odpowiedzi. |
|SSL| Określa, czy pule zaplecza toohello komunikacji używać protokołu SSL. Prawidłowe wartości to on i off.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Dziennika wydajności

dziennik wydajności Hello jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzednich krokach hello. Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello. dane dzienników wydajności Hello jest generowana w 1-minutowych interwałach. rejestrowane są następujące dane Hello:


|Wartość  |Opis  |
|---------|---------|
|Identyfikator wystąpienia     |  Dla wydajności, które dane są generowane wystąpienia bramy aplikacji. Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.        |
|healthyHostCount     | Liczba hostów dobrej kondycji w puli zaplecza hello.        |
|unHealthyHostCount     | Liczba hostów złej kondycji w puli zaplecza hello.        |
|RequestCount     | Liczba żądań obsłużonych.        |
|Czas oczekiwania | Czas oczekiwania (w milisekundach) żądań od toohello wystąpienia hello zaplecza pełniącą hello żądania. |
|failedRequestCount| Liczba żądań zakończonych niepowodzeniem.|
|Przepływność| Średnia przepustowość od czasu ostatniego dziennika hello, mierzony w bajtach na sekundę.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Czas oczekiwania jest obliczana na podstawie hello godzinę hello pierwszy bajt żądania hello HTTP odebrane toohello czas wysłania ostatniego bajtu hello hello odpowiedzi HTTP. Jego hello sumę hello brama aplikacji w czasie przetwarzania oraz hello ponownie toohello sieci koszt końca, oraz czas hello hello zaplecza przyjmuje tooprocess hello żądania.

### <a name="firewall-log"></a>Dziennik zapory

dziennik zapory Hello jest generowany tylko wtedy, gdy włączono dla każdej bramy aplikacji, zgodnie z opisem w poprzednich krokach hello. Ten dziennik wymaga również, że tej zapory aplikacji sieci web hello jest skonfigurowany dla bramy aplikacji. Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello. rejestrowane są następujące dane Hello:


|Wartość  |Opis  |
|---------|---------|
|Identyfikator wystąpienia     | Zapory, które dane są generowane wystąpienia bramy aplikacji. Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.         |
|clientIp     |   Źródłowy adres IP dla żądania hello.      |
|clientPort     |  Źródłowy port hello żądania.       |
|requestUri     | Adres URL hello odebrane żądanie.       |
|ruleSetType     | Typ zestawu reguł. wartość dostępna Hello jest OWASP.        |
|ruleSetVersion     | Wersja używanego zestawu reguł. Dostępne wartości to 2.2.9 i 3.0.     |
|RuleId     | Identyfikator reguły hello wyzwolenie zdarzenia.        |
|Komunikat     | Przyjazna dla użytkownika komunikat dla hello wyzwolenie zdarzenia. Bardziej szczegółowe informacje znajdują się w sekcji szczegółów hello.        |
|Akcja     |  Nie wykonano akcji na powitania żądania. Dostępne wartości to zablokowany, a dozwolone.      |
|Lokacji     | Witryna, dla których hello dziennika został wygenerowany. Obecnie tylko Global jest na liście, ponieważ reguły są globalne.|
|Szczegóły     | Szczegóły hello wyzwolenie zdarzenia.        |
|details.Message     | Opis reguły hello.        |
|details.Data     | Dane dotyczące określonego znaleziono w żądaniu reguły hello dopasowany.         |
|details.File     | Plik konfiguracji zawiera reguły hello.        |
|details.Line     | Numer wiersza w pliku konfiguracyjnym hello, która wyzwoliła hello zdarzeń.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Wyświetlanie i analizowanie hello dziennik aktywności

Można wyświetlać i analizować dane dzienników działania przy użyciu dowolnej z następujących metod hello:

* **Narzędzia Azure**: pobieranie informacji z dziennika aktywności hello za pomocą programu Azure PowerShell, hello Azure CLI hello interfejsu API REST Azure lub hello portalu Azure. Instrukcje krok po kroku dla każdej metody wyszczególnione w hello [operacji działania za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.
* **Power BI**: Jeśli nie masz jeszcze [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie. Za pomocą hello [Dzienniki aktywności Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), można analizować danych za pomocą wstępnie skonfigurowanych pulpity nawigacyjne, które można użyć jako jest lub dostosować je.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Wyświetlanie i analizowanie hello dostępu, wydajności i dzienniki zapory

Azure [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md) może zbierać pliki dziennika zdarzeń i licznik hello z konta magazynu obiektów Blob. Zawiera wizualizacje i tooanalyze możliwości wyszukiwania zaawansowanego dzienników.

Można także połączyć tooyour konta magazynu i pobrać wpisów dziennika JSON hello dzienników dostępu i wydajności. Po pobraniu hello pliki w formacie JSON można przekonwertować tooCSV i wyświetlić je w programie Excel, usłudze Power BI lub innych narzędzi wizualizacji danych.

> [!TIP]
> Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć hello [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.
> 
> 

## <a name="metrics"></a>Metryki

Metryki są funkcją dla niektórych zasobów platformy Azure, w którym liczniki wydajności można przeglądać w portalu hello. Bramy aplikacji jedna metryka jest teraz dostępna. Ta metryka jest przepływność i widoczny w portalu hello. Przeglądaj tooan aplikacji bramy, a następnie kliknij przycisk **metryki**. tooview hello wartości, wybierz opcję przepływność w hello **dostępne metryki** sekcji. Hello po obrazu przedstawiono przykład z filtrami hello w innym czasie zakresów można toodisplay hello danych.

![Widoku metryki z filtrami][5]

Zobacz toosee bieżącą listę metryki, [obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Reguły alertów

Można uruchomić reguły alertów w oparciu metryki dla zasobu. Na przykład alert można wywołać elementu webhook lub wiadomości e-mail administratora, jeśli hello przepływność bramy aplikacji hello jest powyżej, poniżej lub w wartości progowej przez określony czas.

Poniższy przykład Hello przeprowadzi Cię przez proces tworzenia reguły alertu wysyłanej wiadomości e-mail administratora tooan po naruszeń przepływność a próg:

1. Kliknij przycisk **Dodaj alert metryki** tooopen hello **Dodaj regułę** bloku. Zapewnia także łączność tego bloku z hello metryki bloku.

   ![Przycisk "Dodaj metryki alert"][6]

2. Na powitania **Dodaj regułę** bloku wypełniania hello nazwa warunku, powiadom sekcje i kliknij przycisk **OK**.

   * W hello **warunku** selektora, wybierz jedną z wartości hello czterech: **większe**, **większy lub równy**, **mniej niż**, lub  **Mniejsze niż lub równe**.

   * W hello **okres** selektora, wybierz okres od 5 minut too6 godzin.

   * W przypadku wybrania **E-mail właściciele, współautorzy i czytelnicy**, powitalne wiadomości e-mail może być dynamiczny na podstawie hello użytkowników, którzy mają dostęp do zasobów toothat. W przeciwnym razie możesz podać rozdzielana przecinkami lista użytkowników w hello **email(s) dodatkowe administratora** pole.

   ![Dodaj regułę bloku][7]

W przypadku naruszenia progu hello dociera do wiadomości e-mail, która jest podobne toohello, co w powitania po obrazu:

![Wiadomości e-mail w przypadku naruszenia progu][8]

Po utworzeniu metryki alert zostanie wyświetlona lista alertów. Zapewnia przegląd wszystkich hello reguł alertów.

![Lista alertów i reguł][9]

toolearn więcej informacji na temat powiadomień o alertach, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand więcej informacji na temat elementów webhook i jak ich używać z alertami, odwiedź stronę [skonfigurować elementu webhook na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Następne kroki

* Wizualizuj w dziennikach zdarzeń i liczników przy użyciu [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md).
* [Wizualizuj dziennik aktywności platformy Azure z usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.
* [Przeglądać i analizować Dzienniki aktywności platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
