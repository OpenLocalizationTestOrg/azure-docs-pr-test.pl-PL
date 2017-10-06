---
title: "Usługi w chmurze przy użyciu usługi Application Insights aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa w chmurze tootroubleshoot problemy przy użyciu usługi Application Insights tooprocess danych z diagnostyki Azure."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Rozwiązywanie problemów z usługi w chmurze przy użyciu usługi Application Insights
Z [Azure SDK 2.8](https://azure.microsoft.com/downloads/) i rozszerzenie diagnostycznych platformy Azure w wersji 1.5, może wysyłać dane diagnostyczne platformy Azure dla usługi w chmurze bezpośrednio tooApplication szczegółowych informacji. Witaj dzienników zebranych przez diagnostyki Azure&mdash;w tym dzienniki aplikacji, dzienniki zdarzeń systemu Windows, dzienniki zdarzeń systemu Windows i liczniki wydajności&mdash;mogą być wysyłane tooApplication szczegółowych informacji. Następnie można zwizualizować te informacje w portalu usługi Application Insights hello interfejsu użytkownika. Następnie można użyć hello zestaw SDK usługi Application Insights tooget wgląd w dzienniki, które pochodzą z aplikacji, a także hello systemu i danych na poziomie infrastruktury, która pochodzi z diagnostyki Azure i metryki.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Skonfiguruj diagnostyki Azure toosend danych tooApplication Insights
Wykonaj te kroki tooset się z chmury usługi projektu toosend diagnostyki Azure danych tooApplication szczegółowych informacji.

1. W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy rolę i wybierz **właściwości** tooopen hello roli projektanta.

    ![Właściwości roli Eksploratora rozwiązań][1]

2. W hello **diagnostyki** sekcji hello roli projektanta, wybierz hello **wysyłania tooApplication danych diagnostycznych Insights** opcji.

    ![Projektant roli wysyłanie danych diagnostycznych wgląd tooapplication danych][2]

3. W hello okno dialogowe, które pojawia się wybierz zasób usługi Application Insights hello, który ma toosend hello Azure diagnostyki danych. okno dialogowe Hello umożliwia tooselect istniejący zasób usługi Application Insights z subskrypcji lub toomanually określ klucz instrumentacji dla zasobu usługi Application Insights. Aby uzyskać więcej informacji na temat tworzenia zasobu usługi Application Insights, zobacz [utworzyć nowy zasób usługi Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![Wybierz zasób usługi application insights][3]

    Po dodaniu zasobu usługi Application Insights hello hello klucza instrumentacji dla tego zasobu jest przechowywana jako ustawienia konfiguracji usługi o nazwie hello **APPINSIGHTS_INSTRUMENTATIONKEY**. Można zmienić tego ustawienia konfiguracji dla każdej konfiguracji usługi lub środowiska. toodo tak, wybierz inną konfigurację z hello **konfiguracji usługi** listę i określenie nowego klucza Instrumentacji w takiej konfiguracji.

    ![Wybierz konfigurację usługi][4]

    Witaj **APPINSIGHTS_INSTRUMENTATIONKEY** ustawienie konfiguracji jest używany przez rozszerzenie Diagnostyka programu Visual Studio tooconfigure hello hello odpowiednie usługi Application Insights informacje o zasobach podczas publikowania. Ustawienie konfiguracji Hello to wygodny sposób definiowania różnych Instrumentacji kluczy w przypadku konfiguracji z innej usługi. Visual Studio będzie tłumaczenie tego ustawienia i wstawić go w publiczna Konfiguracja rozszerzenia diagnostyki hello podczas hello procesu publikowania. proces hello toosimplify konfigurowania rozszerzenia diagnostyki hello przy użyciu programu PowerShell, hello pakietu wyjście z programu Visual Studio zawiera także hello publicznej konfiguracji XML z hello odpowiedni klucz Instrumentacji usługi Application Insights. pliki konfiguracji publicznego Hello są tworzone w folderze rozszerzenia hello i wykonaj wzorzec hello *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Wszystkie wdrożenia oparte na środowisku PowerShell można użyć tego wzorca toomap każdej roli tooa konfiguracji.

4) toosend diagnostyki Azure tooconfigure wszystkie dzienniki poziom błędów i liczniki wydajności zebrane przez hello Azure diagnostics agenta tooApplication szczegółowych informacji, Włącz hello **wysyłania tooApplication danych diagnostycznych Insights** opcji. 

    Jeśli chcesz toofurther skonfigurować, jakie dane są wysyłane tooApplication szczegółowe informacje, należy ręcznie zmienić hello *diagnostics.wadcfgx* plik dla każdej roli. Zobacz [skonfigurować diagnostyki Azure toosend danych tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn więcej informacji na temat ręcznego aktualizowania konfiguracji hello.

Gdy usługa w chmurze hello jest wgląd tooapplication danych diagnostycznych platformy Azure toosend skonfigurowany, można ją wdrożyć tooAzure normalnie, sprawdzając, czy hello rozszerzenie Azure diagnostics jest włączona. Aby uzyskać więcej informacji, zobacz [publikowania usługi w chmurze przy użyciu programu Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Wyświetlanie danych diagnostycznych platformy Azure w usłudze Application Insights
Hello Azure telemetrii diagnostycznych zostaną wyświetlone w hello zasób skonfigurowany dla usługi w chmurze usługi Application Insights.

Typy dziennika diagnostyki Azure mapy tooApplication pojęcia wgląd w następujący sposób:

* Liczniki wydajności są wyświetlane jako metryki niestandardowe w usłudze Application Insights.
* Dzienniki zdarzeń systemu Windows są wyświetlane jako śladów i zdarzeń niestandardowych w usłudze Application Insights.
* Dzienniki aplikacji, dzienniki zdarzeń systemu Windows i żadnych dzienników diagnostycznych infrastruktury są wyświetlane jako dane śledzenia w usłudze Application Insights.

tooview dane diagnostyczne platformy Azure w usłudze Application Insights, wykonaj jedną z następujących hello:

* Użyj [Eksploratora metryk](../application-insights/app-insights-metrics-explorer.md) toovisualize liczniki wszelkie niestandardowe wydajności lub liczby różnych rodzajów zdarzeń w dzienniku zdarzeń systemu Windows.

    ![Metryki niestandardowe w Eksploratorze metryk][5]

* Użyj [wyszukiwania](../application-insights/app-insights-diagnostic-search.md) toosearch między dzienniki śledzenia hello wysyłane przez diagnostyki Azure. Na przykład, jeśli wystąpił nieobsługiwany wyjątek spowodował hello roli toocrash i odtworzenia, informacje o wyjątku hello zostaną wyświetlone w hello *aplikacji* kanału *dziennika zdarzeń systemu Windows*. Można użyć wyszukiwania toolook na powitania błędu dziennika zdarzeń systemu Windows i uzyskać ślad stosu pełne hello hello wyjątek toohelp Znajdź hello przyczyna problemu hello.

    ![Ślady wyszukiwania][6]

## <a name="next-steps"></a>Następne kroki
* [Dodawanie usługi w chmurze tooyour zestaw SDK usługi Application Insights hello](../application-insights/app-insights-cloudservices.md) toosend dane dotyczące żądań, wyjątków, zależności i wszelkie niestandardowe dane telemetryczne z aplikacji. W połączeniu z danymi diagnostyki Azure hello, te informacje można uzyskać pełny widok aplikacji i systemu, w hello tego samego zasobu szczegółowe informacje o aplikacji.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
