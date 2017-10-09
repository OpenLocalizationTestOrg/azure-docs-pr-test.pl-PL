---
title: "Zarządzanie interfejsami API Azure Monitor aaaMonitor | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor Azure API Management usługi przy użyciu monitora Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Monitor interfejsu API zarządzania z Monitorem systemu Azure
Azure Monitor jest usługą platformy Azure, który udostępnia jedno źródło do monitorowania wszystkich zasobów na platformie Azure. Z monitorem Azure można zwizualizować, zapytania, trasy, archiwizacji i podejmuj działania na powitania metryki i dzienników pochodzących z zasobów platformy Azure, takich jak zarządzanie interfejsami API. 

Witaj, po wideo pokazuje, jak toomonitor zarządzanie interfejsami API Azure monitora. Aby uzyskać więcej informacji na temat Monitora Azure, zobacz [Rozpoczynanie pracy z monitorem Azure]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Metryki
Zarządzanie interfejsami API obecnie emituje pięć metryki i planujemy tooadd więcej w przyszłości hello. Te metryki są emitowane co minutę, umożliwiając niemal w czasie rzeczywistym wgląd w stan hello i kondycji swoje interfejsy API. Poniżej znajduje się podsumowanie hello metryki:
* Całkowita liczba żądań bramy: hello liczba interfejsu API żądań w okresie hello. 
* Pomyślnych żądań bramy: hello liczba żądań interfejsu API, które otrzymały pomyślne kody odpowiedzi HTTP, w tym 304 307 i mniejszego niż 301 (na przykład 200). 
* Nieudane żądania bramy: hello liczba żądań interfejsu API, które odebrano błędną kody odpowiedzi HTTP, w tym 400 i niczego większych niż 500.
* Nieautoryzowanych żądań bramy: hello liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP 401, 403 i 429 w tym. 
* Inne żądania bramy: hello liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP, które nie należą tooany hello poprzedzających kategorii (na przykład 418).

Dostępne metryki w usłudze API Management lub metryki dostęp do wszystkich zasobów platformy Azure w monitorze Azure. metryki tooview w usłudze API Management:
1. Otwórz hello portalu Azure.
2. Przejdź usługi Zarządzanie interfejsami API tooyour.
3. Kliknij przycisk **metryki**.

![Metryki bloku][metrics-blade]

Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [omówienie metryki].

## <a name="activity-logs"></a>Dzienniki aktywności
Dzienniki aktywności zapewniają wgląd w operacji hello, wykonywane na usługi Zarządzanie interfejsami API. Został on wcześniej znana jako "dzienników inspekcji" lub "operacyjne dzienniki". Przy użyciu dzienników działania, można określić hello ", co, która i kiedy" dla operacji (PUT, POST, DELETE) podejmowaną w odniesieniu do usługi API Management żadnego zapisu. 

> [!NOTE]
> Dzienniki aktywności nie obejmują operacji odczytu (GET) lub operacje wykonywane w hello klasyczny Portal wydawcy lub przy użyciu hello oryginalnego interfejsów API Management.

Dostęp do dzienników aktywności w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure. rejestruje działania tooview w usłudze API Management:
1. Otwórz hello portalu Azure.
2. Przejdź usługi Zarządzanie interfejsami API tooyour.
3. Kliknij przycisk **dziennik aktywności**.

![Blok Dzienniki aktywności][activity-logs-blade]

Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [omówienie Dzienniki aktywności].

## <a name="alerts"></a>Alerty
Można skonfigurować alerty tooreceive oparte na dzienniki metryki i działania. Azure Monitor pozwala tooconfigure toodo alertu powitania po wyzwala:

* Wyślij wiadomość e-mail z powiadomieniem
* Wywołanie elementu webhook
* Wywołanie aplikacji logiki platformy Azure

Reguły alertów można skonfigurować w usłudze API Management lub w monitorze Azure. tooconfigure ich w usłudze API Management: 
1. Otwórz hello portalu Azure.
2. Przejdź usługi Zarządzanie interfejsami API tooyour.
3. Kliknij przycisk **reguły alertów**.

![Blok reguły alertów][alert-rules-blade]

Aby uzyskać więcej informacji o korzystaniu z alertami, zobacz [Przegląd alertów].

## <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Dzienniki diagnostyczne zawierają zaawansowane informacje o operacje i błędy, które są ważne w przypadku inspekcji, a także rozwiązywania problemów. Dzienniki diagnostyczne różnią się od Dzienniki aktywności. Dzienniki aktywności wgląd w działania hello, wykonywane na zasobów platformy Azure. Dzienniki diagnostyczne zapewniają wgląd w operacje, w zasobie wykonanie samego.

Zarządzanie interfejsami API zawiera obecnie diagnostyki dzienniki (umieścić w zadaniu wsadowym co godzinę) o poszczególnych interfejsu API żądania z każdego wpisu o hello następujące struktury:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

Można uzyskać dostępu do dzienników diagnostycznych w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure. dzienniki diagnostyczne tooview w usłudze API Management:
1. Otwórz hello portalu Azure.
2. Przejdź usługi Zarządzanie interfejsami API tooyour.
3. Kliknij przycisk **dziennik diagnostyczny**.

![Blok dzienników diagnostycznych][diagnostic-logs-blade]

Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [Przegląd dzienników diagnostycznych].

## <a name="next-step"></a>Następny krok

* [Rozpoczynanie pracy z monitorem Azure]
* [omówienie metryki]
* [omówienie Dzienniki aktywności]
* [Przegląd dzienników diagnostycznych]
* [Przegląd alertów]

[Rozpoczynanie pracy z monitorem Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md
[omówienie metryki]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[omówienie Dzienniki aktywności]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Przegląd dzienników diagnostycznych]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Przegląd alertów]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
