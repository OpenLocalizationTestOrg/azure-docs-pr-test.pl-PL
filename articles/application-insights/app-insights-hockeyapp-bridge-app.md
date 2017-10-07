---
title: "aaaExploring HockeyApp danych w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analizowanie użycia i wydajności aplikacji platformy Azure za pomocą usługi Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Eksplorowanie danych HockeyApp w usłudze Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello zaleca platformy monitorowania na żywo wersje desktop i mobile apps. Z HockeyApp można wysyłać niestandardowych i śledzenia użycia toomonitor telemetrii i ułatwić diagnostyki (w dane awarii toogetting dodanie). Ten strumień danych telemetrycznych może być badana zaawansowanym hello [Analytics](app-insights-analytics.md) funkcji [Azure Application Insights](app-insights-overview.md). Ponadto można [wyeksportować hello niestandardowych i dane telemetryczne śledzenia](app-insights-export-telemetry.md). tooenable funkcji, należy skonfigurować mostek przekazuje HockeyApp danych niestandardowych tooApplication szczegółowych informacji.

## <a name="hello-hockeyapp-bridge-app"></a>Witaj Mostek HockeyApp aplikacji
HockeyApp Mostek aplikacji Hello jest hello core funkcja umożliwiająca tooaccess HockeyApp niestandardowej, a dane telemetryczne śledzenia w usłudze Application Insights za pośrednictwem hello Analytics i funkcji eksportu ciągłego. Niestandardowy i śledzenia zebranych zdarzeń wg HockeyApp po utworzeniu hello hello HockeyApp Mostek aplikacji będzie dostępny z tych funkcji. Zobaczmy, jak tooset jednego z tych aplikacji mostek.

Otwórz ustawienia konta aplikacji HockeyApp, [tokeny interfejsu API](https://rink.hockeyapp.net/manage/auth_tokens). Utwórz nowy token, albo ponownie użyć już istniejącego. Hello minimalne uprawnienia wymagane są tylko do odczytu"". Zająć tokenu kopię hello interfejsu API.

![Pobierz token HockeyApp API](./media/app-insights-hockeyapp-bridge-app/01.png)

Otwórz hello portalu Microsoft Azure i [utworzyć zasobu usługi Application Insights](app-insights-create-new-resource.md). Ustaw typ aplikacji zbyt "Aplikacji HockeyApp Mostek":

![Nowy zasób usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Nie ma potrzeby tooset nazwę — spowoduje to ustawienie automatycznie na podstawie nazwy HockeyApp hello.

Witaj HockeyApp Mostek pola są wyświetlane. 

![Wprowadź pola Mostek](./media/app-insights-hockeyapp-bridge-app/03.png)

Wprowadź token HockeyApp hello, zanotowaną wcześniej. Ta akcja powoduje wypełnienie menu rozwijanym "HockeyApp aplikację" hello z wszystkich aplikacji HockeyApp. Wybierz hello, co ma toouse i pozostałej pełną hello hello pól. 

Otwórz hello nowy zasób. 

Należy pamiętać, że hello danych zajmie trochę czasu toostart przepływu.

![Oczekiwanie na dane zasobu usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/04.png)

Gotowe. Niestandardowy i śledzenia zbieranych danych w aplikacji zinstrumentowane HockeyApp od tego momentu jest teraz również dostępne tooyou w hello Analytics i funkcji eksportu ciągłego usługi Application Insights.

Załóżmy krótko Przejrzyj wszystkie te funkcje tooyou teraz dostępne.

## <a name="analytics"></a>Analiza
Analiza jest zaawansowanym narzędziem do ad hoc wykonywania kwerend danych, dzięki czemu toodiagnose i analizowania telemetrii i szybko odnaleźć główne przyczyny i wzorce.

![Analiza](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Dowiedz się więcej o analityka](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Eksport ciągły
Eksport ciągły umożliwia tooexport danych do kontenera magazynu obiektów Blob Azure. Jest to bardzo przydatne, jeśli potrzebujesz tookeep danych przez czas dłuższy niż okres przechowywania hello obecnie oferowanych przez usługi Application Insights. Możesz hello dane są przechowywane w magazynie obiektów blob, przetworzyć go do bazy danych SQL lub preferowany rozwiązań magazynowania danych.

[Dowiedz się więcej o eksportu ciągłego](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Następne kroki
* [Zastosuj dane analityczne tooyour](app-insights-analytics-tour.md)

