---
title: "aaaMonitor i uzyskać wgląd w aplikację logiki jest wykonywane przy użyciu pakietu OMS - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Monitorowanie sieci jest uruchamiany aplikacji logiki z insights tooget analizy dzienników i Operations Management Suite (OMS) i bardziej zaawansowane funkcje debugowania szczegóły dotyczące rozwiązywania problemów i Diagnostyka"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Monitorowanie i uzyskiwanie szczegółowych informacji o uruchomieniu aplikacji logiki Operations Management Suite (OMS) i analizy dzienników

Do monitorowania i bardziej rozbudowane informacje debugowania, możesz włączyć analizy dzienników na powitania tym samym czasie, podczas tworzenia aplikacji logiki. Diagnostyka rejestrowania i monitorowania aplikacji logiki uruchamia się za pośrednictwem portalu Operations Management Suite (OMS) hello zapewnia analizy dzienników. Po dodaniu tooOMS rozwiązania zarządzania aplikacje logiki hello otrzymasz zagregowany stan logiki aplikacji działa i konkretne szczegółowe informacje, takie jak stan, czas wykonywania, stan ponownego wysyłania i identyfikatorów korelacji.

W tym temacie przedstawiono, jak tooturn analizy dzienników lub zainstaluj hello rozwiązania do zarządzania aplikacji logiki w OMS, dzięki czemu można wyświetlać zdarzenia środowiska uruchomieniowego i uruchom danych aplikacji logiki.

 > [!TIP]
 > toomonitor istniejących aplikacji logiki, wykonaj następujące kroki zbyt [włączyć rejestrowania diagnostycznego i wysyłać logiki aplikacji środowiska wykonawczego danych tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Wymagania

Przed rozpoczęciem należy toohave obszarem roboczym pakietu OMS. Dowiedz się [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Włącz rejestrowanie danych diagnostycznych podczas tworzenia aplikacji logiki

1. W [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki. Wybierz **nowe** > **integracji przedsiębiorstwa** > **aplikacji logiki** > **utworzyć**.

   ![Tworzenie aplikacji logiki](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. W hello **tworzenie aplikacji logiki** wykonaj te zadania, jak pokazano:

   1. Podaj nazwę aplikacji logiki, a następnie wybierz subskrypcję platformy Azure. 
   2. Utwórz lub wybierz grupę zasobów platformy Azure.
   3. Ustaw **analizy dzienników** za**na**. 
   Uruchamia hello wybierz obszar roboczy OMS miejsce za wysyłanie danych do aplikacji logiki. 
   4. Gdy wszystko jest gotowe, wybierz pozycję **toodashboard numeru Pin** > **Utwórz**.

      ![Tworzenie aplikacji logiki](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Po zakończeniu tego kroku, platforma Azure tworzy aplikację logiki, który jest obecnie skojarzony z obszarem roboczym pakietu OMS. 
      Ponadto ten krok również automatycznie instaluje rozwiązanie do zarządzania aplikacje logiki hello w obszarze roboczym pakietu OMS.

3. Uruchamia aplikację logiki w OMS, tooview [wykonaj te czynności](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Instalowanie rozwiązania do zarządzania aplikacje logiki hello w OMS

Jeśli już włączone analizy dzienników, podczas tworzenia aplikacji logiki, Pomiń ten krok. Masz już rozwiązania do zarządzania aplikacje logiki hello zainstalowane w OMS.

1. W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**. Wyszukaj "analizy dzienników" jako filtr, a następnie wybierz pozycję **analizy dzienników** pokazany:

   ![Wybierz pozycję "Analizy dzienników"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS. 

   ![Wybierz obszar roboczy OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. W obszarze **zarządzania**, wybierz **portalu OMS**.

   ![Wybierz pozycję "Portalu OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Na stronie głównej OMS zostanie wyświetlony Baner uaktualnienia hello, jeśli transparent hello tak, aby najpierw uaktualnić obszar roboczy OMS. Następnie wybierz pozycję **galerii rozwiązań**.

   ![Wybierz pozycję "Rozwiązań Galeria"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. W obszarze **wszystkie rozwiązania**, Znajdź i wybierz Kafelek hello hello **zarządzania aplikacje logiki** rozwiązania.

   ![Wybierz pozycję "Zarządzanie aplikacje logiki"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. Wybierz rozwiązanie hello tooinstall w obszarze roboczym pakietu OMS, **Dodaj**.

   ![Wybierz opcję "Dodaj", "Zarządzania aplikacjami logiki"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Widok, który uruchamia aplikację logiki w obszarze roboczym pakietu OMS

1. Stan aplikacji logiki i liczba hello tooview wykonywany, strony Przegląd toohello przejdź do obszaru roboczego OMS. Przejrzyj szczegóły hello na powitania **zarządzania aplikacje logiki** kafelka.

   ![Wyświetlanie stanu i liczba Uruchom aplikację logiki kafelka przeglądu](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Jeśli transparent uaktualnienia pojawia się zamiast hello kafelka zarządzania aplikacji logiki, wybierz hello transparentu, tak, aby najpierw uaktualnić obszar roboczy OMS.
  
   > ![Uaktualnij "Obszarem roboczym pakietu OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview podsumowanie zawierający więcej szczegółów dotyczących sekwencji aplikacji logiki, wybierz hello **zarządzania aplikacje logiki** kafelka.

   W tym miejscu że aplikacja działa logiki są pogrupowane według nazwy lub stan wykonania.

   ![Uruchamia aplikację logiki podsumowanie stanu](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview, którego wszystkie hello jest uruchamiany dla konkretnej logiki aplikacji lub stan, wybierz hello wiersza aplikacji logiki lub stanu.

   Oto przykład pokazujący wszystkie elementy hello konkretnej logiki aplikacji:

   ![Widok jest uruchamiana dla aplikacji logiki lub stanu](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Witaj **ponowne przesłanie** "Yes" w kolumnie jest wyświetlana dla przebiegów wynikających z wykonywania ponownie przesłane.

4. toofilter tych wyników, można wykonać filtrowania zarówno po stronie klienta i po stronie serwera.

   * Filtr po stronie klienta: dla każdej kolumny wybierz hello filtry, które mają. 
   Oto kilka przykładów:

     ![Przykładowe filtry kolumn](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtr po stronie serwera: toochoose określony czas okna lub toolimit hello szereg uruchomień występować, użyj hello zakresu kontroli u góry hello hello strony. 
   Domyślnie są wyświetlane tylko 1000 rekordów jednocześnie. 
   
     ![Przedział czasu hello zmiany](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. wszystkie tooview hello działań i ich szczegóły dla określonych wykonywania, wybierz opcję wiersza, który otwiera stronę wyszukiwania dziennika hello. 

   * Wybierz te informacje w tabeli, tooview **tabeli**.
   * Kwerenda hello toochange, można edytować hello ciągu zapytania w pasku szukania hello. 
   Aby lepiej wykorzystać możliwości wybierz **zaawansowane analizy**.

     ![Wyświetlanie akcji i szczegóły dotyczące uruchamiania aplikacji logiki](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     W tym miejscu na stronie hello Azure Log Analytics można aktualizować zapytania i widoku hello wynikiem hello tabeli. 
     To zapytanie używa [język zapytań Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), który można edytować, jeśli chcesz, aby tooview różne wyniki. 

     ![Analiza dzienników Azure - widok zapytania](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Następne kroki

* [Monitorowanie komunikatów B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
