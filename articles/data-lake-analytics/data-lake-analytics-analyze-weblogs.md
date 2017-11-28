---
title: "Dzienniki aaaAnalyze witryny sieci Web przy użyciu usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dzienników tooanalyze witryn sieci Web, przy użyciu usługi Data Lake Analytics. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="16c0d-103">Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="16c0d-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="16c0d-104">Dowiedz się, jak tooanalyze dzienników witryn sieci Web przy użyciu usługi Data Lake Analytics, szczególnie w przypadku sprawdzanie odwołań, które napotkał błędy podczas próby toovisit hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16c0d-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16c0d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16c0d-105">Prerequisites</span></span>
* <span data-ttu-id="16c0d-106">**Visual Studio 2015 lub Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="16c0d-107">**[Data Lake Tools dla Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="16c0d-108">Po zainstalowaniu narzędzi Data Lake Tools dla programu Visual Studio, zostanie wyświetlona **usługi Data Lake** elementu hello **narzędzia** menu w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="16c0d-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="16c0d-110">**Podstawową wiedzę na temat usługi Data Lake Analytics i hello narzędzi Data Lake Tools dla programu Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="16c0d-111">tooget pracę, zobacz:</span><span class="sxs-lookup"><span data-stu-id="16c0d-111">tooget started, see:</span></span>

  * <span data-ttu-id="16c0d-112">[Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="16c0d-113">**Konto usługi Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="16c0d-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="16c0d-114">Zobacz [Tworzenie konta usługi Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="16c0d-115">**Przekaż konta Data Lake Analytics toohello hello przykładowych danych.**</span><span class="sxs-lookup"><span data-stu-id="16c0d-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="16c0d-116">Zobacz [pliki danych przykładowych toocopy](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="16c0d-117">toorun zadania usługi Data Lake Analytics, konieczne będzie niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="16c0d-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="16c0d-118">Mimo że hello narzędzi Data Lake Tools obsługują przekazywanie danych, zostanie użyty hello portalu tooupload hello przykładowych danych toomake tego samouczka toofollow łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="16c0d-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="16c0d-119">Połącz tooAzure</span><span class="sxs-lookup"><span data-stu-id="16c0d-119">Connect tooAzure</span></span>
<span data-ttu-id="16c0d-120">Zanim można utworzyć i przetestować skrypty U-SQL, należy najpierw połączyć tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16c0d-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="16c0d-121">**tooData tooconnect Lake — analiza**</span><span class="sxs-lookup"><span data-stu-id="16c0d-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="16c0d-122">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16c0d-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="16c0d-123">Kliknij przycisk **usługi Data Lake > Opcje i ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="16c0d-124">Kliknij przycisk **logowania**, lub **Zmień użytkownika** Jeśli ktoś zalogował się i postępuj zgodnie z instrukcjami hello.</span><span class="sxs-lookup"><span data-stu-id="16c0d-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="16c0d-125">Kliknij przycisk **OK** tooclose hello opcji i ustawień okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="16c0d-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="16c0d-126">**toobrowse Twojego konta usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="16c0d-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="16c0d-127">W programie Visual Studio Otwórz **Eksploratora serwera** przez naciśnij **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="16c0d-128">W **Eksploratorze serwera** rozwiń węzeł **Azure**, a następnie rozwiń węzeł **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="16c0d-129">Zostanie wyświetlona lista kont usługi Data Lake Analytics, o ile jakieś istnieją.</span><span class="sxs-lookup"><span data-stu-id="16c0d-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="16c0d-130">Nie można utworzyć kont usługi Data Lake Analytics z hello studio.</span><span class="sxs-lookup"><span data-stu-id="16c0d-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="16c0d-131">toocreate konto, zobacz [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md) lub [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="16c0d-132">Tworzenie aplikacji U-SQL</span><span class="sxs-lookup"><span data-stu-id="16c0d-132">Develop U-SQL application</span></span>
<span data-ttu-id="16c0d-133">Aplikacja U-SQL jest przeważnie skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="16c0d-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="16c0d-134">toolearn więcej informacji o języku U-SQL, zobacz [wprowadzenie do języka U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="16c0d-135">Możesz dodać dodanie operatory zdefiniowane przez użytkownika toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16c0d-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="16c0d-136">Aby uzyskać więcej informacji, zobacz [operatory zadań usługi Data Lake Analytics zdefiniowane przez użytkownika opracowanie U-SQL](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="16c0d-137">**toocreate i przesłać zadanie usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="16c0d-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="16c0d-138">Kliknij przycisk hello **Plik > Nowy > Projekt**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="16c0d-139">Wybierz typ projektu U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="16c0d-139">Select hello U-SQL Project type.</span></span>

    ![nowy projekt U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="16c0d-141">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-141">Click **OK**.</span></span> <span data-ttu-id="16c0d-142">Visual studio tworzy rozwiązanie z plikiem Script.usql.</span><span class="sxs-lookup"><span data-stu-id="16c0d-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="16c0d-143">Wprowadź hello następującego skryptu do pliku Script.usql hello:</span><span class="sxs-lookup"><span data-stu-id="16c0d-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="16c0d-144">Witaj toounderstand U-SQL, zobacz [wprowadzenie do języka U-SQL w programie Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="16c0d-145">Dodaj nowy projekt tooyour skryptu U-SQL i wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="16c0d-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="16c0d-146">Przełącz wstecz toohello pierwszy skryptu U-SQL i dalej toohello **przesyłania** przycisku, określ konto usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="16c0d-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="16c0d-147">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Build Script** (Kompiluj skrypt).</span><span class="sxs-lookup"><span data-stu-id="16c0d-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="16c0d-148">Sprawdź wyniki hello w okienku danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="16c0d-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="16c0d-149">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Submit Script** (Prześlij skrypt).</span><span class="sxs-lookup"><span data-stu-id="16c0d-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="16c0d-150">Sprawdź hello **konta usługi Analytics** jest hello co gdzie toorun hello zadanie, a następnie kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="16c0d-151">Wyniki przesyłania i link do zadania są dostępne w hello narzędzi Data Lake Tools dla programu Visual Studio wyniki okna po zakończeniu przesyłania hello.</span><span class="sxs-lookup"><span data-stu-id="16c0d-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="16c0d-152">Poczekaj, aż zadanie hello zakończyło się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="16c0d-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="16c0d-153">Jeśli zadanie hello nie powiodło się, prawdopodobnie brakuje hello pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="16c0d-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="16c0d-154">Zobacz sekcję wymagań wstępnych hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="16c0d-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="16c0d-155">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, zobacz [monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="16c0d-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="16c0d-156">Po zakończeniu zadania hello zostanie wyświetlona po ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="16c0d-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![Usługa Data lake analytics analizowanie dzienników witryn sieci Web dzienników sieci Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="16c0d-158">Teraz Powtórz kroki od 7 do 10 dla **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="16c0d-159">**dane wyjściowe zadania hello toosee**</span><span class="sxs-lookup"><span data-stu-id="16c0d-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="16c0d-160">Z **Eksploratora serwera**, rozwiń węzeł **Azure**, rozwiń węzeł **usługi Data Lake Analytics**, rozwiń konto usługi Data Lake Analytics, rozwiń węzeł **kont magazynu**, kliknij prawym przyciskiem myszy hello domyślnego konta usługi Data Lake Storage, a następnie kliknij przycisk **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="16c0d-161">Kliknij dwukrotnie **przykłady** tooopen hello folder, a następnie kliknij dwukrotnie **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="16c0d-162">Kliknij dwukrotnie **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="16c0d-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="16c0d-163">Dwukrotne kliknięcie pliku wyjściowego hello w widoku wykresu hello hello zadania w kolejności toonavigate bezpośrednio toohello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="16c0d-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="16c0d-164">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="16c0d-164">See also</span></span>
<span data-ttu-id="16c0d-165">tooget wprowadzenie do usługi Data Lake Analytics przy użyciu różnych narzędzi, zobacz:</span><span class="sxs-lookup"><span data-stu-id="16c0d-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="16c0d-166">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="16c0d-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="16c0d-167">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="16c0d-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="16c0d-168">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu zestawu SDK programu .NET</span><span class="sxs-lookup"><span data-stu-id="16c0d-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
