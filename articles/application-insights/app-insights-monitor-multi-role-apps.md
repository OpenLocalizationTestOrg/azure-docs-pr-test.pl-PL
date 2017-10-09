---
title: "aaaAzure usługi Application Insights Obsługa wielu składników, mikrousług i kontenery | Dokumentacja firmy Microsoft"
description: "Monitorowanie aplikacji, które składają się z wielu składników lub ról, wydajności i użycia."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Monitorowanie wielu składnika aplikacji za pomocą usługi Application Insights (wersja zapoznawcza)

Można monitorować aplikacje, które składają się z wielu składników serwera, ról lub usług z [Azure Application Insights](app-insights-overview.md). Hello kondycji składników hello i hello relacji między nimi są wyświetlane na mapie jednej aplikacji. Można śledzić poszczególnych działań przez kilka składników z automatycznego korelacji HTTP. Diagnostyka kontenera można zintegrowany i skorelowane z danych telemetrycznych aplikacji. Użyj pojedynczego zasobu usługi Application Insights dla wszystkich składników aplikacji hello. 

![Mapowanie wielu składnika aplikacji](./media/app-insights-monitor-multi-role-apps/app-map.png)

Używamy "component" toomean tutaj dowolnej działa części dużych aplikacji. Na przykład typowa aplikacja biznesowa może składać się z kodu klienta działający w przeglądarkach sieci web, mówić tooone lub usług kończyć więcej usług aplikacji sieci web, które z kolei użyć ponownie. Składniki serwera może być obsługiwana lokalnie na powitania chmury, może być Azure role sieci web i proces roboczy lub może działać w kontenerach, takich jak Docker lub sieci szkieletowej usług. 

### <a name="sharing-a-single-application-insights-resource"></a>Udostępnianie pojedynczego zasobu usługi Application Insights 

Witaj klucza technika tutaj jest toosend telemetrii od każdego składnika w Twojej aplikacji toohello tego samego zasobu usługi Application Insights, ale użyj hello `cloud_RoleName` składniki toodistinguish właściwości, gdy jest to konieczne. zestaw SDK usługi Application Insights Hello dodaje hello `cloud_RoleName` Emituj właściwości toohello telemetrii składników. Na przykład hello SDK doda nazwa witryny sieci web lub usługi roli nazwa toohello `cloud_RoleName` właściwości. Można zastąpić tę wartość z telemetryinitializer. Mapowanie aplikacji Hello używa hello `cloud_RoleName` właściwości tooidentify hello składników na mapie hello.

Aby uzyskać więcej informacji o tym, jak zastąpić hello `cloud_RoleName` Zobacz właściwość [dodać właściwości: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

W niektórych przypadkach to nie może być odpowiednie, a lepiej toouse oddzielnych zasobów dla różnych grup składników. Na przykład może być konieczne toouse różne zasoby do zarządzania lub rozliczeń do celów. Korzystanie z osobnych zasobów oznacza, że nie wyświetlone wszystkie składniki hello wyświetlany w jednym mapowaniu aplikacji; oraz że nie można zbadać elementów w [Analytics](app-insights-analytics.md). Masz również tooset hello oddzielnych zasobów.

Z tym ostrzeżenie przyjmiemy w hello pozostałej części tego dokumentu oznaczający toosend danych z wielu składników tooone zasobu usługi Application Insights.

## <a name="configure-multi-component-applications"></a>Konfigurowanie wielu składnika aplikacji

Mapowanie wielu składnika aplikacji tooget, należy tooachieve tych celów:

* **Instalowanie najnowszej wersji wstępnej hello** pakiet usługi Application Insights w poszczególnych składników aplikacji hello. 
* **Udostępnij pojedynczy zasób usługi Application Insights** dla hello wszystkich składników aplikacji.
* **Włączyć usługi roli aplikacji mapy** w bloku podglądy hello.

Skonfiguruj poszczególnych składników aplikacji przy użyciu metody odpowiedniej powitania dla jego typu. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Zainstaluj najnowszy pakiet wersji wstępnej hello

Zaktualizuj lub zainstaluj hello wgląd w aplikację pakietów hello projektu dla każdego składnika serwera. Jeśli używasz programu Visual Studio:

1. Kliknij prawym przyciskiem myszy projekt i wybierz **Zarządzaj pakietami NuGet**. 
2. Wybierz **Uwzględnij wersję wstępną**.
3. Jeśli usługi Application Insights pakiety są widoczne w aktualizacji, zaznacz je. 

    W przeciwnym razie przeglądania i instalowania hello odpowiedniego pakietu:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - składników uruchomiony jako gość plików wykonywalnych i kontenery Docker uruchamiania aplikacji w sieci szkieletowej usług
    * Microsoft.ApplicationInsights.ServiceFabric.Native - niezawodnych usług w aplikacjach ServiceFabric
    * Microsoft.ApplicationInsights.Kubernetes składników działających w Docker na Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Udostępnij pojedynczy zasób usługi Application Insights

* W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Konfiguruj usługę Application Insights**, lub **usługi Application Insights > Konfiguruj**. Dla pierwszego projektu hello Użyj toocreate kreatora hello zasobu usługi Application Insights. W przypadku kolejnych projektów wybierz hello tego samego zasobu.
* Jeśli nie ma żadnych menu usługi Application Insights, skonfigurować ręcznie:

   1. W [portalu Azure](https://portal,azure.com), otwórz zasobu usługi Application Insights hello już utworzone dla innego składnika.
   2. W bloku omówienie hello, otwórz hello rozwijanej Essentials kartę i hello kopiowania **klucza instrumentacji.**
   3. W projekcie Otwórz ApplicationInsights.config i Wstaw:`<InstrumentationKey>your copied key</InstrumentationKey>`

![Skopiuj plik .config toohello klucza Instrumentacji hello](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Włącz mapowanie wielu roli w aplikacji

Hello portalu Azure Otwórz hello zasobów dla aplikacji. W bloku podglądy hello, Włącz *Mapa aplikacji usługi roli*.

### <a name="4-enable-docker-metrics-optional"></a>4. Włączyć metryki Docker (opcjonalnie) 

Jeśli składnik jest uruchomiony w Docker hostowanych na maszynie Wirtualnej Windows Azure, można zbierać dodatkowe metryki z kontenera hello. Wstawianie w Twojej [diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pliku konfiguracji:

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Użyj cloud_RoleName tooseparate składników

Witaj `cloud_RoleName` właściwość jest dołączona tooall telemetrii. Identyfikuje składnik hello - hello roli lub usługi -, który pochodzi hello telemetrii. (Jest nie hello takie same jak cloud_RoleInstance, która oddziela identyczne ról, które są uruchomione jednocześnie na wielu procesy serwera lub maszyny).

W portalu hello możesz filtrować i segment telemetrii za pomocą tej właściwości. W tym przykładzie blok błędów hello jest filtrowane tooshow tylko informacje z usługi frontonu sieci web hello, filtrowanie błędów z zaplecza interfejsu API CRM hello:

![Metryki wykresu segmentowanych przez nazwę roli chmury](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Operacje śledzenia między składnikami

Można śledzić tooanother jeden składnik, hello wywołań podczas przetwarzania indywidualnych operacji.


![Pokaż dane telemetryczne dla operacji](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Kliknij za pośrednictwem listy skorelowane tooa dane telemetryczne dla tej operacji na powitania serwera frontonu sieci web i interfejs API zaplecza hello:

![Wyszukaj między składnikami](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Następne kroki

* [Oddzielne dane telemetryczne z programowanie, testowego i produkcyjnego](app-insights-separate-resources.md)
