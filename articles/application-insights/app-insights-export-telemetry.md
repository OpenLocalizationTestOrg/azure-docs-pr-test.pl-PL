---
title: "Eksport ciągły dane telemetryczne z usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Eksportuj dane diagnostyczne i użycia do magazynu w systemie Microsoft Azure i pobrać ją stamtąd."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="e365c-103">Eksportuj dane telemetryczne z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e365c-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="e365c-104">Czy chcesz zachować telemetrii przez czas dłuższy niż okres przechowywania standardowe?</span><span class="sxs-lookup"><span data-stu-id="e365c-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="e365c-105">Lub przetwarzać dane w jakiś sposób specjalne?</span><span class="sxs-lookup"><span data-stu-id="e365c-105">Or process it in some specialized way?</span></span> <span data-ttu-id="e365c-106">Eksport ciągły jest idealna to.</span><span class="sxs-lookup"><span data-stu-id="e365c-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="e365c-107">Zdarzenia, które są widoczne w portalu usługi Application Insights można wyeksportować do magazynu na platformie Microsoft Azure w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="e365c-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="e365c-108">Z tego miejsca można pobrać danych i zapisu, niezależnie od kod należy go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="e365c-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="e365c-109">Przy użyciu eksportu ciągłego może pociągnąć za sobą dodatkowe opłaty.</span><span class="sxs-lookup"><span data-stu-id="e365c-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="e365c-110">Sprawdź Twojej [model cenowy](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="e365c-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="e365c-111">Przed skonfigurowaniem Eksport ciągły istnieje kilka rozwiązań alternatywnych, które należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="e365c-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="e365c-112">Przycisk Eksportuj w górnej części bloku metryki lub wyszukiwanie umożliwia transfer tabele i wykresy do arkusz kalkulacyjny programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e365c-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="e365c-113">[Analiza](app-insights-analytics.md) zapewnia język kwerendy zaawansowanych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e365c-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="e365c-114">Można także wyeksportować wyniki.</span><span class="sxs-lookup"><span data-stu-id="e365c-114">It can also export results.</span></span>
* <span data-ttu-id="e365c-115">Jeśli szukasz do [eksplorować dane w usłudze Power BI](app-insights-export-power-bi.md), możesz to zrobić bez użycia eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="e365c-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="e365c-116">[Dostępu do danych interfejsu API REST](https://dev.applicationinsights.io/) pozwala uzyskiwać dostęp do telemetrii programowo.</span><span class="sxs-lookup"><span data-stu-id="e365c-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="e365c-117">Po eksportu ciągłego kopiuje dane do magazynu (gdzie pozostawał dla tak długo, jak chcesz), jest on nadal dostępny w usłudze Application Insights dla zwykle [okres przechowywania](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="e365c-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="e365c-118"><a name="setup"></a>Utwórz eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="e365c-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="e365c-119">Zasób usługi Application Insights dla aplikacji, otwórz eksportu ciągłego i wybierz polecenie **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="e365c-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Przewiń w dół i kliknij przycisk eksportu ciągłego](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="e365c-121">Wybierz typy danych, który chcesz wyeksportować telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e365c-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="e365c-122">Utwórz lub wybierz [konto magazynu Azure](../storage/common/storage-introduction.md) której chcesz przechowywać dane.</span><span class="sxs-lookup"><span data-stu-id="e365c-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="e365c-123">Domyślnie zostanie ustawiona lokalizacja magazynu do tego samego regionu geograficznego co zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e365c-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="e365c-124">Jeśli jest przechowywany w innym regionie, może spowodować naliczenie opłat transferu.</span><span class="sxs-lookup"><span data-stu-id="e365c-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Kliknij przycisk Dodaj, wyeksportować miejsce docelowe konto magazynu, a następnie utwórz nowy magazyn lub wybierz istniejący magazyn](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="e365c-126">Utwórz lub Wybierz kontener magazynu:</span><span class="sxs-lookup"><span data-stu-id="e365c-126">Create or select a container in the storage:</span></span>

    ![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="e365c-128">Po utworzeniu eksportu uruchamia przejście.</span><span class="sxs-lookup"><span data-stu-id="e365c-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="e365c-129">Tylko Pobierz dane przychodzący po utworzeniu eksportu.</span><span class="sxs-lookup"><span data-stu-id="e365c-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="e365c-130">Może to być opóźnienie około godziny przed wyświetleniem danych w magazynie.</span><span class="sxs-lookup"><span data-stu-id="e365c-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="e365c-131">Aby edytować Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="e365c-131">To edit continuous export</span></span>

<span data-ttu-id="e365c-132">Jeśli chcesz zmienić typy zdarzeń, które później, po prostu edytować Eksport:</span><span class="sxs-lookup"><span data-stu-id="e365c-132">If you want to change the event types later, just edit the export:</span></span>

![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="e365c-134">Aby zatrzymać eksportu ciągłego</span><span class="sxs-lookup"><span data-stu-id="e365c-134">To stop continuous export</span></span>

<span data-ttu-id="e365c-135">Aby zatrzymać eksportu, kliknij pozycję Wyłącz.</span><span class="sxs-lookup"><span data-stu-id="e365c-135">To stop the export, click Disable.</span></span> <span data-ttu-id="e365c-136">Po kliknięciu włączyć ponownie, eksport zostanie uruchomiony ponownie z nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="e365c-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="e365c-137">Nie otrzymasz dane, które dotarły w portalu podczas eksportowania została wyłączona.</span><span class="sxs-lookup"><span data-stu-id="e365c-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="e365c-138">Aby zatrzymać trwale eksportu, usuń go.</span><span class="sxs-lookup"><span data-stu-id="e365c-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="e365c-139">Dzięki temu nie powoduje usunięcia danych z magazynu.</span><span class="sxs-lookup"><span data-stu-id="e365c-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="e365c-140">Nie można dodać lub zmienić eksportu?</span><span class="sxs-lookup"><span data-stu-id="e365c-140">Can't add or change an export?</span></span>
* <span data-ttu-id="e365c-141">Aby dodać lub zmienić eksportu, niezbędne są uprawnienia dostępu do właściciela, współautora lub współautora wgląd w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e365c-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="e365c-142">[Dowiedz się więcej o rolach][roles].</span><span class="sxs-lookup"><span data-stu-id="e365c-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="e365c-143"><a name="analyze"></a>Jakie zdarzenia uzyskać?</span><span class="sxs-lookup"><span data-stu-id="e365c-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="e365c-144">Wyeksportowane dane jest nieprzetworzone dane telemetryczne, otrzymywanych z aplikacji, ale dodamy danych lokalizacji, które firma Microsoft obliczenia z adresu IP klienta.</span><span class="sxs-lookup"><span data-stu-id="e365c-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="e365c-145">Dane, które zostały odrzucone przez [próbkowania](app-insights-sampling.md) nie wchodzi w wyeksportowanych danych.</span><span class="sxs-lookup"><span data-stu-id="e365c-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="e365c-146">Inne metryki obliczanej nie są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="e365c-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="e365c-147">Na przykład firma Microsoft nie Eksportuj średnie wykorzystanie procesora CPU, ale eksportowania nieprzetworzone dane telemetryczne, z którego jest obliczana średnia.</span><span class="sxs-lookup"><span data-stu-id="e365c-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="e365c-148">Dane obejmują także wyniki dowolnego [testów sieci web dostępności](app-insights-monitor-web-app-availability.md) , które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="e365c-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="e365c-149">**Próbkowania.**</span><span class="sxs-lookup"><span data-stu-id="e365c-149">**Sampling.**</span></span> <span data-ttu-id="e365c-150">Jeśli aplikacja wyśle dużą ilość danych, funkcję pobierania próbek może działać i wysłać tylko część wygenerowanego telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e365c-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="e365c-151">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e365c-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="e365c-152"><a name="get"></a>Sprawdź dane</span><span class="sxs-lookup"><span data-stu-id="e365c-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="e365c-153">Możesz sprawdzić magazynu bezpośrednio w portalu.</span><span class="sxs-lookup"><span data-stu-id="e365c-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="e365c-154">Kliknij przycisk **Przeglądaj**, wybierz konto magazynu, a następnie otwórz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="e365c-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="e365c-155">Aby sprawdzić magazynu Azure w programie Visual Studio, otwórz **widoku**, **Eksplorator chmury**.</span><span class="sxs-lookup"><span data-stu-id="e365c-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="e365c-156">(Jeśli nie masz tego polecenia menu, należy zainstalować zestaw Azure SDK: Otwórz **nowy projekt** okna dialogowego, rozwiń węzeł Visual C# / w chmurze i wybierz polecenie **pobrać zestaw Microsoft Azure SDK dla platformy .NET**.)</span><span class="sxs-lookup"><span data-stu-id="e365c-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="e365c-157">Po otwarciu magazynie obiektów blob, zobaczysz kontener z zestawu plików obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e365c-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="e365c-158">Identyfikator URI poszczególnych plików pochodząca z nazwę zasobu usługi Application Insights, jego klucza instrumentacji, telemetrii — typ, datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="e365c-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="e365c-159">(Nazwa zasobu jest tylko małe litery i łączniki pomija klucza instrumentacji.)</span><span class="sxs-lookup"><span data-stu-id="e365c-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Sprawdź magazynu obiektów blob za pomocą odpowiedniego narzędzia](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="e365c-161">Data i godzina są UTC i gdy telemetrii został złożony w magazynie — nie czas, który został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e365c-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="e365c-162">Dlatego podczas pisania kodu, aby pobrać dane, jego można przesuwać liniowo danych.</span><span class="sxs-lookup"><span data-stu-id="e365c-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="e365c-163">Poniżej przedstawiono formularz ścieżki:</span><span class="sxs-lookup"><span data-stu-id="e365c-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="e365c-164">gdzie</span><span class="sxs-lookup"><span data-stu-id="e365c-164">Where</span></span>

* <span data-ttu-id="e365c-165">`blobCreationTimeUtc`Godzina utworzenia obiektu blob w wewnętrznej jest przemieszczania magazynu</span><span class="sxs-lookup"><span data-stu-id="e365c-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="e365c-166">`blobDeliveryTimeUtc`to czas, kiedy obiekt blob jest kopiowany do magazynu docelowego eksportu</span><span class="sxs-lookup"><span data-stu-id="e365c-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="e365c-167"><a name="format"></a>Format danych</span><span class="sxs-lookup"><span data-stu-id="e365c-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="e365c-168">Każdy obiekt blob jest to plik tekstowy, który zawiera wiele "\n'-separated wierszy.</span><span class="sxs-lookup"><span data-stu-id="e365c-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="e365c-169">Zawiera on telemetrii przetwarzane w czasie około pół minuty.</span><span class="sxs-lookup"><span data-stu-id="e365c-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="e365c-170">Każdy wiersz reprezentuje punktu danych telemetrii, takich jak żądania lub strony widoku.</span><span class="sxs-lookup"><span data-stu-id="e365c-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="e365c-171">Każdy wiersz jest niesformatowany dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="e365c-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="e365c-172">Jeśli sit i stare jego, otwórz go w programie Visual Studio i wybierz pozycję Edytuj, zaawansowane, Format pliku:</span><span class="sxs-lookup"><span data-stu-id="e365c-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Wyświetl dane telemetryczne z narzędziem do odpowiedniego](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="e365c-174">Okresach czasu są w taktach, gdzie znaczniki 10 000 = 1 MS.</span><span class="sxs-lookup"><span data-stu-id="e365c-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="e365c-175">Na przykład te wartości pokazują czas 1 MS, aby wysłać żądanie z przeglądarki, 3ms do odbierania go i 1.8s do przetwarzania tej strony w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="e365c-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="e365c-176">Szczegółowe dane modelu odwołania dla typów właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="e365c-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="e365c-177">Przetwarzanie danych</span><span class="sxs-lookup"><span data-stu-id="e365c-177">Processing the data</span></span>
<span data-ttu-id="e365c-178">Na małą skalę można napisać kod służący do pobierania danych, przeczytaj je do arkusza kalkulacyjnego i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e365c-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="e365c-179">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e365c-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="e365c-180">Dla większych przykładowy kod, zobacz [przy użyciu roli procesu roboczego][exportasa].</span><span class="sxs-lookup"><span data-stu-id="e365c-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="e365c-181"><a name="delete"></a>Usuń stare dane</span><span class="sxs-lookup"><span data-stu-id="e365c-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="e365c-182">Należy pamiętać, że jest odpowiedzialny za zarządzanie pojemności pamięci masowej i usuwania starych danych, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e365c-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="e365c-183">Jeśli musisz ponownie wygenerować klucz magazynu...</span><span class="sxs-lookup"><span data-stu-id="e365c-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="e365c-184">Jeśli zmienisz klucz magazynu, Eksport ciągły przestaną działać.</span><span class="sxs-lookup"><span data-stu-id="e365c-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="e365c-185">Zostanie wyświetlone powiadomienie na koncie Azure.</span><span class="sxs-lookup"><span data-stu-id="e365c-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="e365c-186">Otwarcie bloku eksportu ciągłego i edytowanie eksportu.</span><span class="sxs-lookup"><span data-stu-id="e365c-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="e365c-187">Edytowanie docelowego eksportu, ale pozostaw tego samego magazynu wybrane.</span><span class="sxs-lookup"><span data-stu-id="e365c-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="e365c-188">Kliknij przycisk OK, aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="e365c-188">Click OK to confirm.</span></span>

![Edytuj Eksport ciągły otwierających i zamykających ją miejsce docelowe eksportu.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="e365c-190">Eksport ciągły zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="e365c-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="e365c-191">Przykłady eksportu</span><span class="sxs-lookup"><span data-stu-id="e365c-191">Export samples</span></span>

* <span data-ttu-id="e365c-192">[Eksportowanie do bazy danych SQL przy użyciu usługi analiza strumienia][exportasa]</span><span class="sxs-lookup"><span data-stu-id="e365c-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="e365c-193">Stream Analytics próbki 2</span><span class="sxs-lookup"><span data-stu-id="e365c-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="e365c-194">Na większą skalę, należy wziąć pod uwagę [HDInsight](https://azure.microsoft.com/services/hdinsight/) -klastrów Hadoop w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e365c-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="e365c-195">Usługa HDInsight zapewnia różne technologie zarządzania i analizy danych big data, i można go używać do przetwarzania danych, który został wyeksportowany z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e365c-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="e365c-196">Pytania i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e365c-196">Q & A</span></span>
* <span data-ttu-id="e365c-197">*Ale wszystkie wybrane jednorazowe pobierania wykresu.*</span><span class="sxs-lookup"><span data-stu-id="e365c-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="e365c-198">Tak, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="e365c-198">Yes, you can do that.</span></span> <span data-ttu-id="e365c-199">W górnej części bloku, kliknij **eksportowanie danych**.</span><span class="sxs-lookup"><span data-stu-id="e365c-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="e365c-200">*Skonfigurować eksportu, ale nie ma żadnych danych w magazynie my.*</span><span class="sxs-lookup"><span data-stu-id="e365c-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="e365c-201">Usługi Application Insights dotarła wszystkie dane telemetryczne z aplikacji, ponieważ ustawić eksport?</span><span class="sxs-lookup"><span data-stu-id="e365c-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="e365c-202">Otrzymasz nowych danych.</span><span class="sxs-lookup"><span data-stu-id="e365c-202">You'll only receive new data.</span></span>
* <span data-ttu-id="e365c-203">*Nastąpiła próba ustawienia eksportu, ale nastąpiła odmowa dostępu*</span><span class="sxs-lookup"><span data-stu-id="e365c-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="e365c-204">Jeśli konto jest własnością organizacji, musisz być członkiem grupy Właściciele i współautorzy.</span><span class="sxs-lookup"><span data-stu-id="e365c-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="e365c-205">*Można wyeksportować wprost do sklep lokalnej?*</span><span class="sxs-lookup"><span data-stu-id="e365c-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="e365c-206">Nie, Niestety.</span><span class="sxs-lookup"><span data-stu-id="e365c-206">No, sorry.</span></span> <span data-ttu-id="e365c-207">Nasze mechanizm eksportu jest obecnie obsługiwane tylko z usługą Azure storage w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="e365c-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="e365c-208">*Czy istnieje limitów ilości danych, które należy umieścić w sklepu?*</span><span class="sxs-lookup"><span data-stu-id="e365c-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="e365c-209">Nie.</span><span class="sxs-lookup"><span data-stu-id="e365c-209">No.</span></span> <span data-ttu-id="e365c-210">Firma Microsoft będzie przechowywać przekazywanie danych do momentu usunięcia eksportu.</span><span class="sxs-lookup"><span data-stu-id="e365c-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="e365c-211">Jeśli mamy trafień zewnętrzne limity dla magazynu obiektów blob, ale jest to bardzo dużych zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="e365c-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="e365c-212">Jest na kontrolowanie ile miejsca do magazynowania można użyć.</span><span class="sxs-lookup"><span data-stu-id="e365c-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="e365c-213">*Jak wiele obiektów blob zobacz w magazynie*</span><span class="sxs-lookup"><span data-stu-id="e365c-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="e365c-214">Dla każdego typu danych wybranych do wyeksportowania nowego obiektu blob jest tworzony co minutę (jeśli są dostępne dane).</span><span class="sxs-lookup"><span data-stu-id="e365c-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="e365c-215">Ponadto w przypadku aplikacji o dużym ruchu, jednostki dodatkowe partycji są przydzielone.</span><span class="sxs-lookup"><span data-stu-id="e365c-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="e365c-216">W takim przypadku każdej jednostki tworzy obiektu blob, co minutę.</span><span class="sxs-lookup"><span data-stu-id="e365c-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="e365c-217">*I ponownie wygenerować klucz do mojego magazynu lub zmienić nazwę kontenera, a teraz eksportu nie działa.*</span><span class="sxs-lookup"><span data-stu-id="e365c-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="e365c-218">Edytuj Eksport i otwarcie bloku docelowego eksportu.</span><span class="sxs-lookup"><span data-stu-id="e365c-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="e365c-219">Pozostaw tego samego magazynu co poprzednio zaznaczone, a następnie kliknij przycisk OK, aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="e365c-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="e365c-220">Eksport zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="e365c-220">Export will restart.</span></span> <span data-ttu-id="e365c-221">Zmiany były w ciągu ostatnich kilku dni, nie spowodować utratę danych.</span><span class="sxs-lookup"><span data-stu-id="e365c-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="e365c-222">*Czy można wstrzymać eksportu?*</span><span class="sxs-lookup"><span data-stu-id="e365c-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="e365c-223">Tak.</span><span class="sxs-lookup"><span data-stu-id="e365c-223">Yes.</span></span> <span data-ttu-id="e365c-224">Kliknij przycisk Wyłącz.</span><span class="sxs-lookup"><span data-stu-id="e365c-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="e365c-225">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="e365c-225">Code samples</span></span>

* [<span data-ttu-id="e365c-226">Przykładowe analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e365c-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="e365c-227">[Eksportowanie do bazy danych SQL przy użyciu usługi analiza strumienia][exportasa]</span><span class="sxs-lookup"><span data-stu-id="e365c-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="e365c-228">Szczegółowe dane modelu odwołania dla typów właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="e365c-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
