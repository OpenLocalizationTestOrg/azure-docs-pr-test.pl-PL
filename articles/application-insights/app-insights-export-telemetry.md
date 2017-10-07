---
title: "Eksport aaaContinuous dane telemetryczne z usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Eksportuj toostorage danych diagnostycznych i użycia w systemie Microsoft Azure i pobierz go z tego miejsca."
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="af09c-103">Eksportuj dane telemetryczne z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="af09c-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="af09c-104">Chcesz tookeep telemetrii przez czas dłuższy niż okres przechowywania standardowe hello?</span><span class="sxs-lookup"><span data-stu-id="af09c-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="af09c-105">Lub przetwarzać dane w jakiś sposób specjalne?</span><span class="sxs-lookup"><span data-stu-id="af09c-105">Or process it in some specialized way?</span></span> <span data-ttu-id="af09c-106">Eksport ciągły jest idealna to.</span><span class="sxs-lookup"><span data-stu-id="af09c-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="af09c-107">Hello zdarzenia, które są widoczne w portalu usługi Application Insights hello może być eksportowany toostorage platformie Microsoft Azure w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="af09c-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="af09c-108">Z tego miejsca można pobrać danych i zapisu, niezależnie od kod należy tooprocess go.</span><span class="sxs-lookup"><span data-stu-id="af09c-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="af09c-109">Przy użyciu eksportu ciągłego może pociągnąć za sobą dodatkowe opłaty.</span><span class="sxs-lookup"><span data-stu-id="af09c-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="af09c-110">Sprawdź Twojej [model cenowy](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="af09c-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="af09c-111">Przed skonfigurowaniem Eksport ciągły istnieje kilka rozwiązań alternatywnych można tooconsider:</span><span class="sxs-lookup"><span data-stu-id="af09c-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="af09c-112">przycisk Eksportuj Hello u góry bloku metryki lub wyszukiwania hello umożliwia transfer arkusz kalkulacyjny programu Excel tooan tabel i wykresów.</span><span class="sxs-lookup"><span data-stu-id="af09c-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="af09c-113">[Analiza](app-insights-analytics.md) zapewnia język kwerendy zaawansowanych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="af09c-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="af09c-114">Można także wyeksportować wyniki.</span><span class="sxs-lookup"><span data-stu-id="af09c-114">It can also export results.</span></span>
* <span data-ttu-id="af09c-115">Jeśli szukasz zbyt[eksplorować dane w usłudze Power BI](app-insights-export-power-bi.md), możesz to zrobić bez użycia eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="af09c-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="af09c-116">Witaj [dostępu do danych interfejsu API REST](https://dev.applicationinsights.io/) pozwala uzyskiwać dostęp do telemetrii programowo.</span><span class="sxs-lookup"><span data-stu-id="af09c-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="af09c-117">Po eksportu ciągłego kopiuje Twojej toostorage danych (jeżeli pozostawał dla tak długo, jak chcesz), jest on nadal dostępny w usłudze Application Insights dla hello zwykle [okres przechowywania](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="af09c-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="af09c-118"><a name="setup"></a>Utwórz eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="af09c-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="af09c-119">Hello zasobu usługi Application Insights dla aplikacji, otwórz eksportu ciągłego i wybierz polecenie **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="af09c-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Przewiń w dół i kliknij przycisk eksportu ciągłego](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="af09c-121">Wybierz typy danych telemetrycznych hello ma tooexport.</span><span class="sxs-lookup"><span data-stu-id="af09c-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="af09c-122">Utwórz lub wybierz [konto magazynu Azure](../storage/common/storage-introduction.md) miejscu toostore hello danych.</span><span class="sxs-lookup"><span data-stu-id="af09c-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="af09c-123">Domyślnie program hello lokalizacji magazynu zostanie ustawiona toohello tego samego regionu geograficznego co zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="af09c-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="af09c-124">Jeśli jest przechowywany w innym regionie, może spowodować naliczenie opłat transferu.</span><span class="sxs-lookup"><span data-stu-id="af09c-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Kliknij przycisk Dodaj, wyeksportować miejsce docelowe konto magazynu, a następnie utwórz nowy magazyn lub wybierz istniejący magazyn](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="af09c-126">Utwórz lub Wybierz kontener magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="af09c-126">Create or select a container in hello storage:</span></span>

    ![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="af09c-128">Po utworzeniu eksportu uruchamia przejście.</span><span class="sxs-lookup"><span data-stu-id="af09c-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="af09c-129">Tylko Pobierz dane przychodzący po utworzeniu hello eksportu.</span><span class="sxs-lookup"><span data-stu-id="af09c-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="af09c-130">Może to być opóźnienie około godziny przed wyświetleniem danych w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="af09c-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="af09c-131">Eksport ciągły tooedit</span><span class="sxs-lookup"><span data-stu-id="af09c-131">tooedit continuous export</span></span>

<span data-ttu-id="af09c-132">Jeśli chcesz typów zdarzeń toochange hello później, po prostu edytować Eksport hello:</span><span class="sxs-lookup"><span data-stu-id="af09c-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="af09c-134">Eksport ciągły toostop</span><span class="sxs-lookup"><span data-stu-id="af09c-134">toostop continuous export</span></span>

<span data-ttu-id="af09c-135">Wyłącz toostop hello eksportu, kliknij przycisk.</span><span class="sxs-lookup"><span data-stu-id="af09c-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="af09c-136">Po kliknięciu włączyć ponownie, hello eksportu zostanie uruchomiony ponownie z nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="af09c-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="af09c-137">Użytkownik nie będzie otrzymywał hello dane, które dotarły w portalu hello podczas eksportowania została wyłączona.</span><span class="sxs-lookup"><span data-stu-id="af09c-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="af09c-138">Eksport hello toostop stałe, usuń go.</span><span class="sxs-lookup"><span data-stu-id="af09c-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="af09c-139">Dzięki temu nie powoduje usunięcia danych z magazynu.</span><span class="sxs-lookup"><span data-stu-id="af09c-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="af09c-140">Nie można dodać lub zmienić eksportu?</span><span class="sxs-lookup"><span data-stu-id="af09c-140">Can't add or change an export?</span></span>
* <span data-ttu-id="af09c-141">eksporty tooadd lub zmiany, należy właściciela, współautora lub Application Insights współautora praw dostępu.</span><span class="sxs-lookup"><span data-stu-id="af09c-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="af09c-142">[Dowiedz się więcej o rolach][roles].</span><span class="sxs-lookup"><span data-stu-id="af09c-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="af09c-143"><a name="analyze"></a>Jakie zdarzenia uzyskać?</span><span class="sxs-lookup"><span data-stu-id="af09c-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="af09c-144">Witaj wyeksportowanych danych jest hello nieprzetworzone dane telemetryczne, otrzymywanych z aplikacji, ale dodamy danych lokalizacji, które firma Microsoft obliczenia z adresu IP powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="af09c-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="af09c-145">Dane, które zostały odrzucone przez [próbkowania](app-insights-sampling.md) nie jest uwzględniony w hello wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="af09c-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="af09c-146">Inne metryki obliczanej nie są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="af09c-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="af09c-147">Na przykład firma Microsoft nie Eksportuj średnie wykorzystanie procesora CPU, ale eksportowania telemetrii raw hello, z którego jest obliczana średnia hello.</span><span class="sxs-lookup"><span data-stu-id="af09c-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="af09c-148">Witaj danych obejmuje również hello wyniki dowolnego [testów sieci web dostępności](app-insights-monitor-web-app-availability.md) , które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="af09c-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="af09c-149">**Próbkowania.**</span><span class="sxs-lookup"><span data-stu-id="af09c-149">**Sampling.**</span></span> <span data-ttu-id="af09c-150">Jeśli aplikacja wyśle dużą ilość danych, funkcja próbkowania hello może działać i tylko część telemetrii hello wygenerowane wysyłać.</span><span class="sxs-lookup"><span data-stu-id="af09c-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="af09c-151">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="af09c-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="af09c-152"><a name="get"></a>Sprawdź hello danych</span><span class="sxs-lookup"><span data-stu-id="af09c-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="af09c-153">Możesz sprawdzić magazynu hello bezpośrednio w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="af09c-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="af09c-154">Kliknij przycisk **Przeglądaj**, wybierz konto magazynu, a następnie otwórz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="af09c-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="af09c-155">Otwórz tooinspect magazynu Azure w programie Visual Studio, **widoku**, **Eksplorator chmury**.</span><span class="sxs-lookup"><span data-stu-id="af09c-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="af09c-156">(Jeśli nie masz tego polecenia menu, należy tooinstall hello Azure SDK: Otwórz hello **nowy projekt** okna dialogowego, rozwiń Visual C# / w chmurze i wybierz polecenie **pobrać zestaw Microsoft Azure SDK dla platformy .NET**.)</span><span class="sxs-lookup"><span data-stu-id="af09c-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="af09c-157">Po otwarciu magazynie obiektów blob, zobaczysz kontener z zestawu plików obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="af09c-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="af09c-158">Witaj identyfikatora URI poszczególnych plików pochodząca z nazwę zasobu usługi Application Insights, jego klucza instrumentacji, telemetrii — typ, datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="af09c-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="af09c-159">(nazwa zasobu hello jest tylko małe litery, a klucza Instrumentacji hello pomija łączniki).</span><span class="sxs-lookup"><span data-stu-id="af09c-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Sprawdź hello magazynu obiektów blob za pomocą odpowiedniego narzędzia](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="af09c-161">Witaj Data i godzina są UTC i gdy telemetrii hello został złożony w magazynie hello — nie hello czasu został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="af09c-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="af09c-162">Dlatego podczas pisania kodu toodownload hello danych, jej przechodzić liniowo hello danych.</span><span class="sxs-lookup"><span data-stu-id="af09c-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="af09c-163">Poniżej przedstawiono formularz hello hello ścieżki:</span><span class="sxs-lookup"><span data-stu-id="af09c-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="af09c-164">gdzie</span><span class="sxs-lookup"><span data-stu-id="af09c-164">Where</span></span>

* <span data-ttu-id="af09c-165">`blobCreationTimeUtc`Godzina blob utworzenia w hello wewnętrznego jest przemieszczania magazynu</span><span class="sxs-lookup"><span data-stu-id="af09c-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="af09c-166">`blobDeliveryTimeUtc`gdy obiekt blob jest Magazyn docelowy eksportu skopiowanych toohello po raz hello</span><span class="sxs-lookup"><span data-stu-id="af09c-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="af09c-167"><a name="format"></a>Format danych</span><span class="sxs-lookup"><span data-stu-id="af09c-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="af09c-168">Każdy obiekt blob jest to plik tekstowy, który zawiera wiele "\n'-separated wierszy.</span><span class="sxs-lookup"><span data-stu-id="af09c-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="af09c-169">Zawiera ona dane telemetryczne hello przetwarzane w czasie około pół minuty.</span><span class="sxs-lookup"><span data-stu-id="af09c-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="af09c-170">Każdy wiersz reprezentuje punktu danych telemetrii, takich jak żądania lub strony widoku.</span><span class="sxs-lookup"><span data-stu-id="af09c-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="af09c-171">Każdy wiersz jest niesformatowany dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="af09c-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="af09c-172">Toosit i stare go, otwórz go w programie Visual Studio i wybierz pozycję Edytuj, zaawansowane, Format pliku:</span><span class="sxs-lookup"><span data-stu-id="af09c-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Dane telemetryczne hello widoku z narzędziem do odpowiedniego](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="af09c-174">Okresach czasu są w taktach, gdzie znaczniki 10 000 = 1 MS.</span><span class="sxs-lookup"><span data-stu-id="af09c-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="af09c-175">Na przykład te wartości wyświetlane przez czas 1 MS toosend żądania z przeglądarki hello, 3ms tooreceive i 1.8s tooprocess hello strony w przeglądarce hello:</span><span class="sxs-lookup"><span data-stu-id="af09c-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="af09c-176">Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="af09c-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="af09c-177">Przetwarzanie danych hello</span><span class="sxs-lookup"><span data-stu-id="af09c-177">Processing hello data</span></span>
<span data-ttu-id="af09c-178">Na małą skalę można zapisać niektórych toopull kodu od siebie danych, przeczytaj je do arkusza kalkulacyjnego i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="af09c-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="af09c-179">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="af09c-179">For example:</span></span>

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

<span data-ttu-id="af09c-180">Dla większych przykładowy kod, zobacz [przy użyciu roli procesu roboczego][exportasa].</span><span class="sxs-lookup"><span data-stu-id="af09c-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="af09c-181"><a name="delete"></a>Usuń stare dane</span><span class="sxs-lookup"><span data-stu-id="af09c-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="af09c-182">Należy pamiętać, że jest odpowiedzialny za zarządzanie pojemności pamięci masowej i usuwania starych danych hello, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="af09c-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="af09c-183">Jeśli musisz ponownie wygenerować klucz magazynu...</span><span class="sxs-lookup"><span data-stu-id="af09c-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="af09c-184">Jeśli zmienisz magazynu kluczy tooyour hello Eksport ciągły przestaną działać.</span><span class="sxs-lookup"><span data-stu-id="af09c-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="af09c-185">Zostanie wyświetlone powiadomienie na koncie Azure.</span><span class="sxs-lookup"><span data-stu-id="af09c-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="af09c-186">Otwarcie bloku eksportu ciągłego hello i edytowanie eksportu.</span><span class="sxs-lookup"><span data-stu-id="af09c-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="af09c-187">Edytuj hello docelowego eksportu, ale pozostaw hello wybrane tego samego magazynu.</span><span class="sxs-lookup"><span data-stu-id="af09c-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="af09c-188">Kliknij przycisk OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="af09c-188">Click OK tooconfirm.</span></span>

![Edytuj hello ciągłego wyeksportować, Otwórz i zamknąć ją docelowego eksportu.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="af09c-190">Witaj Eksport ciągły zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="af09c-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="af09c-191">Przykłady eksportu</span><span class="sxs-lookup"><span data-stu-id="af09c-191">Export samples</span></span>

* <span data-ttu-id="af09c-192">[Eksportuj tooSQL przy użyciu usługi analiza strumienia][exportasa]</span><span class="sxs-lookup"><span data-stu-id="af09c-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="af09c-193">Stream Analytics próbki 2</span><span class="sxs-lookup"><span data-stu-id="af09c-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="af09c-194">Na większą skalę, należy wziąć pod uwagę [HDInsight](https://azure.microsoft.com/services/hdinsight/) -klastrów Hadoop w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="af09c-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="af09c-195">Usługa HDInsight zapewnia różne technologie zarządzania i analizy danych big data i może używać tooprocess danych, który został wyeksportowany z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="af09c-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="af09c-196">Pytania i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="af09c-196">Q & A</span></span>
* <span data-ttu-id="af09c-197">*Ale wszystkie wybrane jednorazowe pobierania wykresu.*</span><span class="sxs-lookup"><span data-stu-id="af09c-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="af09c-198">Tak, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="af09c-198">Yes, you can do that.</span></span> <span data-ttu-id="af09c-199">U góry hello hello bloku, kliknij przycisk **eksportowanie danych**.</span><span class="sxs-lookup"><span data-stu-id="af09c-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="af09c-200">*Skonfigurować eksportu, ale nie ma żadnych danych w magazynie my.*</span><span class="sxs-lookup"><span data-stu-id="af09c-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="af09c-201">Application Insights dotarła wszystkie dane telemetryczne z aplikacji ponieważ konfigurowanie hello eksportu?</span><span class="sxs-lookup"><span data-stu-id="af09c-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="af09c-202">Otrzymasz nowych danych.</span><span class="sxs-lookup"><span data-stu-id="af09c-202">You'll only receive new data.</span></span>
* <span data-ttu-id="af09c-203">*Nastąpiła tooset się eksportu, ale nastąpiła odmowa dostępu*</span><span class="sxs-lookup"><span data-stu-id="af09c-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="af09c-204">Jeśli konto hello jest własnością organizacji, należy toobe hello właściciele i współautorzy grup.</span><span class="sxs-lookup"><span data-stu-id="af09c-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="af09c-205">*Można wyeksportować proste toomy własnych z lokalnym magazynem?*</span><span class="sxs-lookup"><span data-stu-id="af09c-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="af09c-206">Nie, Niestety.</span><span class="sxs-lookup"><span data-stu-id="af09c-206">No, sorry.</span></span> <span data-ttu-id="af09c-207">Nasze mechanizm eksportu jest obecnie obsługiwane tylko z usługą Azure storage w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="af09c-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="af09c-208">*Czy istnieje limit żadnych toohello ilość danych, które należy umieścić w sklep?*</span><span class="sxs-lookup"><span data-stu-id="af09c-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="af09c-209">Nie.</span><span class="sxs-lookup"><span data-stu-id="af09c-209">No.</span></span> <span data-ttu-id="af09c-210">Firma Microsoft będzie przechowywać przekazywanie danych do momentu usunięcia hello eksportu.</span><span class="sxs-lookup"><span data-stu-id="af09c-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="af09c-211">Jeśli mamy trafień hello zewnętrzne limity dla magazynu obiektów blob, ale jest to bardzo dużych zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="af09c-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="af09c-212">Należy się tooyou toocontrol ile miejsca do magazynowania można użyć.</span><span class="sxs-lookup"><span data-stu-id="af09c-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="af09c-213">*Jak wiele obiektów blob zobacz w magazynie hello*</span><span class="sxs-lookup"><span data-stu-id="af09c-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="af09c-214">Dla typu danych co wybrany tooexport, nowy obiekt blob jest tworzony co minutę (jeśli są dostępne dane).</span><span class="sxs-lookup"><span data-stu-id="af09c-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="af09c-215">Ponadto w przypadku aplikacji o dużym ruchu, jednostki dodatkowe partycji są przydzielone.</span><span class="sxs-lookup"><span data-stu-id="af09c-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="af09c-216">W takim przypadku każdej jednostki tworzy obiektu blob, co minutę.</span><span class="sxs-lookup"><span data-stu-id="af09c-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="af09c-217">*I ponownie wygenerować hello toomy klucza magazynu lub zmienić nazwę hello hello kontenera i hello eksportu nie działają.*</span><span class="sxs-lookup"><span data-stu-id="af09c-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="af09c-218">Edytuj Eksport hello i otwarcie bloku docelowego eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="af09c-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="af09c-219">Pozostaw hello tego samego magazynu co poprzednio zaznaczone, a następnie kliknij przycisk OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="af09c-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="af09c-220">Eksport zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="af09c-220">Export will restart.</span></span> <span data-ttu-id="af09c-221">Zmiana hello była w hello ostatnie kilka dni, nie spowodować utratę danych.</span><span class="sxs-lookup"><span data-stu-id="af09c-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="af09c-222">*Czy można wstrzymać hello eksportu?*</span><span class="sxs-lookup"><span data-stu-id="af09c-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="af09c-223">Tak.</span><span class="sxs-lookup"><span data-stu-id="af09c-223">Yes.</span></span> <span data-ttu-id="af09c-224">Kliknij przycisk Wyłącz.</span><span class="sxs-lookup"><span data-stu-id="af09c-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="af09c-225">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="af09c-225">Code samples</span></span>

* [<span data-ttu-id="af09c-226">Przykładowe analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="af09c-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="af09c-227">[Eksportuj tooSQL przy użyciu usługi analiza strumienia][exportasa]</span><span class="sxs-lookup"><span data-stu-id="af09c-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="af09c-228">Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="af09c-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
