---
title: "Analiza zdarzeń usługi sieci szkieletowej z usługą Application Insights aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wizualizacji i analizowania zdarzeń za pomocą usługi Application Insights, monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Analiza zdarzeń i wizualizacji z usługą Application Insights

Azure Application Insights to rozszerzalna platforma aplikacji monitorowania i diagnostyki. Obejmuje zaawansowane analizy i badania narzędzia, można dostosować pulpit nawigacyjny i wizualizacje i dalsze opcje w tym automatycznego tworzenia alertu. Jest hello zalecane platforma do monitorowania i diagnostyki dla aplikacji platformy Service Fabric i usług.

## <a name="setting-up-application-insights"></a>Konfigurowanie usługi Application Insights

### <a name="creating-an-ai-resource"></a>Tworzenie zasobu AI

zasób toocreate AI head za pośrednictwem portalu Azure Marketplace toohello i wyszukaj "Usługi Application Insights". Powinien on wyświetlane jako pierwsze rozwiązanie hello (znajduje się w kategorii "Web + Mobile"). Kliknij przycisk **Utwórz** podczas szukania na właściwy zasób hello (Sprawdź, czy ścieżka zgodna hello obraz poniżej).

![Nowy zasób usługi Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Konieczne będzie toofill zasób hello tooprovision niektóre informacje poprawnie. W hello *typu aplikacji* pola, użyj "Aplikacja sieci web ASP.NET" Jeśli będziesz używać dowolną sieć szkieletowa usług modele programowania lub publikowania klastra toohello aplikacji .NET. Użyj "Ogólne", jeśli będziesz wdrażać pliki wykonywalne gościa i kontenerów. Ogólnie rzecz biorąc tookeep "Aplikacja sieci web ASP.NET" toousing domyślne opcje Otwórz w przyszłości hello. Nazwa Hello jest tooyour preferencji, a zarówno subskrypcji, jak i grupy zasobów hello są włączone po wdrożeniu hello zasobu. Zaleca się, że zasób AI znajduje się w hello tej samej grupie zasobów co klaster. Aby uzyskać więcej informacji, zobacz [utworzyć zasobu usługi Application Insights](../application-insights/app-insights-create-new-resource.md)

Należy tooconfigure klucza Instrumentacji AI hello AI narzędziem agregacji zdarzeń. Po zasobu AI (zajmuje kilka minut po zweryfikowaniu jest wdrożenie hello), przejdź tooit i Znajdź hello **właściwości** sekcji na pasku nawigacyjnym po lewej stronie powitania. Zostanie otwarty nowy blok pokazujący *klucza INSTRUMENTACJI*. Jeśli potrzebujesz toochange hello subskrypcji lub grupy zasobów zasobu hello mogą to robić tutaj również.

### <a name="configuring-ai-with-wad"></a>Konfigurowanie AI z WAD

Istnieją dwa podstawowe sposoby danych toosend z tooAzure WAD AI, co jest osiągane przez dodanie AI zbiornika toohello WAD konfiguracji, zgodnie z opisem w [w tym artykule](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Dodaj klucz Instrumentacji AI, podczas tworzenia klastra w portalu Azure

![Dodawanie AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Podczas tworzenia klastra, jeśli włączono diagnostyki "Włączone", wyświetli się tooenter pole opcjonalne klucza Instrumentacji wgląd w aplikacji. Po wklejeniu Twojej IKey AI tutaj zbiornika hello AI zostanie automatycznie konfigurowane w szablonie usługi Resource Manager hello, który jest używany toodeploy klastra.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Dodaj hello szablonu usługi Resource Manager toohello zbiornika AI

W hello "WadCfg" hello szablonu usługi Resource Manager należy dodać "Sink" przy tym hello następujące dwie zmiany:

1. Dodaj konfigurację zbiornika hello:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Dołącz hello zbiornika hello DiagnosticMonitorConfiguration przez dodawanie powitania po wierszu w "DiagnosticMonitorConfiguration" hello "WadCfg":

    ```json
    "sinks": "applicationInsights"
    ```

W obu wstawki kodu hello powyżej hello nazwa "applicationInsights" była używane toodescribe hello ujścia. Nie jest wymagane i tak długo, jak nazwa hello zbiornika hello jest dołączona do "sink", można ustawić ciąg tooany nazwy hello.

Obecnie dzienniki z hello klastra będzie wyświetlany jako dane śledzenia w przeglądarce dzienników AI firmy. Ponieważ większość hello śladów pochodzących z hello platform jest poziom "Informacyjny", możesz również należy rozważyć zmianę hello zbiornika konfiguracji tooonly wysyłania dzienników typu "Krytyczne" lub "Error". Można to zrobić przez dodanie "węzła kanały" tooyour zbiornika, jak pokazano w [w tym artykule](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Użycie niepoprawne IKey AI w portalu lub w szablonie usługi Resource Manager masz toomanually należy zmienić wartość klucza hello i zaktualizować klastra hello / Wdróż go ponownie. 

### <a name="configuring-ai-with-eventflow"></a>Konfigurowanie AI z EventFlow

Jeśli używasz EventFlow tooaggregate zdarzeń, upewnij się, że hello tooimport `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`pakietu NuGet. Witaj następujące ma toobe objęte hello *generuje* sekcji hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Wprowadź zmiany wymagane hello toomake się, że w filtry, a także zawierać innych danych wejściowych (wraz z ich odpowiednich pakietów NuGet).

## <a name="aisdk"></a>AI. ZESTAW SDK

Ogólnie zaleca się toouse EventFlow i WAD jako rozwiązania agregacji, ponieważ pozwalają one na bardziej moduły toodiagnostics podejścia i monitorowania, tj. Jeśli chcesz toochange Twoje dane wyjściowe z EventFlow, nie wymaga żadnych rzeczywistych tooyour zmiany Instrumentacja, po prostu prostą modyfikację tooyour pliku. Jeśli jednak zdecydować tooinvest za pomocą usługi Application Insights i nie są prawdopodobnie toochange tooa różnych platform, należy rozważyć w celu agregowania zdarzeń i wysyłania ich tooAI przy użyciu nowego zestawu SDK przez AI. Oznacza to, nie będą mieć tooconfigure EventFlow toosend Twojego tooAI danych, ale zamiast tego zostanie zainstalowany pakiet NuGet usługi Service Fabric hello ApplicationInsight. Szczegółowe informacje dotyczące pakietów hello można znaleźć [tutaj](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Obsługa usługi Application Insights Mikrousług i kontenery](https://azure.microsoft.com/app-insights-microservices/) przedstawiono niektóre hello nowe funkcje pracuje (nadal obecnie w wersji beta), co pozwala użytkownikowi toohave bardziej rozbudowane poza pole opcje monitorowania z AI. Obejmują one śledzenia zależności (używanego podczas konstruowania AppMap wszystkich usług i aplikacji w klastrze i hello komunikację między nimi) oraz lepsze korelacji śladów pochodzących z usług (pomaga w lepiej trafić problemu w hello przepływ pracy aplikacji lub usługi).

Jeśli opracowujesz w .NET i prawdopodobnie będzie używać niektórych modele programowania usługi Service Fabric, a są ujawniane toouse AI jako platformy wizualizacji i analizowanie danych zdarzeń i dzienników, wówczas zalecamy go za pośrednictwem hello trasy AI SDK jako monitorowanie i Diagnostyka przepływ pracy. Odczyt [to](../application-insights/app-insights-asp-net-more.md) i [to](../application-insights/app-insights-asp-net-trace-logs.md) tooget korzystanie z zapleczy AI toocollect i wyświetlenia dzienników.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Nawigowanie po hello AI zasobów w portalu Azure

AI skonfigurowane jako dane wyjściowe dla zdarzeń i dzienniki informacji należy uruchomić tooshow w zasobie AI za kilka minut. Przejdź toohello AI zasobu, który będzie miał użytkownik toohello AI pulpitu nawigacyjnego zasobów. Kliknij przycisk **wyszukiwania** hello AI zadań toosee hello najnowsze śledzenia o odebraniu i stanie toofilter toobe za ich pośrednictwem.

*Eksploratora metryk* stanowi przydatne narzędzie do tworzenia niestandardowych pulpitów nawigacyjnych w oparciu metryki aplikacji, usług i klaster mogą raportowania. Zobacz [metryki Eksplorowanie w usłudze Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset się kilka wykresów dla siebie na podstawie hello danych są zbierane.

Kliknięcie przycisku **Analytics** spowoduje przejście portalu Application Insights Analytics toohello, gdzie można zbadać zdarzenia i dane śledzenia z większą zakresu i opcjonalność. Dowiedz się więcej o tym w [analizy w usłudze Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Następne kroki

* [Konfigurowanie alertów w AI](../application-insights/app-insights-alerts.md) toobe otrzymywać powiadomienia o zmianach w wydajności i użycia
* [Inteligentne wykrywania w usłudze Application Insights](../application-insights/app-insights-proactive-diagnostics.md) wykonuje aktywnego analizy telemetrii hello wysyłane tooAI toowarn o potencjalnych problemach z wydajnością
