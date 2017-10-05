---
title: "Eksportowanie przy użyciu usługi Stream Analytics z usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analiza strumienia stale można przekształcić, filtrować i przekazywanie danych, które możesz wyeksportować z usługi Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="1acd3-103">Używać usługi Stream Analytics do przetworzenia wyeksportowane dane z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="1acd3-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="1acd3-104">[Usługa Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) to idealne narzędzie do przetwarzania danych [wyeksportowany z usługi Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="1acd3-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="1acd3-105">Analiza strumienia może pobierają dane z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="1acd3-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="1acd3-106">Go transformacji i filtrowanie danych i kierowania go do różnych sink.</span><span class="sxs-lookup"><span data-stu-id="1acd3-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="1acd3-107">W tym przykładzie utworzymy Adapter pobiera dane z usługi Application Insights, zmiana nazwy i przetwarza część pól, która powoduje przekazanie w potoku go do usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="1acd3-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="1acd3-108">Są znacznie lepsze i łatwiejsze [zalecane sposoby wyświetlania danych usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="1acd3-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="1acd3-109">Ścieżka przedstawione w tym miejscu jest po prostu przykład ilustrujący sposób przetwarzania wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="1acd3-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Diagram blokowy eksportu przez administratora systemu do PBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="1acd3-111">Tworzenie magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1acd3-111">Create storage in Azure</span></span>
<span data-ttu-id="1acd3-112">Eksport ciągły zawsze generuje dane do konta usługi Azure Storage, należy najpierw utworzyć magazyn.</span><span class="sxs-lookup"><span data-stu-id="1acd3-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="1acd3-113">Utwórz konto magazynu "klasycznym" w ramach subskrypcji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1acd3-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![W portalu Azure wybierz opcję Nowy, danych, magazynu](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="1acd3-115">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="1acd3-115">Create a container</span></span>
   
    ![W nowym magazynie wybierz kontenery, kliknij Kafelek kontenerów, a następnie dodaj](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="1acd3-117">Skopiuj klucz dostępu do magazynu</span><span class="sxs-lookup"><span data-stu-id="1acd3-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="1acd3-118">Należy ją szybko, aby skonfigurować dane wejściowe usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="1acd3-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![W magazynie Otwórz ustawienia kluczy i wykonać kopię podstawowego klucza dostępu](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="1acd3-120">Rozpocząć eksport ciągły w celu magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="1acd3-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="1acd3-121">[Eksport ciągły](app-insights-export-telemetry.md) przenosi dane z usługi Application Insights do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1acd3-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="1acd3-122">W portalu Azure przejdź do zasobu usługi Application Insights, utworzone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1acd3-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Kliknij przycisk Przeglądaj, usługi Application Insights aplikacji](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="1acd3-124">Utwórz eksport ciągły.</span><span class="sxs-lookup"><span data-stu-id="1acd3-124">Create a continuous export.</span></span>
   
    ![Wybierz ustawienia, Eksport ciągły](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="1acd3-126">Wybierz utworzone wcześniej konto magazynu:</span><span class="sxs-lookup"><span data-stu-id="1acd3-126">Select the storage account you created earlier:</span></span>

    ![Skonfiguruj docelowego eksportu](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="1acd3-128">Ustaw typy zdarzeń, które chcesz wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="1acd3-128">Set the event types you want to see:</span></span>

    ![Wybierz typy zdarzeń](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="1acd3-130">Let niektóre dane gromadzone.</span><span class="sxs-lookup"><span data-stu-id="1acd3-130">Let some data accumulate.</span></span> <span data-ttu-id="1acd3-131">Zaczekaj i innym użytkownikom za pomocą aplikacji przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="1acd3-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="1acd3-132">Dane telemetryczne wejdzie i zobaczysz statystyczne wykresów w [Eksploratora metryk](app-insights-metrics-explorer.md) i zdarzeń z [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1acd3-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="1acd3-133">A także będzie eksportować dane do usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="1acd3-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="1acd3-134">Sprawdź, czy wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="1acd3-134">Inspect the exported data.</span></span> <span data-ttu-id="1acd3-135">W programie Visual Studio, wybierz **wyświetlić / w chmurze Explorer**i otwórz Azure / magazynu.</span><span class="sxs-lookup"><span data-stu-id="1acd3-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="1acd3-136">(Jeśli nie masz tej opcji menu, należy zainstalować zestaw Azure SDK: Otwórz okno dialogowe nowego projektu i Otwórz program Visual C# / w chmurze / Get Microsoft Azure SDK dla platformy .NET.)</span><span class="sxs-lookup"><span data-stu-id="1acd3-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="1acd3-137">Zanotuj części wspólnej nazwy ścieżki, która jest pochodną klucz nazwy i instrumentacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1acd3-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="1acd3-138">Zdarzenia są zapisywane do obiektu blob pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="1acd3-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="1acd3-139">Każdy plik może zawierać co najmniej jednego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="1acd3-139">Each file may contain one or more events.</span></span> <span data-ttu-id="1acd3-140">Dlatego chcemy odczytuje dane zdarzenia i filtrować polami, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="1acd3-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="1acd3-141">Wszystkie rodzaje czynności, które firma Microsoft może wykonywać z danymi, ale naszego planu jest obecnie przekazać dane do usługi Power BI za pomocą usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="1acd3-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="1acd3-142">Utwórz wystąpienie usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1acd3-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="1acd3-143">Z [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz usługę Azure Stream Analytics i utworzyć nowe zadanie usługi Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="1acd3-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="1acd3-144">Po utworzeniu nowego zadania, należy rozwinąć jego szczegóły:</span><span class="sxs-lookup"><span data-stu-id="1acd3-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="1acd3-145">Ustawianie lokalizacji obiektu blob</span><span class="sxs-lookup"><span data-stu-id="1acd3-145">Set blob location</span></span>
<span data-ttu-id="1acd3-146">Ustaw, aby pobrać dane wejściowe z obiektu blob z eksportu ciągłego:</span><span class="sxs-lookup"><span data-stu-id="1acd3-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="1acd3-147">Teraz musisz podstawowy klucz dostępu z konta magazynu, który wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="1acd3-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="1acd3-148">Ustaw jako klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1acd3-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="1acd3-149">Wzorzec prefiksu ścieżki zestawu</span><span class="sxs-lookup"><span data-stu-id="1acd3-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="1acd3-150">**Pamiętaj ustawienie formatu RRRR-MM-DD (Łączniki).**</span><span class="sxs-lookup"><span data-stu-id="1acd3-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="1acd3-151">Ścieżka prefiksu wzorzec Określa, gdzie Stream Analytics wyszukuje pliki wejściowe w magazynie.</span><span class="sxs-lookup"><span data-stu-id="1acd3-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="1acd3-152">Należy ustawić odpowiadają jak eksportu ciągłego przechowuje dane.</span><span class="sxs-lookup"><span data-stu-id="1acd3-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="1acd3-153">Ustaw go następująco:</span><span class="sxs-lookup"><span data-stu-id="1acd3-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="1acd3-154">W tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1acd3-154">In this example:</span></span>

* <span data-ttu-id="1acd3-155">`webapplication27`jest to nazwa zasobu usługi Application Insights **małe litery**.</span><span class="sxs-lookup"><span data-stu-id="1acd3-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="1acd3-156">`1234...`jest to klucz Instrumentacji zasobu usługi Application Insights **pominięcie łączniki**.</span><span class="sxs-lookup"><span data-stu-id="1acd3-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="1acd3-157">`PageViews`jest to typ danych, które mają być analizowane.</span><span class="sxs-lookup"><span data-stu-id="1acd3-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="1acd3-158">Dostępne typy są zależne od filtr ustawionych w eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="1acd3-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="1acd3-159">Sprawdź wyeksportowane dane na temat dostępnych typów oraz temat [wyeksportować modelu danych](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="1acd3-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="1acd3-160">`/{date}/{time}`wzorzec są zapisywane jako literału.</span><span class="sxs-lookup"><span data-stu-id="1acd3-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="1acd3-161">Sprawdź, czy Magazyn upewnij się, że można uzyskać ścieżki prawo.</span><span class="sxs-lookup"><span data-stu-id="1acd3-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="1acd3-162">Zakończ początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1acd3-162">Finish initial setup</span></span>
<span data-ttu-id="1acd3-163">Upewnij się, format serializacji:</span><span class="sxs-lookup"><span data-stu-id="1acd3-163">Confirm the serialization format:</span></span>

![Potwierdź i zamknąć kreatora](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="1acd3-165">Zamknij kreatora i poczekaj, aż do ukończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="1acd3-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="1acd3-166">Polecenie przykładowe można pobrać niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="1acd3-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="1acd3-167">Zachowaj go jako przykład testu, aby debugować zapytania.</span><span class="sxs-lookup"><span data-stu-id="1acd3-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="1acd3-168">Ustaw dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="1acd3-168">Set the output</span></span>
<span data-ttu-id="1acd3-169">Wybierz swoją pracę i ustawić dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1acd3-169">Now select your job and set the output.</span></span>

![Wybierz nowy kanał, kliknij pozycję dane wyjściowe, Dodaj usługi Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="1acd3-171">Podaj Twojej **konto służbowe** do autoryzacji Stream Analytics, aby uzyskać dostęp do zasobów usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="1acd3-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="1acd3-172">Następnie magazynowa nazwę dla danych wyjściowych i docelowy zestaw danych z usługi Power BI i tabeli.</span><span class="sxs-lookup"><span data-stu-id="1acd3-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Trzy nazwy magazynu](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="1acd3-174">Ustawianie zapytania</span><span class="sxs-lookup"><span data-stu-id="1acd3-174">Set the query</span></span>
<span data-ttu-id="1acd3-175">Zapytanie podlega translacji z danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1acd3-175">The query governs the translation from input to output.</span></span>

![Wybierz zadanie, a następnie kliknij przycisk zapytanie.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="1acd3-178">Funkcja testu Aby sprawdzić, czy możesz uzyskać prawo danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1acd3-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="1acd3-179">Nadaj przykładowych danych, które miał na stronie dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="1acd3-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="1acd3-180">Aby wyświetlić liczby zdarzeń</span><span class="sxs-lookup"><span data-stu-id="1acd3-180">Query to display counts of events</span></span>
<span data-ttu-id="1acd3-181">Wklej tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="1acd3-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="1acd3-182">dane wejściowe eksportu jest alias, który firma Microsoft udostępniła do strumienia danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="1acd3-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="1acd3-183">dane wyjściowe pbi jest alias wyjściowy, który zdefiniowanego</span><span class="sxs-lookup"><span data-stu-id="1acd3-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="1acd3-184">Używamy [zewnętrzne GetElements ZASTOSOWAĆ](https://msdn.microsoft.com/library/azure/dn706229.aspx) ponieważ nazwa zdarzenia jest zagnieżdżony arrray JSON.</span><span class="sxs-lookup"><span data-stu-id="1acd3-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="1acd3-185">Następnie wybierz wybiera nazwę zdarzenia, wraz z licznik wystąpienia o tej nazwie w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="1acd3-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="1acd3-186">[Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) klauzuli grupuje elementy w okresach czasu wynoszącym 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="1acd3-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="1acd3-187">Aby wyświetlić wartości metryki</span><span class="sxs-lookup"><span data-stu-id="1acd3-187">Query to display metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="1acd3-188">To zapytanie bardziej szczegółowy na dane telemetryczne metryki można pobrać czasu zdarzenia i wartość metryki.</span><span class="sxs-lookup"><span data-stu-id="1acd3-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="1acd3-189">Wartości metryki znajdują się wewnątrz tablicy, więc używamy zewnętrzne GetElements Zastosuj wzorzec wyodrębniać wiersze.</span><span class="sxs-lookup"><span data-stu-id="1acd3-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="1acd3-190">"myMetric" w tym przypadku jest nazwa metryki.</span><span class="sxs-lookup"><span data-stu-id="1acd3-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="1acd3-191">Zapytanie zawierało wartości właściwości wymiaru</span><span class="sxs-lookup"><span data-stu-id="1acd3-191">Query to include values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="1acd3-192">To zapytanie zawiera wartości bez właściwości wymiaru, w zależności od określonego wymiaru w stałej indeks w tablicy wymiaru.</span><span class="sxs-lookup"><span data-stu-id="1acd3-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="1acd3-193">Uruchamianie zadania</span><span class="sxs-lookup"><span data-stu-id="1acd3-193">Run the job</span></span>
<span data-ttu-id="1acd3-194">W przeszłości, aby uruchomić zadanie z można wybrać datę.</span><span class="sxs-lookup"><span data-stu-id="1acd3-194">You can select a date in the past to start the job from.</span></span> 

![Wybierz zadanie, a następnie kliknij przycisk zapytanie.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="1acd3-197">Zaczekaj, aż zadanie jest uruchomione.</span><span class="sxs-lookup"><span data-stu-id="1acd3-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="1acd3-198">Zobacz wyniki w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="1acd3-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="1acd3-199">Są znacznie lepsze i łatwiejsze [zalecane sposoby wyświetlania danych usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="1acd3-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="1acd3-200">Ścieżka przedstawione w tym miejscu jest po prostu przykład ilustrujący sposób przetwarzania wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="1acd3-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="1acd3-201">Otwórz usługę Power BI pracy lub konta służbowego, a następnie wybierz zestaw danych i tabeli, która jest zdefiniowana jako dane wyjściowe zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="1acd3-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="1acd3-203">Teraz można używać tego zestawu danych, raportów i pulpitów nawigacyjnych w [usługi Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1acd3-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="1acd3-205">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="1acd3-205">No data?</span></span>
* <span data-ttu-id="1acd3-206">Sprawdź, że [ustawić format daty](#set-path-prefix-pattern) poprawnie do RRRR-MM-DD (z kreskami).</span><span class="sxs-lookup"><span data-stu-id="1acd3-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="1acd3-207">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="1acd3-207">Video</span></span>
<span data-ttu-id="1acd3-208">Noam Ben Zeev pokazuje, jak można przetworzyć wyeksportowane dane przy użyciu usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1acd3-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1acd3-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1acd3-209">Next steps</span></span>
* [<span data-ttu-id="1acd3-210">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="1acd3-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="1acd3-211">Szczegółowe dane modelu odwołania dla typów właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="1acd3-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="1acd3-212">Usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="1acd3-212">Application Insights</span></span>](app-insights-overview.md)

