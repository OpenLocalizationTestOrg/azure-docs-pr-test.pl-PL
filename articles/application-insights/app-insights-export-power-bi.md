---
title: "aaaExport tooPower BI z usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Zapytania analityczne mogą być wyświetlane w usłudze Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="3526f-103">Źródła danych usługi Power BI z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="3526f-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="3526f-104">[Power BI](http://www.powerbi.com/) jest pakiet narzędzia do analizy biznesowe, które ułatwiają analizowanie danych i udostępniać informacji.</span><span class="sxs-lookup"><span data-stu-id="3526f-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="3526f-105">Pulpity nawigacyjne sformatowanego są dostępne na każdym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="3526f-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="3526f-106">Można połączyć dane z wielu źródeł, takich jak analiza zapytania z [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3526f-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="3526f-107">Istnieją trzy metody zalecane eksportowania tooPower dane usługi Application Insights BI.</span><span class="sxs-lookup"><span data-stu-id="3526f-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="3526f-108">Można ich używać oddzielnie lub razem.</span><span class="sxs-lookup"><span data-stu-id="3526f-108">You can use them separately or together.</span></span>

* <span data-ttu-id="3526f-109">[**Power BI karty** ](#power-pi-adapter) — skonfiguruj Tworzenie pulpitu nawigacyjnego dane telemetryczne z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3526f-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="3526f-110">wstępnie zdefiniowane Hello zbiór wykresy, ale można dodać własne zapytania z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="3526f-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="3526f-111">[**Eksportuj zapytania analityczne** ](#export-analytics-queries) -pisać zapytania przy użyciu analizy, a następnie wyeksportować go tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="3526f-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="3526f-112">To zapytanie można umieścić na pulpicie nawigacyjnym, wraz z innymi danymi.</span><span class="sxs-lookup"><span data-stu-id="3526f-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="3526f-113">[**Eksport ciągły i analiza strumienia** ](app-insights-export-stream-analytics.md) -się proces ten obejmuje więcej tooset pracy.</span><span class="sxs-lookup"><span data-stu-id="3526f-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="3526f-114">Jest on przydatny, gdy chcesz tookeep dane przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="3526f-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="3526f-115">W przeciwnym razie hello inne metody są zalecane.</span><span class="sxs-lookup"><span data-stu-id="3526f-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="3526f-116">Power BI karty</span><span class="sxs-lookup"><span data-stu-id="3526f-116">Power BI adapter</span></span>
<span data-ttu-id="3526f-117">Ta metoda tworzy pełne pulpitu nawigacyjnego dane telemetryczne dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3526f-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="3526f-118">wstępnie zdefiniowane Hello początkowego zestawu danych, ale można dodać więcej tooit danych.</span><span class="sxs-lookup"><span data-stu-id="3526f-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="3526f-119">Pobierz hello karty</span><span class="sxs-lookup"><span data-stu-id="3526f-119">Get hello adapter</span></span>
1. <span data-ttu-id="3526f-120">Zaloguj się za[usługi Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="3526f-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="3526f-121">Otwórz **Pobierz dane**, **usług**, **usługi Application Insights**</span><span class="sxs-lookup"><span data-stu-id="3526f-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Pobierz ze źródła danych usługi Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="3526f-123">Podaj szczegóły hello zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3526f-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Pobierz ze źródła danych usługi Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="3526f-125">Zaczekaj minutę lub dwie na toobe danych hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="3526f-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Power BI karty](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="3526f-127">Można edytować hello pulpitu nawigacyjnego, łączenie hello usługi Application Insights wykresów z systemami innych źródeł oraz z zapytaniami Analytics.</span><span class="sxs-lookup"><span data-stu-id="3526f-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="3526f-128">Brak galerii wizualizacji, gdzie uzyskasz więcej wykresów, a każdy wykres ma parametry, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="3526f-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="3526f-129">Po początkowej importu hello, hello pulpitu nawigacyjnego i raportów hello nadal tooupdate codziennie.</span><span class="sxs-lookup"><span data-stu-id="3526f-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="3526f-130">Można kontrolować harmonogram odświeżania hello na powitania zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3526f-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="3526f-131">Zapytania analityczne eksportu</span><span class="sxs-lookup"><span data-stu-id="3526f-131">Export Analytics queries</span></span>
<span data-ttu-id="3526f-132">Trasa ta umożliwia toowrite żadnych Analytics chcesz zbadać, a następnie wyeksportować tego pulpitu nawigacyjnego usługi Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="3526f-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="3526f-133">(Dodaj pulpit nawigacyjny toohello utworzone przez kartę hello).</span><span class="sxs-lookup"><span data-stu-id="3526f-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="3526f-134">Jeden raz: Zainstaluj Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3526f-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="3526f-135">tooimport kwerenda usługi Application Insights, użyj hello pulpitu wersja aplikacji Power BI.</span><span class="sxs-lookup"><span data-stu-id="3526f-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="3526f-136">Ale następnie można opublikować toohello sieci web lub tooyour roboczym chmury usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="3526f-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="3526f-137">Zainstaluj [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="3526f-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="3526f-138">Eksportuj zapytania analityka</span><span class="sxs-lookup"><span data-stu-id="3526f-138">Export an Analytics query</span></span>
1. <span data-ttu-id="3526f-139">[Otwórz Analytics i zapisać zapytanie](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="3526f-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="3526f-140">Testowanie i kwerendzie hello dopóki zakończeniu modyfikowania hello wyników.</span><span class="sxs-lookup"><span data-stu-id="3526f-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="3526f-141">**Upewnij się, kwerendy hello działa prawidłowo w module analiz przed go wyeksportować.**</span><span class="sxs-lookup"><span data-stu-id="3526f-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="3526f-142">Na powitania **wyeksportować** menu, wybierz **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="3526f-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="3526f-143">Zapisz plik tekstowy hello.</span><span class="sxs-lookup"><span data-stu-id="3526f-143">Save hello text file.</span></span>
   
    ![Eksportuj zapytania usługi Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="3526f-145">Wybierz Power BI Desktop w **pobieranie danych, pustą zapytania** , a następnie w hello zapytania edytora, w obszarze **widoku** wybierz **zaawansowany Edytor zapytań**.</span><span class="sxs-lookup"><span data-stu-id="3526f-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="3526f-146">Wklej hello wyeksportowane M język skryptu do hello zaawansowany Edytor zapytań.</span><span class="sxs-lookup"><span data-stu-id="3526f-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Edytor zaawansowanych zapytań](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="3526f-148">Konieczne może być tooprovide poświadczenia tooallow usługi Power BI tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="3526f-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="3526f-149">Użyj toosign "konta organizacyjnego" przy użyciu swojego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3526f-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Podaj poświadczenia Azure tooenable usługi Power BI toorun kwerenda usługi Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="3526f-151">(Tooverify hello poświadczeń, należy użyć hello ustawienia źródła danych menu polecenia hello edytora zapytań.</span><span class="sxs-lookup"><span data-stu-id="3526f-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="3526f-152">Zwróć uwagę na to toospecify hello poświadczeń, których można użyć dla platformy Azure, która może być inny niż poświadczenia dla usługi Power BI.)</span><span class="sxs-lookup"><span data-stu-id="3526f-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="3526f-153">Wybierz wizualizacji zapytania i wybierz pola hello osi x, y i podzielenie wymiaru.</span><span class="sxs-lookup"><span data-stu-id="3526f-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Wybierz wizualizację](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="3526f-155">Opublikuj obszar roboczy chmury raportu tooyour usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="3526f-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="3526f-156">Z tego miejsca można osadzić zsynchronizowanej wersji do innych stron sieci web.</span><span class="sxs-lookup"><span data-stu-id="3526f-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Wybierz wizualizację](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="3526f-158">Ręcznie odświeżyć raport hello w odstępach czasu, lub skonfigurowania zaplanowanego odświeżania na stronie Opcje hello.</span><span class="sxs-lookup"><span data-stu-id="3526f-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3526f-159">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="3526f-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="3526f-160">401 lub 403 bez autoryzacji</span><span class="sxs-lookup"><span data-stu-id="3526f-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="3526f-161">Może to nastąpić, jeśli refesh token nie został zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="3526f-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="3526f-162">Spróbuj tooensure te kroki, nadal mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="3526f-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="3526f-163">Jeśli masz dostęp, a poświadczenia hello refershing nie działa, otwórz bilet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="3526f-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="3526f-164">Zaloguj się do portalu Azure hello i upewnij się, że można uzyskać dostępu do zasobów hello</span><span class="sxs-lookup"><span data-stu-id="3526f-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="3526f-165">Spróbuj toorefresh poświadczenia hello hello pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="3526f-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="3526f-166">502 Niewłaściwa brama</span><span class="sxs-lookup"><span data-stu-id="3526f-166">502 Bad Gateway</span></span>
<span data-ttu-id="3526f-167">Jest to zazwyczaj spowodowane Analytics kwerendę, która zwraca za dużo danych.</span><span class="sxs-lookup"><span data-stu-id="3526f-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="3526f-168">Spróbuj użyć przy użyciu mniejszego zakresu czasu lub za pomocą hello [temu](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) lub [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) działa tylko [projektu](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello potrzebne pola.</span><span class="sxs-lookup"><span data-stu-id="3526f-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="3526f-169">Jeśli zmniejszenie hello zestawu danych pochodzących z hello Analytics query nie spełnia wymagań należy rozważyć użycie hello [interfejsu API](https://dev.applicationinsights.io/documentation/overview) toopull większy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="3526f-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="3526f-170">Poniżej przedstawiono instrukcje eksportowania hello tooconvert M zapytania hello toouse interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3526f-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="3526f-171">Utwórz [klucz interfejsu API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="3526f-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="3526f-172">Adres URL ARM z interfejsem API AI hello hello aktualizacji skryptu Power BI M, wyeksportowany z usługi Analytics zastępując (zobacz poniższy przykład)</span><span class="sxs-lookup"><span data-stu-id="3526f-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="3526f-173">Zastąp **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="3526f-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="3526f-174">**https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="3526f-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="3526f-175">Na koniec Zaktualizuj poświadczenia toobasic i korzystania z klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3526f-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="3526f-176">**Istniejący skrypt**</span><span class="sxs-lookup"><span data-stu-id="3526f-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="3526f-177">**Zaktualizowany skrypt**</span><span class="sxs-lookup"><span data-stu-id="3526f-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="3526f-178">O pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="3526f-178">About sampling</span></span>
<span data-ttu-id="3526f-179">Jeśli aplikacja wyśle dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii.</span><span class="sxs-lookup"><span data-stu-id="3526f-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="3526f-180">Witaj, które same ma wartość true, jeśli ręcznie ustawiono próbkowania hello zestawu SDK lub na wprowadzanie.</span><span class="sxs-lookup"><span data-stu-id="3526f-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="3526f-181">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="3526f-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="3526f-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3526f-182">Next steps</span></span>
* [<span data-ttu-id="3526f-183">Power BI — informacje</span><span class="sxs-lookup"><span data-stu-id="3526f-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="3526f-184">Samouczek analityka</span><span class="sxs-lookup"><span data-stu-id="3526f-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

