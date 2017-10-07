---
title: "aaaCreate nowy zasób usługi Application Insights dla platformy Azure | Dokumentacja firmy Microsoft"
description: "Ręcznie skonfiguruj monitorowanie usługi Application Insights dla nowej aplikacji na żywo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Tworzenie zasobu usługi Application Insights
Azure Application Insights przedstawia dane dotyczące Twojej aplikacji w systemie Microsoft Azure *zasobów*. Tworzenie nowego zasobu w związku z tym jest częścią [konfigurowania usługi Application Insights toomonitor nową aplikację][start]. W wielu przypadkach tworzenie zasobu można automatycznie hello IDE. Jednak w niektórych przypadkach należy Utwórz ręcznie zasób — na przykład toohave oddzielne zasoby do rozwoju i produkcji tworzy aplikacji.

Po utworzeniu zasobu hello, możesz pobrać jego klucza Instrumentacji i użyć tego hello tooconfigure zestawu SDK w aplikacji hello. linki do kluczowych zasobów Hello hello telemetrii toohello zasobów.

## <a name="sign-up-toomicrosoft-azure"></a>Zarejestruj się tooMicrosoft Azure
Jeśli nie mam [Microsoft konto, Uzyskaj je teraz](http://live.com). (Jeśli korzystasz z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, masz już konto Microsoft.)

Należy również subskrypcji zbyt[Microsoft Azure](http://azure.com). Jeśli zespół lub organizacja ma subskrypcję platformy Azure, właściciela hello można dodać możesz tooit, za pomocą identyfikatora Windows Live ID. Tylko są naliczane opłaty za można użyć. podstawowy plan domyślny Hello umożliwia pewnego wykorzystanie eksperymentalne bezpłatnie.

Jeśli masz już dostępu tooa subskrypcji, zaloguj się za tooApplication wgląd w [http://portal.azure.com](https://portal.azure.com)i użyj toologin Twojego Identyfikatora Live.

## <a name="create-an-application-insights-resource"></a>Tworzenie zasobu usługi Application Insights
W hello [portal.azure.com](https://portal.azure.com), Dodaj zasób usługi Application Insights:

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Typ aplikacji** wpływa na informacje wyświetlane na powitania omówienie bloku i właściwości hello dostępnych w [Eksploratora metryk][metrics]. Jeśli nie widzisz typ aplikacji, wybierz pozycję Ogólne.
* **Subskrypcja** Twojego konta płatności na platformie Azure.
* **Grupa zasobów** jest wygodne właściwości zarządzania, takich jak kontrola dostępu. Jeśli utworzono już innych zasobów platformy Azure, możesz wybrać tooput tego nowego zasobu w hello tej samej grupy.
* **Lokalizacja** jest, gdzie możemy przechowywanie danych.
* **Numer PIN toodashboard** umieszcza kafelka szybkiego dostępu dla zasobu na stronie głównej Azure. Zalecane.

Po utworzeniu aplikacji, zostanie otwarty nowy blok. Ten blok jest, gdzie zobaczyć dane wydajności i użycia dotyczące Twojej aplikacji. 

tooit wstecz tooget następnym zalogowaniu tooAzure, poszukaj aplikacji szybki start kafelka na powitania start tablicy (ekranu). Lub kliknij przycisk Przeglądaj toofind go.

## <a name="copy-hello-instrumentation-key"></a>Skopiuj klucz Instrumentacji hello
klucz Instrumentacji Hello identyfikuje hello utworzony zasób. Należy go toohello toogive zestawu SDK.

![Kliknij Essentials, kliknij przycisk hello klucza Instrumentacji klawisze CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Zainstaluj hello zestawu SDK w aplikacji
Zainstaluj zestaw SDK usługi Application Insights hello w aplikacji. Ten krok zależy od silnie hello typu aplikacji. 

Użyj tooconfigure klucza Instrumentacji hello [SDK zainstalowany w aplikacji hello][start].

Hello zestaw SDK zawiera standardowe moduły, które wysłać dane telemetryczne bez konieczności toowrite żadnego kodu. akcje użytkownika tootrack lub diagnozowanie problemów bardziej szczegółowo [za pomocą interfejsu API hello] [ api] toosend własnych danych telemetrycznych.

## <a name="monitor"></a>Zobacz dane telemetryczne
Zamknij hello szybkie uruchomienie bloku tooreturn tooyour aplikacji bloku w hello portalu Azure.

Kliknij przycisk hello wyszukiwania kafelka toosee [diagnostycznych wyszukiwania][diagnostic], gdzie widoczne hello pierwsze zdarzenia. 

Jeśli spodziewasz większej ilości danych, kliknij przycisk **Odśwież** po kilku sekundach.

## <a name="creating-a-resource-automatically"></a>Automatyczne tworzenie zasobu
Można napisać [skrypt programu PowerShell](app-insights-powershell.md) toocreate zasobu automatycznie.

## <a name="next-steps"></a>Następne kroki
* [Tworzenie pulpitu nawigacyjnego](app-insights-dashboards.md)
* [Wyszukiwanie diagnostyczne](app-insights-diagnostic-search.md)
* [Eksplorowanie metryk](app-insights-metrics-explorer.md)
* [Pisanie zapytań analitycznych](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

