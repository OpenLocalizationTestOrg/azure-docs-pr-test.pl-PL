---
title: "aaaImport Twojego tooAnalytics danych w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Importowanie danych statycznych toojoin o telemetrii aplikacji lub zaimportować tooquery strumień danych, z Analytics."
services: application-insights
keywords: "Otwórz schematu, importowania danych"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="576b6-104">Importowanie danych do analityka</span><span class="sxs-lookup"><span data-stu-id="576b6-104">Import data into Analytics</span></span>

<span data-ttu-id="576b6-105">Importowanie danych tabelarycznych w [Analytics](app-insights-analytics.md), albo toojoin za pomocą [usługi Application Insights](app-insights-overview.md) dane telemetryczne z aplikacji, lub tak, aby można analizować je jako osobne strumienia.</span><span class="sxs-lookup"><span data-stu-id="576b6-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="576b6-106">Analytics to zaawansowane zapytania języka tooanalyzing dobrze nadaje się oznaczony znacznikiem czasowym dużych strumieni danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="576b6-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="576b6-107">Możesz zaimportować dane analizy przy użyciu własnego schematu.</span><span class="sxs-lookup"><span data-stu-id="576b6-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="576b6-108">Nie ma toouse hello standardowe usługi Application Insights schematów, takich jak żądania lub śledzenia.</span><span class="sxs-lookup"><span data-stu-id="576b6-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="576b6-109">Możesz zaimportować JSON lub widoku źródła danych (wartości rozdzielonych ogranicznikami - przecinek, średnik lub kartę) plików.</span><span class="sxs-lookup"><span data-stu-id="576b6-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="576b6-110">Istnieją trzy sytuacje, w którym importowanie tooAnalytics jest przydatne:</span><span class="sxs-lookup"><span data-stu-id="576b6-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="576b6-111">**Dołącz z danych telemetrycznych aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="576b6-111">**Join with app telemetry.**</span></span> <span data-ttu-id="576b6-112">Na przykład można zaimportować tabelę, która mapuje adresy URL z tytułów do odczytu strony toomore z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="576b6-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="576b6-113">W module analiz można utworzyć raport wykresu pulpitu nawigacyjnego, który zawiera hello dziesięć najpopularniejszych stron w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="576b6-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="576b6-114">Teraz go można wyświetlić hello tytuły stron zamiast hello adresów URL.</span><span class="sxs-lookup"><span data-stu-id="576b6-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="576b6-115">**Korelowanie dane telemetryczne aplikacji** z innych źródeł, takie jak ruch w sieci, dane serwera lub CDN pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="576b6-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="576b6-116">**Zastosuj Analytics tooa odrębne strumienia.**</span><span class="sxs-lookup"><span data-stu-id="576b6-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="576b6-117">Application Insights Analytics jest zaawansowane narzędzia, która współdziała również z rozrzedzony, strumienie oznaczony znacznikiem czasowym — znacznie lepszą niż SQL w wielu przypadkach.</span><span class="sxs-lookup"><span data-stu-id="576b6-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="576b6-118">Jeśli masz takich strumienia z z innego źródła, można analizować je z Analytics.</span><span class="sxs-lookup"><span data-stu-id="576b6-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="576b6-119">Wysyłanie danych tooyour źródło danych jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="576b6-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="576b6-120">(Jeden raz) Zdefiniuj schematu hello danych w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="576b6-121">(Okresowo) Przekaż tooAzure magazynu danych, a przesadzamy toonotify interfejsu API REST hello które czeka na wprowadzanie nowych danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="576b6-122">W ciągu kilku minut hello dane są dostępne dla kwerendy w module analiz.</span><span class="sxs-lookup"><span data-stu-id="576b6-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="576b6-123">Hello częstotliwość przekazywania hello jest zdefiniowane przez użytkownika i tempa chcesz Twojej toobe danych jest niedostępne dla zapytań.</span><span class="sxs-lookup"><span data-stu-id="576b6-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="576b6-124">Jest bardziej wydajne danych tooupload w większych fragmentów, ale nie większą niż 1GB.</span><span class="sxs-lookup"><span data-stu-id="576b6-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="576b6-125">*Uzyskano wiele tooanalyze źródeł danych?*</span><span class="sxs-lookup"><span data-stu-id="576b6-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="576b6-126">*Należy rozważyć użycie* logstash *tooship dane do usługi Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="576b6-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="576b6-127">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="576b6-127">Before you start</span></span>

<span data-ttu-id="576b6-128">Potrzebne elementy:</span><span class="sxs-lookup"><span data-stu-id="576b6-128">You need:</span></span>

1. <span data-ttu-id="576b6-129">Zasób usługi Application Insights w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="576b6-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="576b6-130">Jeśli chcesz tooanalyze danych niezależnie od innych telemetrii [utworzyć nowy zasób usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="576b6-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="576b6-131">Sprzęganie lub porównywanie danych za pomocą dane telemetryczne z aplikacji, która jest już skonfigurowane przy użyciu usługi Application Insights, można użyć hello zasobów dla danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="576b6-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="576b6-132">Współautor lub właściciela zasobu toothat dostępu.</span><span class="sxs-lookup"><span data-stu-id="576b6-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="576b6-133">Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="576b6-133">Azure storage.</span></span> <span data-ttu-id="576b6-134">Przekaż tooAzure magazynu, a Analytics pobiera dane z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="576b6-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="576b6-135">Zaleca się tworzenie konta magazynu dedykowane dla obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="576b6-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="576b6-136">Jeżeli obiektów blob są współużytkowane z innymi procesami, trwa dłużej naszych tooread procesy obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="576b6-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="576b6-137">Definiowania schematu</span><span class="sxs-lookup"><span data-stu-id="576b6-137">Define your schema</span></span>

<span data-ttu-id="576b6-138">Przed importowaniem danych, należy zdefiniować *źródła danych* określającej schematu hello danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="576b6-139">Może zawierać maksymalnie too50 źródeł danych w pojedynczy zasób usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="576b6-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="576b6-140">Uruchom Kreatora źródła danych hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-140">Start hello data source wizard.</span></span> <span data-ttu-id="576b6-141">Użyj przycisku "Dodaj nowe źródło danych".</span><span class="sxs-lookup"><span data-stu-id="576b6-141">Use "Add new data source" button.</span></span> <span data-ttu-id="576b6-142">Alternatywnie — kliknij przycisk Ustawienia w prawym górnym rogu i wybierz w menu rozwijanym "Źródła danych".</span><span class="sxs-lookup"><span data-stu-id="576b6-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Dodaj nowe źródło danych](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="576b6-144">Podaj nazwę dla nowego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="576b6-145">Definiowanie formatu hello plików, które możesz przekazać.</span><span class="sxs-lookup"><span data-stu-id="576b6-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="576b6-146">Można ręcznie zdefiniować hello format lub Przekaż plik przykładowy.</span><span class="sxs-lookup"><span data-stu-id="576b6-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="576b6-147">Pierwszy wiersz hello próbki hello hello danych jest w formacie CSV, może być nagłówki kolumn.</span><span class="sxs-lookup"><span data-stu-id="576b6-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="576b6-148">Można zmienić nazwy pól hello w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="576b6-149">przykład Witaj powinna zawierać co najmniej 10 wierszy lub rekordów danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="576b6-150">Nazwy kolumn lub pole ma alfanumerycznych nazw (bez spacji i znaków interpunkcyjnych).</span><span class="sxs-lookup"><span data-stu-id="576b6-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Przekaż plik przykładowy](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="576b6-152">Otrzymano schemat hello przeglądu hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="576b6-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="576b6-153">Jeśli typy hello z próbki go wywnioskować, może być konieczne tooadjust typy hello wywnioskować hello kolumn.</span><span class="sxs-lookup"><span data-stu-id="576b6-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Przejrzyj hello wywnioskować schematu](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="576b6-155">(opcjonalnie) Przekaż definicji schematu.</span><span class="sxs-lookup"><span data-stu-id="576b6-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="576b6-156">Zobacz hello format poniżej.</span><span class="sxs-lookup"><span data-stu-id="576b6-156">See hello format below.</span></span>

 * <span data-ttu-id="576b6-157">Wybierz sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="576b6-157">Select a Timestamp.</span></span> <span data-ttu-id="576b6-158">Wszystkie dane w module analiz musi mieć pola sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="576b6-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="576b6-159">Musi mieć typ `datetime`, ale nie ma toobe o nazwie "timestamp".</span><span class="sxs-lookup"><span data-stu-id="576b6-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="576b6-160">Jeśli dane mają kolumny zawierającej daty i godziny w formacie ISO, wybierz tę opcję, jako hello kolumny znaczników czasu.</span><span class="sxs-lookup"><span data-stu-id="576b6-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="576b6-161">W przeciwnym razie wybierz pozycję "jako dane dostarczone", a proces importowania hello doda pola sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="576b6-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="576b6-162">Utwórz źródło danych hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="576b6-163">Format pliku definicji schematu</span><span class="sxs-lookup"><span data-stu-id="576b6-163">Schema definition file format</span></span>

<span data-ttu-id="576b6-164">Zamiast edycji hello schematu w interfejsie użytkownika, można załadować definicji schematu hello z pliku.</span><span class="sxs-lookup"><span data-stu-id="576b6-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="576b6-165">format definicji schematu Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="576b6-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="576b6-166">Format rozdzielanego</span><span class="sxs-lookup"><span data-stu-id="576b6-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="576b6-167">JSON format</span><span class="sxs-lookup"><span data-stu-id="576b6-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="576b6-168">Każda kolumna jest identyfikowany przez hello lokalizację, nazwy i typu.</span><span class="sxs-lookup"><span data-stu-id="576b6-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="576b6-169">Lokalizacja — pliku rozdzielanego go sformatować jest pozycja hello wartości hello zamapowane.</span><span class="sxs-lookup"><span data-stu-id="576b6-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="576b6-170">JSON format jest jpath hello hello mapowane klucza.</span><span class="sxs-lookup"><span data-stu-id="576b6-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="576b6-171">Nazwa — Witaj wyświetlana nazwa kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="576b6-172">Typ — typ danych hello tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="576b6-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="576b6-173">W przypadku użyto przykładowych danych i rozdzielana format pliku, definicji schematu hello należy mapować wszystkie kolumny i dodać nowe kolumny na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="576b6-174">JSON umożliwia mapowania częściowe hello danych, w związku z tym hello definicji schematu formatu JSON nie ma toomap każdego klucza, który znajduje się w przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="576b6-175">Można również mapować kolumn, które nie są częścią hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="576b6-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="576b6-176">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="576b6-176">Import data</span></span>

<span data-ttu-id="576b6-177">tooimport danych, przekaż go tooAzure magazynu lub Utwórz klucz dostępu dla niego, a następnie dokonaj wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="576b6-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Dodaj nowe źródło danych](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="576b6-179">Wykonaj powitania po procesie ręcznie lub skonfigurować toodo systemu go w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="576b6-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="576b6-180">Należy toofollow te kroki dla każdego bloku danych ma tooimport.</span><span class="sxs-lookup"><span data-stu-id="576b6-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="576b6-181">Przekazywanie danych hello zbyt[magazynu obiektów blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="576b6-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="576b6-182">Obiekty BLOB może być dowolnej wielkości zapasowej too1GB jako nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="576b6-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="576b6-183">Duże obiekty BLOB setek MB idealnie nadają się z punktu widzenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="576b6-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="576b6-184">Można skompresować je z Gzip tooimprove przekazywania czas i czas oczekiwania na powitania toobe danych jest dostępne dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="576b6-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="576b6-185">Użyj hello `.gz` rozszerzenie nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="576b6-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="576b6-186">W tym celu wywołania tooavoid z różnych usług spowolnienia jest najlepszym toouse oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="576b6-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="576b6-187">Podczas wysyłania danych w wysokiej częstotliwości, co kilka sekund, zalecane jest toouse więcej niż jedno konto magazynu, ze względu na wydajność.</span><span class="sxs-lookup"><span data-stu-id="576b6-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="576b6-188">[Utwórz klucz sygnatura dostępu współdzielonego dla obiekt blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="576b6-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="576b6-189">klucz Hello powinny mieć okres ważności jeden dzień i zapewniają dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="576b6-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="576b6-190">Należy toonotify wywołania REST usługi Application Insights, która oczekuje na dane.</span><span class="sxs-lookup"><span data-stu-id="576b6-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="576b6-191">Punkt końcowy:`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="576b6-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="576b6-192">Metoda HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="576b6-192">HTTP method: POST</span></span>
 * <span data-ttu-id="576b6-193">Ładunek:</span><span class="sxs-lookup"><span data-stu-id="576b6-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="576b6-194">symbole zastępcze Hello to:</span><span class="sxs-lookup"><span data-stu-id="576b6-194">hello placeholders are:</span></span>

* <span data-ttu-id="576b6-195">`Blob URI with Shared Access Key`: Otrzymujesz to z procedury hello do tworzenia kluczy.</span><span class="sxs-lookup"><span data-stu-id="576b6-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="576b6-196">Jest toohello określonego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="576b6-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="576b6-197">`Schema ID`: hello generowane dla określonych schemat Identyfikatora schematu.</span><span class="sxs-lookup"><span data-stu-id="576b6-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="576b6-198">Witaj danych w tym obiekcie blob powinna być zgodna toohello schematu.</span><span class="sxs-lookup"><span data-stu-id="576b6-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="576b6-199">`DateTime`: hello czas na powitania, które zostało przesłane żądanie, UTC.</span><span class="sxs-lookup"><span data-stu-id="576b6-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="576b6-200">Możemy zaakceptować te formaty: ISO8601 (takich jak "2016-01-01-13:45:01"); Rfc822 ("śro, 14 gru 16 14:57:01 + 0000"); RFC850 ("Środa, 16-14-gru UTC 14:57:00"); RFC1123 ("śro 14 gru 2016 14:57:00 + 0000").</span><span class="sxs-lookup"><span data-stu-id="576b6-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="576b6-201">`Instrumentation key`zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="576b6-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="576b6-202">Witaj dane są dostępne w module analiz po kilku minutach.</span><span class="sxs-lookup"><span data-stu-id="576b6-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="576b6-203">Błąd odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="576b6-203">Error responses</span></span>

* <span data-ttu-id="576b6-204">**Nieprawidłowe żądanie 400**: wskazuje, że hello ładunku żądania jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="576b6-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="576b6-205">Sprawdzanie:</span><span class="sxs-lookup"><span data-stu-id="576b6-205">Check:</span></span>
 * <span data-ttu-id="576b6-206">Instrumentacja poprawny klucz.</span><span class="sxs-lookup"><span data-stu-id="576b6-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="576b6-207">Wartość czas ważności.</span><span class="sxs-lookup"><span data-stu-id="576b6-207">Valid time value.</span></span> <span data-ttu-id="576b6-208">Należy go hello czasu w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="576b6-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="576b6-209">JSON zdarzenia hello zgodne toohello schematu.</span><span class="sxs-lookup"><span data-stu-id="576b6-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="576b6-210">**403 Zabroniony**: hello obiektu blob zostało wysłane nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="576b6-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="576b6-211">Upewnij się, że hello udostępniony klucz dostępu jest prawidłowa i nie wygasł.</span><span class="sxs-lookup"><span data-stu-id="576b6-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="576b6-212">**Nie można odnaleźć 404**:</span><span class="sxs-lookup"><span data-stu-id="576b6-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="576b6-213">Witaj obiektu blob nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="576b6-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="576b6-214">Hello sourceId jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="576b6-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="576b6-215">Bardziej szczegółowe informacje są dostępne w komunikacie o błędzie odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="576b6-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="576b6-216">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="576b6-216">Sample code</span></span>

<span data-ttu-id="576b6-217">Ten kod zawiera hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="576b6-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="576b6-218">Klasy</span><span class="sxs-lookup"><span data-stu-id="576b6-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="576b6-219">Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="576b6-219">Ingest data</span></span>

<span data-ttu-id="576b6-220">Użyj tego kodu dla każdego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="576b6-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="576b6-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="576b6-221">Next steps</span></span>

* [<span data-ttu-id="576b6-222">Samouczek hello język zapytań usługi Analiza dzienników</span><span class="sxs-lookup"><span data-stu-id="576b6-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="576b6-223">Użyj *Logstash* toosend tooApplication danych usługi Insights</span><span class="sxs-lookup"><span data-stu-id="576b6-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
