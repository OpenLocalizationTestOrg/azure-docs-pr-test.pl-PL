---
title: "aaaSCOM integracji z usługą Application Insights | Dokumentacja firmy Microsoft"
description: "Jeśli jesteś użytkownikiem SCOM monitorowania wydajności i diagnozowanie problemów z usługą Application Insights. Kompleksowe pulpity nawigacyjne, inteligentne alertów, zaawansowanych narzędzi diagnostycznych i zapytań analiz."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Monitorowanie wydajności aplikacji za pomocą usługi Application Insights dla oprogramowania SCOM
Jeśli używasz programu System Center Operations Manager (SCOM) toomanage serwerów, można monitorować wydajność i diagnozowanie problemów z wydajnością z pomocy hello [Azure Application Insights](app-insights-asp-net.md). Usługi Application Insights monitoruje aplikację sieci web żądania przychodzące, wychodzące REST i wywołania SQL, wyjątków i ślady dziennika. Zapewnia on pulpity nawigacyjne z wykresami metryki i inteligentne alerty, a także zaawansowane wyszukiwanie diagnostycznych i zapytania analityczne przez ten telemetrii. 

Można przełączyć na monitorowanie usługi Application Insights przy użyciu pakietu administracyjnego programu SCOM.

## <a name="before-you-start"></a>Przed rozpoczęciem
Przyjęto założenie:

* Serwery sieci web znasz SCOM i korzystanie z programu SCOM 2012 R2 lub 2016 toomanage programu IIS.
* Użytkownik zainstalował już na serwerach aplikacji sieci web, które mają toomonitor z usługi Application Insights.
* Wersja platformy aplikacji jest .NET 4.5 lub nowszej.
* Masz subskrypcję tooa dostępu [Microsoft Azure](https://azure.com) i zalogować się toohello [portalu Azure](https://portal.azure.com). Organizacji mogą mieć subskrypcję i dodać Twojego tooit konta Microsoft.

(zespół deweloperów hello może zbudować hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md) do aplikacji sieci web hello. Instrumentacja to czas kompilacji daje im większa elastyczność w pisaniu telemetria niestandardowa. Jednak nie ma znaczenia,:, można wykonać hello czynności opisane w tym miejscu lub bez hello wbudowany zestaw SDK.)

## <a name="one-time-install-application-insights-management-pack"></a>(Jeden raz) Zainstaluj pakiet administracyjny usługi Application Insights
Na komputerze hello realizującym programu Operations Manager:

1. Odinstaluj wszelkie starą wersję pakietu administracyjnego hello:
   1. W programie Operations Manager Otwórz administracji, pakietów administracyjnych. 
   2. Usuń starą wersję hello.
2. Pobierz i zainstaluj pakiet administracyjny hello z hello katalogu.
3. Ponowne uruchomienie programu Operations Manager.

## <a name="create-a-management-pack"></a>Utwórz pakiet administracyjny
1. W programie Operations Manager, otwórz **tworzenie**, **.NET... with usługi Application Insights**, **Kreator dodawania monitorowania**i ponownie wybierz **.NET... z aplikacją Informacje na temat technologii**.
   
    ![](./media/app-insights-scom/020.png)
2. Nazwa konfiguracji powitania po aplikacji. (Masz tooinstrument jedną aplikację naraz.)
   
    ![](./media/app-insights-scom/030.png)
3. Na hello sama strona kreatora tworzenia nowej zarządzania dodatkiem Service pack, lub wybierz pakiet, który wcześniej utworzony dla usługi Application Insights.
   
     (hello usługi Application Insights [pakiet administracyjny](https://technet.microsoft.com/library/cc974491.aspx) szablonem, z którego można utworzyć wystąpienia. Można użyć ponownie hello samo wystąpienie później.)

    ![W hello karta Ogólne właściwości wpisz nazwę hello aplikacji hello. Kliknij przycisk Nowy, a następnie wpisz nazwę dla pakietu administracyjnego. Kliknij przycisk OK, a następnie kliknij przycisk Dalej.](./media/app-insights-scom/040.png)

1. Wybierz jedną aplikację, które mają toomonitor. Hello funkcja wyszukiwania wyszukuje między aplikacji zainstalowanych na serwerach.
   
    ![Na jakie kartę tooMonitor kliknij przycisk Dodaj, wpisz część nazwy aplikacji hello, kliknij przycisk Wyszukaj, wybierz OK aplikacji hello, a następnie Dodaj.](./media/app-insights-scom/050.png)
   
    Hello pole opcjonalne zakresu monitorowania może być używane toospecify podzestawu serwerów, jeśli nie chcesz, aby aplikacja hello toomonitor na wszystkich serwerach.
2. Na następnej stronie kreatora hello musisz podać toosign Twoje poświadczenia w tooMicrosoft Azure.
   
    Na tej stronie wybierz polecenie zasobu usługi Application Insights hello miejscu hello toobe danych telemetrycznych przeanalizowany i wyświetlane. 
   
   * Jeśli aplikacja hello został skonfigurowany dla usługi Application Insights podczas tworzenia, wybierz jej istniejącego zasobu.
   * W przeciwnym razie utwórz nowy zasób o nazwie aplikacji hello. Jeśli istnieją inne aplikacje, które są składnikami programu hello tego samego systemu, umieść je w hello tej samej grupie zasobów, toomanage łatwiejsze toohello telemetrii toomake dostępu.
     
     Te ustawienia można zmienić później.
     
     ![Na karcie Ustawienia usługi Application Insights kliknij przycisk "Zarejestruj" i podaj poświadczenia konta Microsoft Azure. Następnie wybierz pozycję subskrypcji, grupy zasobów i zasobów.](./media/app-insights-scom/060.png)
3. Kreator hello ukończone.
   
    ![Kliknięcie pozycji Utwórz](./media/app-insights-scom/070.png)

Powtórz tę procedurę dla każdej aplikacji, które mają toomonitor.

Ustawienia toochange później, należy ponownie otworzyć właściwości hello hello monitora z okna Tworzenie hello.

![W tworzenie, wybierz opcję monitorowanie wydajności aplikacji .NET z usługi Application Insights, wybierz monitora, a następnie kliknij przycisk Właściwości.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Sprawdź monitorowania
monitor Hello na każdym serwerze zainstalowano wyszukiwania dla aplikacji. Gdy znajdzie aplikacji hello konfiguruje aplikacji hello toomonitor Monitor stanu usługi Application Insights. W razie potrzeby najpierw instaluje Monitor stanu na powitania serwera.

Aby sprawdzić, które wystąpienia aplikacji hello znaleziono:

![Monitorowanie, otwórz usługę Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Dane telemetryczne wyświetleń w usłudze Application Insights
W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello zasobów dla aplikacji. Możesz [zobaczyć wykresy przedstawiający telemetrii](app-insights-dashboards.md) z aplikacji. (Jeśli go nie pokazano na stronie głównej hello jeszcze, kliknij strumień na żywo metryk).

## <a name="next-steps"></a>Następne kroki
* [Konfigurowanie pulpitu nawigacyjnego](app-insights-dashboards.md) toobring razem hello najważniejszych wykresy monitorowania to i inne aplikacje.
* [Dowiedz się więcej o metryk](app-insights-metrics-explorer.md)
* [Konfigurowanie alertów](app-insights-alerts.md)
* [Diagnozowanie problemów z wydajnością](app-insights-detect-triage-diagnose.md)
* [Zaawansowane zapytania analityczne](app-insights-analytics.md)
* [Dostępność testy sieci web](app-insights-monitor-web-app-availability.md)

