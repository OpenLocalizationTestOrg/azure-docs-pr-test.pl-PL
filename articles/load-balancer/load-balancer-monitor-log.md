---
title: "aaaMonitor operacje, zdarzenia i liczniki dla usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable alertów zdarzeń i sondy kondycji stanu rejestrowania dla usługi równoważenia obciążenia Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Analiza dzienników dotyczących usługi Azure Load Balancer

Można użyć różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługi równoważenia obciążenia. Niektóre z tych dzienników jest możliwy za pośrednictwem portalu hello. Wszystkie dzienniki można wyodrębnić z magazynu obiektów blob platformy Azure i wyświetlane w różnych narzędzi, takich jak program Excel i Power BI. Użytkownik może Dowiedz się więcej o hello różne typy dzienników z poniższej listy hello.

* **Dzienniki inspekcji:** można użyć [dzienników inspekcji platformy Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako operacyjne dzienniki) tooview wszystkie operacje są przesłane tooyour subskrypcji platformy Azure i ich stan. Dzienniki inspekcji są domyślnie włączone i mogą być wyświetlane w portalu Azure hello.
* **Dzienniki zdarzeń alertów:** można użyć tego dziennika tooview alerty rasied przez hello równoważenia obciążenia. Stan powitania dla usługi równoważenia obciążenia hello są gromadzone co pięć minut. Ten dziennik napisano tylko, jeśli zdarzenia alertu modułu równoważenia obciążenia jest wywoływane.
* **Dzienniki badania kondycji:** można użyć tego dziennika tooview problemach przez użytkownika sondy kondycji, takich jak hello liczbę wystąpień w puli zaplecza, które nie są odbierane żądań z modułu równoważenia obciążenia hello spowodowane błędami sondy kondycji. Ten dziennik jest zapisywany toowhen nastąpiła zmiana stanu sondy kondycji hello.

> [!IMPORTANT]
> Zaloguj się analytics jest obecnie obsługiwane tylko w przypadku internetowy usług równoważenia obciążenia. Dzienniki są dostępne tylko dla zasobów wdrożone w modelu wdrażania usługi Resource Manager hello. Nie można używać dzienników zasobów w hello klasycznego modelu wdrażania. Aby uzyskać więcej informacji na temat modeli wdrażania hello, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Włącz rejestrowanie

Rejestrowanie inspekcji jest automatycznie włączona dla każdego zasobu usługi Resource Manager. Należy tooenable zdarzeń i toostart rejestrowania sondy kondycji zbierania danych hello dostępne za pośrednictwem tych dzienników. Użyj hello następujące kroki tooenable rejestrowania.

Logowanie toohello [portalu Azure](http://portal.azure.com). Jeśli nie masz już usługę równoważenia obciążenia, [tworzenia modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) przed kontynuowaniem.

1. W portalu powitania kliknij **Przeglądaj**.
2. Wybierz **usługi równoważenia obciążenia**.

    ![Portal — moduł równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Wybierz istniejący moduł równoważenia obciążenia >> **wszystkie ustawienia**.
4. Na powitania po prawej stronie okna dialogowego hello pod nazwą hello hello usługi równoważenia obciążenia, przewiń zbyt**monitorowanie**, kliknij przycisk **diagnostyki**.

    ![Portal — ustawienia usługi równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. W hello **diagnostyki** okienku w obszarze **stan**, wybierz pozycję **na**.
6. Kliknij przycisk **konta magazynu**.
7. W obszarze **DZIENNIKI**, wybrać istniejące konto magazynu lub Utwórz nową. Użyj toodetermine suwaka hello ilu dniach danych zdarzenia będą przechowywane w dziennikach zdarzeń hello. 
8. Kliknij pozycję **Zapisz**.

    ![Portal — dzienniki diagnostyczne](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Dzienniki inspekcji nie wymagają oddzielnego konta magazynu. Witaj wykorzystania przestrzeni dyskowej na zdarzenie oraz kondycji sondowania rejestrowania będą naliczane opłaty za usługę.

## <a name="audit-log"></a>Dziennik inspekcji

Dziennik inspekcji Hello jest generowany domyślnie. Dzienniki Hello są zachowywane przez 90 dni w magazynie dzienniki zdarzeń platformy Azure. Dowiedz się więcej o tych dzienników, odczytując hello [wyświetlania zdarzeń i dzienniki inspekcji](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.

## <a name="alert-event-log"></a>Dziennik zdarzeń alertów

Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych usługi równoważenia obciążenia. Hello zdarzenia są rejestrowane w formacie JSON i przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello. Witaj poniżej znajduje się przykład zdarzenia.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Pokazuje hello output Hello JSON *eventname* właściwość, która będzie opisywać hello Przyczyna hello modułu równoważenia obciążenia utworzony alert. W takim przypadku hello alert wygenerowany został powodu tooTCP portu wyczerpania spowodowane przez źródło, który ogranicza IP translatora adresów Sieciowych (SNAT).

## <a name="health-probe-log"></a>Dziennik badania kondycji

Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych obciążenia równoważenia zgodnie z opisem powyżej. Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello. Kontener o nazwie "insights dzienniki loadbalancerprobehealthstatus" jest tworzony i jest rejestrowany hello następujące dane:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

dane wyjściowe JSON Hello zawiera hello właściwości pola hello podstawowe informacje dotyczące stanu kondycji hello sondowania. Witaj *dipDownCount* właściwość pokazuje hello całkowita liczba wystąpień na zaplecza hello, które nie są odbierane ruchu sieciowego powodu toofailed sondowania odpowiedzi.

## <a name="view-and-analyze-hello-audit-log"></a>Wyświetlanie i analizowanie dzienników inspekcji hello

Można wyświetlać i analizować dane dzienników inspekcji przy użyciu dowolnej z następujących metod hello:

* **Narzędzia platformy Azure:** pobieranie informacji z dzienników inspekcji hello za pomocą programu Azure PowerShell, hello Azure interfejsu wiersza polecenia (CLI), hello interfejsu API REST Azure lub hello Azure w wersji zapoznawczej portalu. Instrukcje krok po kroku dla każdej metody wyszczególnione w hello [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.
* **Usługa Power BI:** Jeśli jeszcze nie masz [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie. Przy użyciu hello [dzienników inspekcji platformy Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)można analizować danych za pomocą wstępnie skonfigurowanych pulpitów nawigacyjnych i można dostosowywać widoki toosuit wymagań.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Wyświetlanie i analizowanie hello sondy kondycji i dziennika zdarzeń

Potrzebny jest magazyn tooyour tooconnect konta i pobieranie hello wpisy dziennika JSON dla dziennikami sondy kondycji i zdarzeń. Po pobraniu hello pliki w formacie JSON można konwertować tooCSV i widoku w programie Excel, usłudze PowerBI lub inne narzędzie do wizualizacji danych.

> [!TIP]
> Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć hello [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Wizualizuj dzienników inspekcji Azure przy użyciu usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.
* [Wyświetlanie i analizowanie dzienników inspekcji platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.

## <a name="next-steps"></a>Następne kroki

[Opis sond modułu równoważenia obciążenia](load-balancer-custom-probe-overview.md)
