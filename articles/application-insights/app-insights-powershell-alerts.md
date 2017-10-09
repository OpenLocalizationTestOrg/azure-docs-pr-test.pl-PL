---
title: "aaaUse Powershell tooset alertów w usłudze Application Insights | Dokumentacja firmy Microsoft"
description: "Zautomatyzować konfigurację usługi Application Insights tooget powiadomienia dotyczące zmiany metryki."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Użyj programu PowerShell tooset alertów w usłudze Application Insights
Można zautomatyzować konfigurację hello [alerty](app-insights-alerts.md) w [usługi Application Insights](app-insights-overview.md).

Ponadto można [ustawić tooautomate elementów webhook alertu tooan odpowiedzi](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Jeśli chcesz toocreate zasobów i alerty o hello takie same czasu, należy wziąć pod uwagę [przy użyciu szablonu usługi Azure Resource Manager](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Jednorazowej konfiguracji
Jeśli nie użyto programu PowerShell z subskrypcją platformy Azure przed:

Instalowanie modułu Azure Powershell hello na maszynie hello miejscu toorun hello skryptów.

* Zainstaluj [Instalatora platformy sieci Web firmy Microsoft (w wersji 5 lub nowszej)](http://www.microsoft.com/web/downloads/platform.aspx).
* Użyj go tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Połącz tooAzure
Uruchom program Azure PowerShell i [połączenia subskrypcji tooyour](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Uzyskiwanie alertów
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Dodawanie alertu
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Przykład 1
Wyślij mi wiadomość e-mail, jeśli żądania tooHTTP odpowiedzi serwera hello, średnio ponad 5 minut, jest mniejsza niż 1 sekunda. Moje zasobu usługi Application Insights jest nazywany IceCreamWebApp i jest w grupie zasobów firmy Fabrikam. Jestem właścicielem hello hello subskrypcji platformy Azure.

Witaj identyfikator GUID jest Identyfikatorem subskrypcji hello (nie hello klucza instrumentacji aplikacji hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Przykład 2
Używana aplikacja, I użyj [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport metrykę o nazwie "salesPerHour." Wyślij wiadomość e-mail toomy współpracowników, jeśli "salesPerHour" spadnie poniżej 100, średnio ponad 24 godzin.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

zasada może służyć do Metryka hello Hello zgłosił za pomocą hello [parametru pomiaru](app-insights-api-custom-events-metrics.md#properties) wywołania innego śledzenia, takie jak TrackEvent lub trackPageView.

## <a name="metric-names"></a>Nazwy metryki
| Nazwa metryki | Nazwa ekranu | Opis |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Wyjątki przeglądarki |Liczba nieprzechwyconych wyjątków zgłoszonych w przeglądarce hello. |
| `basicExceptionServer.count` |Wyjątki serwera |Liczba nieobsługiwanych wyjątków zgłoszonych przez aplikację hello |
| `clientPerformance.clientProcess.value` |Czas przetwarzania klienta |Czas między odebraniem ostatniego bajtu hello dokumentu do momentu załadowania modelu DOM hello. Żądania asynchroniczne mogą nadal być przetwarzane. |
| `clientPerformance.networkConnection.value` |Czas połączenia sieciowego podczas ładowania strony |Czas hello przeglądarki przyjmuje tooconnect toohello sieci. Może być równa 0, jeśli w pamięci podręcznej. |
| `clientPerformance.receiveRequest.value` |Odbieranie czas odpowiedzi |Czas między przeglądarki wysyłania żądania toostarting tooreceive odpowiedzi. |
| `clientPerformance.sendRequest.value` |Wyślij czas żądania |Czas trwania żądania toosend przeglądarki. |
| `clientPerformance.total.value` |Czas ładowania strony przeglądarki |Czas od wysłania żądania użytkownika do modelu DOM, arkuszy stylów, skryptów i obrazów są ładowane. |
| `performanceCounter.available_bytes.value` |Dostępna pamięć |Pamięć fizyczna dostępna natychmiast dla procesów lub do wykorzystania przez system. |
| `performanceCounter.io_data_bytes_per_sec.value` |Szybkość przetwarzania We/Wy |Całkowita liczba bajtów na drugi odczytu i zapisywane toofiles, sieci i urządzeń. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |szybkość wyjątku |Wyjątków zgłaszanych na sekundę. |
| `performanceCounter.percentage_processor_time.value` |Proces Procesora |Procent Hello wszystkich wątków procesów używanych przez hello procesora tooexecution instrukcje dla procesu aplikacji hello czas, który upłynął. |
| `performanceCounter.percentage_processor_total.value` |Czas procesora |Hello wartość procentową czasu hello procesor spędza w Aktywne wątki. |
| `performanceCounter.process_private_bytes.value` |Bajtów prywatnych procesu |Pamięć przypisana wyłącznie toohello monitorowane procesów aplikacji. |
| `performanceCounter.request_execution_time.value` |Czas wykonania żądania programu ASP.NET |Czas wykonywania hello ostatniego żądania. |
| `performanceCounter.requests_in_application_queue.value` |ASP.NET żądań w kolejce wykonywania |Długość kolejki żądań aplikacji hello. |
| `performanceCounter.requests_per_sec.value` |Współczynnik żądań ASP.NET |Częstotliwość wszystkich żądań aplikacji toohello na sekundę z platformy ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Błędy zależności |Liczba nieudanych wywołań powitania serwera aplikacji tooexternal zasobów. |
| `request.duration` |Czas odpowiedzi serwera |Czas między odebraniem żądania HTTP i zakończeniem wysyłania odpowiedzi hello. |
| `request.rate` |Współczynnik żądań |Częstotliwość wszystkich żądań aplikacji toohello na sekundę. |
| `requestFailed.count` |Żądań zakończonych niepowodzeniem |Liczba żądań HTTP które wywołały kod odpowiedzi > = 400 |
| `view.count` |Liczba wyświetleń strony |Liczba żądań użytkowników klientów dla strony sieci web. Ruchu syntetycznego jest odfiltrowana. |
| {niestandardowe metryki nazwę} |{Nazwa metryki} |Wartość metryki zgłoszone przez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) lub hello [pomiarów parametru wywołania śledzenia](app-insights-api-custom-events-metrics.md#properties). |

metryki Hello są wysyłane przez moduły różnych telemetrii:

| Metryki grupy | Moduł zbierający |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>wyświetl |[Kod JavaScript przeglądarki](app-insights-javascript.md) |
| performanceCounter |[Wydajność](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Zależność](app-insights-configuration-with-applicationinsights-config.md) |
| żądanie,<br/>requestFailed |[Żądanie serwera](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>elementów webhook
Możesz [zautomatyzować alertu tooan odpowiedzi](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure będzie wywoływać adres sieci web wybranych przez użytkownika, gdy zostanie zgłoszony alert.

## <a name="see-also"></a>Zobacz też
* [Skrypt tooconfigure usługi Application Insights](app-insights-powershell-script-create-resource.md)
* [Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów](app-insights-powershell.md)
* [Automatyzowanie sprzężenia Insights tooApplication Diagnostyka pakietu Microsoft Azure](app-insights-powershell-azure-diagnostics.md)
* [Automatyzowanie alertu tooan odpowiedzi](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
