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
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="c2157-103">Monitorowanie i uzyskiwanie szczegółowych informacji o uruchomieniu aplikacji logiki Operations Management Suite (OMS) i analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="c2157-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="c2157-104">Do monitorowania i bardziej rozbudowane informacje debugowania, możesz włączyć analizy dzienników na powitania tym samym czasie, podczas tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c2157-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="c2157-105">Diagnostyka rejestrowania i monitorowania aplikacji logiki uruchamia się za pośrednictwem portalu Operations Management Suite (OMS) hello zapewnia analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c2157-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="c2157-106">Po dodaniu tooOMS rozwiązania zarządzania aplikacje logiki hello otrzymasz zagregowany stan logiki aplikacji działa i konkretne szczegółowe informacje, takie jak stan, czas wykonywania, stan ponownego wysyłania i identyfikatorów korelacji.</span><span class="sxs-lookup"><span data-stu-id="c2157-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="c2157-107">W tym temacie przedstawiono, jak tooturn analizy dzienników lub zainstaluj hello rozwiązania do zarządzania aplikacji logiki w OMS, dzięki czemu można wyświetlać zdarzenia środowiska uruchomieniowego i uruchom danych aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c2157-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="c2157-108">toomonitor istniejących aplikacji logiki, wykonaj następujące kroki zbyt [włączyć rejestrowania diagnostycznego i wysyłać logiki aplikacji środowiska wykonawczego danych tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="c2157-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="c2157-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c2157-109">Requirements</span></span>

<span data-ttu-id="c2157-110">Przed rozpoczęciem należy toohave obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="c2157-111">Dowiedz się [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2157-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="c2157-112">Włącz rejestrowanie danych diagnostycznych podczas tworzenia aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="c2157-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="c2157-113">W [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c2157-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="c2157-114">Wybierz **nowe** > **integracji przedsiębiorstwa** > **aplikacji logiki** > **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="c2157-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Tworzenie aplikacji logiki](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="c2157-116">W hello **tworzenie aplikacji logiki** wykonaj te zadania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="c2157-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="c2157-117">Podaj nazwę aplikacji logiki, a następnie wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2157-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="c2157-118">Utwórz lub wybierz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2157-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="c2157-119">Ustaw **analizy dzienników** za**na**.</span><span class="sxs-lookup"><span data-stu-id="c2157-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="c2157-120">Uruchamia hello wybierz obszar roboczy OMS miejsce za wysyłanie danych do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c2157-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="c2157-121">Gdy wszystko jest gotowe, wybierz pozycję **toodashboard numeru Pin** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c2157-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Tworzenie aplikacji logiki](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="c2157-123">Po zakończeniu tego kroku, platforma Azure tworzy aplikację logiki, który jest obecnie skojarzony z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="c2157-124">Ponadto ten krok również automatycznie instaluje rozwiązanie do zarządzania aplikacje logiki hello w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="c2157-125">Uruchamia aplikację logiki w OMS, tooview [wykonaj te czynności](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="c2157-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="c2157-126">Instalowanie rozwiązania do zarządzania aplikacje logiki hello w OMS</span><span class="sxs-lookup"><span data-stu-id="c2157-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="c2157-127">Jeśli już włączone analizy dzienników, podczas tworzenia aplikacji logiki, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="c2157-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="c2157-128">Masz już rozwiązania do zarządzania aplikacje logiki hello zainstalowane w OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="c2157-129">W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="c2157-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c2157-130">Wyszukaj "analizy dzienników" jako filtr, a następnie wybierz pozycję **analizy dzienników** pokazany:</span><span class="sxs-lookup"><span data-stu-id="c2157-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Wybierz pozycję "Analizy dzienników"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="c2157-132">W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Wybierz obszar roboczy OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="c2157-134">W obszarze **zarządzania**, wybierz **portalu OMS**.</span><span class="sxs-lookup"><span data-stu-id="c2157-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Wybierz pozycję "Portalu OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="c2157-136">Na stronie głównej OMS zostanie wyświetlony Baner uaktualnienia hello, jeśli transparent hello tak, aby najpierw uaktualnić obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="c2157-137">Następnie wybierz pozycję **galerii rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="c2157-137">Then choose **Solutions Gallery**.</span></span>

   ![Wybierz pozycję "Rozwiązań Galeria"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="c2157-139">W obszarze **wszystkie rozwiązania**, Znajdź i wybierz Kafelek hello hello **zarządzania aplikacje logiki** rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c2157-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Wybierz pozycję "Zarządzanie aplikacje logiki"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="c2157-141">Wybierz rozwiązanie hello tooinstall w obszarze roboczym pakietu OMS, **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c2157-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Wybierz opcję "Dodaj", "Zarządzania aplikacjami logiki"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="c2157-143">Widok, który uruchamia aplikację logiki w obszarze roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="c2157-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="c2157-144">Stan aplikacji logiki i liczba hello tooview wykonywany, strony Przegląd toohello przejdź do obszaru roboczego OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="c2157-145">Przejrzyj szczegóły hello na powitania **zarządzania aplikacje logiki** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c2157-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Wyświetlanie stanu i liczba Uruchom aplikację logiki kafelka przeglądu](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="c2157-147">Jeśli transparent uaktualnienia pojawia się zamiast hello kafelka zarządzania aplikacji logiki, wybierz hello transparentu, tak, aby najpierw uaktualnić obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="c2157-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Uaktualnij "Obszarem roboczym pakietu OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="c2157-149">tooview podsumowanie zawierający więcej szczegółów dotyczących sekwencji aplikacji logiki, wybierz hello **zarządzania aplikacje logiki** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c2157-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="c2157-150">W tym miejscu że aplikacja działa logiki są pogrupowane według nazwy lub stan wykonania.</span><span class="sxs-lookup"><span data-stu-id="c2157-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Uruchamia aplikację logiki podsumowanie stanu](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="c2157-152">tooview, którego wszystkie hello jest uruchamiany dla konkretnej logiki aplikacji lub stan, wybierz hello wiersza aplikacji logiki lub stanu.</span><span class="sxs-lookup"><span data-stu-id="c2157-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="c2157-153">Oto przykład pokazujący wszystkie elementy hello konkretnej logiki aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c2157-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Widok jest uruchamiana dla aplikacji logiki lub stanu](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="c2157-155">Witaj **ponowne przesłanie** "Yes" w kolumnie jest wyświetlana dla przebiegów wynikających z wykonywania ponownie przesłane.</span><span class="sxs-lookup"><span data-stu-id="c2157-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="c2157-156">toofilter tych wyników, można wykonać filtrowania zarówno po stronie klienta i po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="c2157-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="c2157-157">Filtr po stronie klienta: dla każdej kolumny wybierz hello filtry, które mają.</span><span class="sxs-lookup"><span data-stu-id="c2157-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="c2157-158">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="c2157-158">Here are some examples:</span></span>

     ![Przykładowe filtry kolumn](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="c2157-160">Filtr po stronie serwera: toochoose określony czas okna lub toolimit hello szereg uruchomień występować, użyj hello zakresu kontroli u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c2157-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="c2157-161">Domyślnie są wyświetlane tylko 1000 rekordów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="c2157-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Przedział czasu hello zmiany](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="c2157-163">wszystkie tooview hello działań i ich szczegóły dla określonych wykonywania, wybierz opcję wiersza, który otwiera stronę wyszukiwania dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="c2157-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="c2157-164">Wybierz te informacje w tabeli, tooview **tabeli**.</span><span class="sxs-lookup"><span data-stu-id="c2157-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="c2157-165">Kwerenda hello toochange, można edytować hello ciągu zapytania w pasku szukania hello.</span><span class="sxs-lookup"><span data-stu-id="c2157-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="c2157-166">Aby lepiej wykorzystać możliwości wybierz **zaawansowane analizy**.</span><span class="sxs-lookup"><span data-stu-id="c2157-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Wyświetlanie akcji i szczegóły dotyczące uruchamiania aplikacji logiki](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="c2157-168">W tym miejscu na stronie hello Azure Log Analytics można aktualizować zapytania i widoku hello wynikiem hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="c2157-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="c2157-169">To zapytanie używa [język zapytań Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), który można edytować, jeśli chcesz, aby tooview różne wyniki.</span><span class="sxs-lookup"><span data-stu-id="c2157-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Analiza dzienników Azure - widok zapytania](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="c2157-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2157-171">Next steps</span></span>

* [<span data-ttu-id="c2157-172">Monitorowanie komunikatów B2B</span><span class="sxs-lookup"><span data-stu-id="c2157-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
