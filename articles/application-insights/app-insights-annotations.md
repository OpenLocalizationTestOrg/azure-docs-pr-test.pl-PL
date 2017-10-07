---
title: "Adnotacje aaaRelease dla usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Dodaj wdrożenie lub kompilacji znaczników wykresy Eksploratora metryk tooyour w usłudze Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Adnotacje na wykresach metryki w usłudze Application Insights
Adnotacje w [Eksploratora metryk](app-insights-metrics-explorer.md) wdrożonym nowej kompilacji lub innego istotnego zdarzenia na wykresach. Finalizowania go łatwo toosee czy zmiany miało wpływu na wydajność aplikacji. Mogą być automatycznie tworzone przez hello [systemu kompilacji programu Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). Można również utworzyć tooflag adnotacje dowolnego zdarzenia, które chcesz przez [tworzenie je z programu PowerShell](#create-annotations-from-powershell).

![Przykład adnotacje z korelacją widoczne z czas odpowiedzi serwera](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Adnotacje wydania z kompilacji programu VSTS

Adnotacje zlecenia są funkcją hello kompilacji opartej na chmurze i wersję usługi Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Zainstaluj rozszerzenie adnotacje hello (jeden raz)
Adnotacje zlecenia może toocreate toobe, będziesz potrzebować tooinstall jedną z hello w wiele rozszerzeń usługi Team hello Visual Studio Marketplace.

1. Zaloguj się tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projektu.
2. W programie Visual Studio Marketplace [uzyskać rozszerzenie wersji adnotacje hello](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)i dodaj go tooyour konta usługi Team Services.

![AT z góry po prawej stronie sieci web usługi Team Services, otwórz Marketplace. Wybierz Visual Team Services, a następnie w obszarze kompilacji i wydania, wybierz pozycję Zobacz więcej.](./media/app-insights-annotations/10.png)

Wystarczy toodo raz dla Twojego konta Visual Studio Team Services. Adnotacje wersji można teraz skonfigurować dla każdego projektu w ramach Twojego konta. 

### <a name="configure-release-annotations"></a>Skonfiguruj adnotacje zlecenia

Należy klucza tooget oddzielne interfejsu API dla każdego szablonu wersji usługi VSTS.

1. Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com) , a następnie otwórz hello zasobu usługi Application Insights, który monitoruje aplikacji. (Lub [teraz utworzyć](app-insights-overview.md), jeśli nie zostało to jeszcze zrobione jeszcze.)
2. Otwórz **dostępu do interfejsu API**, **Application Insights identyfikator**.
   
    ![Portal.azure.com Otwórz zasobu usługi Application Insights i wybierz polecenie Ustawienia. Otwórz dostępu do interfejsu API. Skopiuj identyfikator aplikacji hello](./media/app-insights-annotations/20.png)

4. W osobnym oknie przeglądarki otworzyć lub utworzyć hello wersji szablonu, który zarządza wdrożeń z Visual Studio Team Services. 
   
    Dodaj zadanie, a hello Application Insights wersji adnotacji zadań, wybierz z hello menu.
   
    Wklej hello **identyfikator aplikacji** skopiowany z hello bloku dostępu do interfejsu API.
   
    ![W programie Visual Studio Team Services otwórz wersji, wybierz definicji wersji i wybierz polecenie Edytuj. Kliknij pozycję Dodaj zadanie, a następnie wybierz Application Insights wersji adnotacji. Wklej hello identyfikator aplikacji szczegółowych informacji.](./media/app-insights-annotations/30.png)
4. Zestaw hello **APIKey** zmiennej tooa pola `$(ApiKey)`.

5. Po powrocie do hello Azure okna Utwórz nowy klucz interfejsu API i wykonać jego kopię.
   
    ![W bloku dostępu do interfejsu API w hello Azure okna hello kliknij przycisk Utwórz klucz interfejsu API. Podaj komentarz, sprawdź adnotacje zapisu, a następnie kliknij przycisk Wygeneruj klucz. Skopiuj hello nowego klucza.](./media/app-insights-annotations/40.png)

6. Otwórz kartę Konfiguracja hello hello wersji szablonu.
   
    Tworzenie definicji zmiennej `ApiKey`.
   
    Wklej Twojej toohello klucza interfejsu API ApiKey definicji zmiennej.
   
    ![W oknie usługi Team Services hello wybierz kartę Konfiguracja hello, a następnie kliknij przycisk Dodaj zmienną. Ustaw tooApiKey nazwa hello na powitania wartość Wklej klucz hello wygenerowane przed chwilą i kliknij ikonę blokady hello.](./media/app-insights-annotations/50.png)
7. Na koniec **zapisać** hello definicji wersji.


## <a name="view-annotations"></a>Adnotacje widoku
Teraz przy każdym użyciu hello wersji szablonu toodeploy nową wersję adnotacja zostanie wysłane tooApplication szczegółowych informacji. Adnotacje Hello będą wyświetlane na wykresach w Eksploratorze metryk.

Kliknięcie dowolnej adnotacji znacznika tooopen szczegółowe informacje o wersji hello, m.in. obiekt żądający, Rozgałęzienie kontroli źródła, definicji wersji i środowiska.

![Kliknij znacznik adnotacji dowolnej wersji.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Tworzenie niestandardowych adnotacje z programu PowerShell
Można również utworzyć adnotacje z żaden proces, który chcesz (bez użycia programu VS Team System). 


1. Wykonaj kopię lokalne powitania [skrypt programu Powershell z usługi GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Pobierz identyfikator aplikacji hello i Utwórz klucz interfejsu API z hello bloku dostępu do interfejsu API.

3. Wywołanie skryptu hello następująco:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Jest łatwy toomodify hello skryptu, na przykład toocreate adnotacje dla ostatnich hello.

## <a name="next-steps"></a>Następne kroki

* [Tworzenie elementów roboczych](app-insights-diagnostic-search.md#create-work-item)
* [Automatyzacja przy użyciu programu PowerShell](app-insights-powershell.md)
