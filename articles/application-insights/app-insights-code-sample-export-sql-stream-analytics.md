---
title: "Eksportowanie tooSQL z usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Stale wyeksportować za pomocą usługi Stream Analytics tooSQL dane usługi Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="0ca11-103">Wskazówki: Eksportowanie tooSQL z usługi Application Insights przy użyciu usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="0ca11-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="0ca11-104">W tym artykule przedstawiono sposób toomove dane telemetryczne z [Azure Application Insights] [ start] do bazy danych Azure SQL za pomocą [eksportu ciągłego] [ export] i [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="0ca11-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="0ca11-105">Eksport ciągły przenosi dane telemetryczne do usługi Azure Storage w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0ca11-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="0ca11-106">Firma Microsoft będzie analizować hello obiektów JSON przy użyciu usługi Azure Stream Analytics i utworzyć wiersze w tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0ca11-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="0ca11-107">(Eksportu ciągłego jest ogólnie rzecz biorąc, toodo sposób hello analizy hello dane telemetryczne aplikacji wysyłania tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="0ca11-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="0ca11-108">Można dostosować ten kod przykładowy toodo innymi z hello wyeksportowane dane telemetryczne, takich jak agregacji danych.)</span><span class="sxs-lookup"><span data-stu-id="0ca11-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="0ca11-109">Zaczniemy założeń hello już aplikacji hello ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0ca11-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="0ca11-110">W tym przykładzie użyjemy hello strony widoku danych, ale hello tego samego wzorca można z łatwością rozszerzyć tooother typów danych, takich jak niestandardowe zdarzenia i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="0ca11-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="0ca11-111">Dodawanie usługi Application Insights tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ca11-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="0ca11-112">Rozpoczęto tooget:</span><span class="sxs-lookup"><span data-stu-id="0ca11-112">tooget started:</span></span>

1. <span data-ttu-id="0ca11-113">[Skonfiguruj usługę Application Insights dla stron sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="0ca11-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="0ca11-114">(W tym przykładzie firma Microsoft będzie skupić się na przetwarzanie danych widoku strony z powitania klienta przeglądarki, ale można również skonfigurować usługi Application Insights po stronie serwera na powitania z Twojej [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md) żądania aplikacji i procesów zależności i inne dane telemetryczne serwera.)</span><span class="sxs-lookup"><span data-stu-id="0ca11-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="0ca11-115">Publikowanie aplikacji i obserwować dane telemetryczne w zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ca11-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="0ca11-116">Tworzenie magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0ca11-116">Create storage in Azure</span></span>
<span data-ttu-id="0ca11-117">Eksport ciągły zawsze generuje konto magazynu Azure tooan danych, więc najpierw należy toocreate hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="0ca11-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="0ca11-118">Utwórz konto magazynu w ramach subskrypcji w hello [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="0ca11-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![W portalu Azure wybierz nowy, danych, magazynu.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="0ca11-122">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="0ca11-122">Create a container</span></span>
   
    ![W hello nowego magazynu wybierz kontenery, kliknij Kafelek kontenery hello, a następnie dodaj](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="0ca11-124">Skopiuj klucz dostępu do magazynu hello</span><span class="sxs-lookup"><span data-stu-id="0ca11-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="0ca11-125">Będzie on potrzebny wkrótce tooset się usługa analiza strumienia wejściowego toohello hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![W magazynie hello Otwórz ustawienia kluczy i kopiować hello podstawowy klucz dostępu](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="0ca11-127">Uruchom magazynu tooAzure eksportu ciągłego</span><span class="sxs-lookup"><span data-stu-id="0ca11-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="0ca11-128">W hello portalu Azure Przejdź zasobu usługi Application Insights toohello utworzone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ca11-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Kliknij przycisk Przeglądaj, usługi Application Insights aplikacji](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="0ca11-130">Utwórz eksport ciągły.</span><span class="sxs-lookup"><span data-stu-id="0ca11-130">Create a continuous export.</span></span>
   
    ![Wybierz ustawienia, Eksport ciągły](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="0ca11-132">Wybierz utworzone wcześniej konto magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="0ca11-132">Select hello storage account you created earlier:</span></span>

    ![Ustaw miejsce docelowe hello eksportu](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="0ca11-134">Ustaw hello typy zdarzeń, które mają toosee:</span><span class="sxs-lookup"><span data-stu-id="0ca11-134">Set hello event types you want toosee:</span></span>

    ![Wybierz typy zdarzeń](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="0ca11-136">Let niektóre dane gromadzone.</span><span class="sxs-lookup"><span data-stu-id="0ca11-136">Let some data accumulate.</span></span> <span data-ttu-id="0ca11-137">Zaczekaj i innym użytkownikom za pomocą aplikacji przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="0ca11-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="0ca11-138">Dane telemetryczne wejdzie i zobaczysz statystyczne wykresów w [Eksploratora metryk](app-insights-metrics-explorer.md) i zdarzeń z [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="0ca11-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="0ca11-139">I ponadto hello danych będzie eksportować tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="0ca11-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="0ca11-140">Sprawdź hello wyeksportowane dane, albo w portalu hello — wybierz **Przeglądaj**, wybierz konto magazynu, a następnie **kontenery** — lub w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ca11-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="0ca11-141">W programie Visual Studio, wybierz **wyświetlić / w chmurze Explorer**i otwórz Azure / magazynu.</span><span class="sxs-lookup"><span data-stu-id="0ca11-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="0ca11-142">(Jeśli nie mają tej opcji menu, należy tooinstall hello Azure SDK: Otwórz okno dialogowe Nowy projekt hello a Visual C# / w chmurze / Get Microsoft Azure SDK dla platformy .NET.)</span><span class="sxs-lookup"><span data-stu-id="0ca11-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![W programie Visual Studio Otwórz przeglądarkę serwera, Azure, Magazyn](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="0ca11-144">Zanotuj hello wspólnej część nazwy ścieżki hello, która jest pochodną klucz nazwy i instrumentacji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="0ca11-145">Witaj zdarzenia są zapisywane pliki tooblob w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0ca11-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="0ca11-146">Każdy plik może zawierać co najmniej jednego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0ca11-146">Each file may contain one or more events.</span></span> <span data-ttu-id="0ca11-147">Dlatego chcemy dane zdarzeń hello tooread i Filtruj limit pól hello, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="0ca11-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="0ca11-148">Wszystkie rodzaje czynności, które firma Microsoft może wykonywać hello danych, ale naszego planu obecnie jest toouse Stream Analytics toomove hello danych tooa bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="0ca11-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="0ca11-149">Który ułatwi partii łatwe toorun interesujące zapytań.</span><span class="sxs-lookup"><span data-stu-id="0ca11-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="0ca11-150">Utwórz bazę danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="0ca11-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="0ca11-151">Ponownie od subskrypcji w [portalu Azure][portal], Utwórz bazę danych hello (i nowy serwer, chyba że masz już jeden) toowhich przedstawiono tworzenie hello danych.</span><span class="sxs-lookup"><span data-stu-id="0ca11-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Nowe dane, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="0ca11-153">Upewnij się, że tego serwera bazy danych hello zezwala na dostęp tooAzure usług:</span><span class="sxs-lookup"><span data-stu-id="0ca11-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Przeglądaj, serwery, serwera, ustawień, zapory, tooAzure Zezwalaj na dostęp](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="0ca11-155">Utwórz tabelę w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ca11-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="0ca11-156">Połączenia bazy danych toohello utworzony w poprzedniej sekcji hello z narzędzia do zarządzania preferowany.</span><span class="sxs-lookup"><span data-stu-id="0ca11-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="0ca11-157">W ramach tego przewodnika użyjemy [narzędzia do zarządzania serwerem SQL](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="0ca11-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="0ca11-158">Utwórz nowe zapytanie i wykonaj powitania po T-SQL:</span><span class="sxs-lookup"><span data-stu-id="0ca11-158">Create a new query, and execute hello following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="0ca11-159">W tym przykładzie użyto dane wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="0ca11-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="0ca11-160">toosee hello innych dostępnych danych, sprawdź dane wyjściowe JSON i zobaczyć hello [wyeksportować modelu danych](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ca11-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="0ca11-161">Utwórz wystąpienie usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ca11-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="0ca11-162">Z hello [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz usługę Azure Stream Analytics hello i utworzyć nowe zadanie usługi Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="0ca11-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="0ca11-163">Podczas tworzenia nowego zadania hello rozwiń jego szczegóły:</span><span class="sxs-lookup"><span data-stu-id="0ca11-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="0ca11-164">Ustawianie lokalizacji obiektu blob</span><span class="sxs-lookup"><span data-stu-id="0ca11-164">Set blob location</span></span>
<span data-ttu-id="0ca11-165">Ustaw wprowadzania tootake z obiektu blob z eksportu ciągłego:</span><span class="sxs-lookup"><span data-stu-id="0ca11-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="0ca11-166">Teraz musisz hello podstawowy klucz dostępu z konta magazynu, który wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="0ca11-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="0ca11-167">Ustaw jako hello klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0ca11-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="0ca11-168">Wzorzec prefiksu ścieżki zestawu</span><span class="sxs-lookup"><span data-stu-id="0ca11-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="0ca11-169">Jest zbyt hello tooset się, że Format daty**RRRR-MM-DD** (z **łączniki**).</span><span class="sxs-lookup"><span data-stu-id="0ca11-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="0ca11-170">Witaj wzorzec prefiksu ścieżki Określa sposób odnajdowania usługi Stream Analytics plików wejściowych hello w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="0ca11-171">Należy tooset on toohow toocorrespond eksportu ciągłego przechowuje dane hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="0ca11-172">Ustaw go następująco:</span><span class="sxs-lookup"><span data-stu-id="0ca11-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="0ca11-173">W tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="0ca11-173">In this example:</span></span>

* <span data-ttu-id="0ca11-174">`webapplication27`to nazwa hello hello zasobu usługi Application Insights **w przypadku małych**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="0ca11-175">`1234...`jest klucz Instrumentacji hello hello zasobu usługi Application Insights **z kreskami usunięte**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="0ca11-176">`PageViews`Typ hello danych chcemy tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="0ca11-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="0ca11-177">dostępne typy Hello są zależne od filtru hello, ustawionych w eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="0ca11-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="0ca11-178">Sprawdź hello wyeksportowane dane toosee hello innych dostępnych typów i zobacz hello [wyeksportować modelu danych](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ca11-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="0ca11-179">`/{date}/{time}`wzorzec są zapisywane jako literału.</span><span class="sxs-lookup"><span data-stu-id="0ca11-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="0ca11-180">Nazwa hello tooget iKey zasobu usługi Application Insights, otwórz Essentials na stronie Przegląd i Otwórz ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0ca11-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="0ca11-181">Zakończ początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0ca11-181">Finish initial setup</span></span>
<span data-ttu-id="0ca11-182">Upewnij się, format serializacji hello:</span><span class="sxs-lookup"><span data-stu-id="0ca11-182">Confirm hello serialization format:</span></span>

![Potwierdź i zamknąć kreatora](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="0ca11-184">Zamknij kreatora hello i poczekaj, aż hello toocomplete Instalatora.</span><span class="sxs-lookup"><span data-stu-id="0ca11-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="0ca11-185">Użyj toocheck funkcja próbki hello poprawnie ustawiona ścieżka wejściowa hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="0ca11-186">Jeśli działanie nie powiodło się: Sprawdź, czy dane w magazynie hello zakresu czasu próbki hello została wybrana opcja.</span><span class="sxs-lookup"><span data-stu-id="0ca11-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="0ca11-187">Dokonaj edycji definicji wejściowych hello i sprawdź Ustaw hello konta magazynu, ścieżkę prefiks i Data formacie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="0ca11-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="0ca11-188">Zapytanie zestawu</span><span class="sxs-lookup"><span data-stu-id="0ca11-188">Set query</span></span>
<span data-ttu-id="0ca11-189">Otwórz sekcję zapytania hello:</span><span class="sxs-lookup"><span data-stu-id="0ca11-189">Open hello query section:</span></span>

![Analiza strumienia wybierz zapytanie](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="0ca11-191">Zastąp hello domyślne zapytanie z:</span><span class="sxs-lookup"><span data-stu-id="0ca11-191">Replace hello default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="0ca11-192">Należy zauważyć, że najpierw hello kilka właściwości są toopage określonych danych widoku.</span><span class="sxs-lookup"><span data-stu-id="0ca11-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="0ca11-193">Eksporty inne typy telemetrii ma inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="0ca11-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="0ca11-194">Zobacz hello [szczegółowe odwołania do modelu danych dla hello typy właściwości i wartości.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="0ca11-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="0ca11-195">Konfigurowanie toodatabase danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="0ca11-195">Set up output toodatabase</span></span>
<span data-ttu-id="0ca11-196">Wybierz SQL jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-196">Select SQL as hello output.</span></span>

![Analiza strumienia wybierz dane wyjściowe](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="0ca11-198">Określ bazę danych SQL hello.</span><span class="sxs-lookup"><span data-stu-id="0ca11-198">Specify hello SQL database.</span></span>

![Uzupełnij informacje dotyczące hello bazy danych](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="0ca11-200">Zamknij kreatora hello i poczekaj, aż powiadomienie, które skonfigurowano hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0ca11-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="0ca11-201">Rozpocznij przetwarzanie</span><span class="sxs-lookup"><span data-stu-id="0ca11-201">Start processing</span></span>
<span data-ttu-id="0ca11-202">Uruchom zadanie hello z hello pasku akcji:</span><span class="sxs-lookup"><span data-stu-id="0ca11-202">Start hello job from hello action bar:</span></span>

![W module analiz strumienia kliknij przycisk Start](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="0ca11-204">Można wybrać, czy przetwarzanie toostart hello danych od teraz lub toostart z wcześniejszych danych.</span><span class="sxs-lookup"><span data-stu-id="0ca11-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="0ca11-205">ostatnie Hello jest przydatne, jeśli masz już uruchomione na chwilę eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="0ca11-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![W module analiz strumienia kliknij przycisk Start](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="0ca11-207">Po kilku minutach Przejdź wstecz tooSQL narzędzia do zarządzania serwerem i obejrzyj hello przepływu danych, w.</span><span class="sxs-lookup"><span data-stu-id="0ca11-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="0ca11-208">Na przykład użyć zapytania następująco:</span><span class="sxs-lookup"><span data-stu-id="0ca11-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="0ca11-209">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="0ca11-209">Related articles</span></span>
* [<span data-ttu-id="0ca11-210">Eksportuj tooPowerBI przy użyciu usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="0ca11-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="0ca11-211">Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="0ca11-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="0ca11-212">Eksport ciągły w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ca11-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="0ca11-213">Usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ca11-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

