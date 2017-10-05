---
title: "Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i analizowanie dzienników witryn sieci Web przy użyciu usługi Data Lake Analytics. "
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="d17a5-103">Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d17a5-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="d17a5-104">Dowiedz się, jak i analizowanie dzienników witryn sieci Web przy użyciu usługi Data Lake Analytics, szczególnie w przypadku sprawdzanie odwołań, które pojawiły się błędy w podczas próby uzyskania witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d17a5-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d17a5-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d17a5-105">Prerequisites</span></span>
* <span data-ttu-id="d17a5-106">**Visual Studio 2015 lub Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="d17a5-107">**[Data Lake Tools dla Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="d17a5-108">Po zainstalowaniu narzędzi Data Lake Tools dla programu Visual Studio, zostanie wyświetlona **usługi Data Lake** elementu **narzędzia** menu w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d17a5-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="d17a5-110">**Podstawową wiedzę na temat usługi Data Lake Analytics i narzędzi Data Lake Tools dla programu Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="d17a5-111">Aby rozpocząć, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d17a5-111">To get started, see:</span></span>

  * <span data-ttu-id="d17a5-112">[Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d17a5-113">**Konto usługi Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="d17a5-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="d17a5-114">Zobacz [Tworzenie konta usługi Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="d17a5-115">**Przekaż przykładowe dane do konta usługi Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="d17a5-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="d17a5-116">Zobacz [można skopiować pliki danych przykładowych](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="d17a5-117">Do uruchomienia zadania w usłudze Data Lake Analytics potrzebne są określone dane.</span><span class="sxs-lookup"><span data-stu-id="d17a5-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="d17a5-118">Chociaż narzędzia Data Lake Tools obsługują przekazywanie danych, przekaż przykładowe dane za pośrednictwem portalu, aby łatwiej wykonać instrukcje przedstawione w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d17a5-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="d17a5-119">Nawiązywanie połączenia z usługą Azure</span><span class="sxs-lookup"><span data-stu-id="d17a5-119">Connect to Azure</span></span>
<span data-ttu-id="d17a5-120">Aby można było kompilacji i przetestować skrypty U-SQL, musisz najpierw połączyć na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d17a5-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="d17a5-121">**Aby nawiązać połączenie z usługą Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="d17a5-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="d17a5-122">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d17a5-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="d17a5-123">Kliknij przycisk **usługi Data Lake > Opcje i ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="d17a5-124">Kliknij przycisk **logowania**, lub **Zmień użytkownika** Jeśli ktoś zalogował się i postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="d17a5-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="d17a5-125">Kliknij przycisk **OK** aby zamknąć okno dialogowe opcji i ustawień.</span><span class="sxs-lookup"><span data-stu-id="d17a5-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="d17a5-126">**Aby przeglądać swoje konta usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="d17a5-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="d17a5-127">W programie Visual Studio Otwórz **Eksploratora serwera** przez naciśnij **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="d17a5-128">W **Eksploratorze serwera** rozwiń węzeł **Azure**, a następnie rozwiń węzeł **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="d17a5-129">Zostanie wyświetlona lista kont usługi Data Lake Analytics, o ile jakieś istnieją.</span><span class="sxs-lookup"><span data-stu-id="d17a5-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="d17a5-130">Nie można utworzyć kont usługi Data Lake Analytics z studio.</span><span class="sxs-lookup"><span data-stu-id="d17a5-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="d17a5-131">Aby utworzyć konto, zobacz temat [Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu Portalu Azure](data-lake-analytics-get-started-portal.md) lub [Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="d17a5-132">Tworzenie aplikacji U-SQL</span><span class="sxs-lookup"><span data-stu-id="d17a5-132">Develop U-SQL application</span></span>
<span data-ttu-id="d17a5-133">Aplikacja U-SQL jest przeważnie skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d17a5-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="d17a5-134">Aby dowiedzieć się więcej o języku U-SQL, zobacz [wprowadzenie do języka U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="d17a5-135">Dodanie operatory zdefiniowane przez użytkownika można dodać do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d17a5-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="d17a5-136">Aby uzyskać więcej informacji, zobacz [operatory zadań usługi Data Lake Analytics zdefiniowane przez użytkownika opracowanie U-SQL](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="d17a5-137">**Aby utworzyć i przesłać zadanie usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="d17a5-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="d17a5-138">Kliknij przycisk **Plik > Nowy > Projekt**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="d17a5-139">Wybierz typ projektu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d17a5-139">Select the U-SQL Project type.</span></span>

    ![nowy projekt U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="d17a5-141">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-141">Click **OK**.</span></span> <span data-ttu-id="d17a5-142">Visual studio tworzy rozwiązanie z plikiem Script.usql.</span><span class="sxs-lookup"><span data-stu-id="d17a5-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="d17a5-143">Wprowadź następujący skrypt do pliku Script.usql:</span><span class="sxs-lookup"><span data-stu-id="d17a5-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="d17a5-144">Aby poznać U-SQL, zobacz [wprowadzenie do języka U-SQL w programie Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="d17a5-145">Dodaj nowy skrypt U-SQL do projektu i wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="d17a5-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="d17a5-146">Przełącz wstecz do pierwszego skryptu U-SQL i obok pozycji **przesyłania** przycisku, określ konto usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="d17a5-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="d17a5-147">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Build Script** (Kompiluj skrypt).</span><span class="sxs-lookup"><span data-stu-id="d17a5-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="d17a5-148">Sprawdź wyniki w okienku danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d17a5-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="d17a5-149">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Submit Script** (Prześlij skrypt).</span><span class="sxs-lookup"><span data-stu-id="d17a5-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="d17a5-150">Sprawdź **konta usługi Analytics** jest tą, w którym chcesz uruchomić zadanie, a następnie kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="d17a5-151">Po zakończeniu przesyłania wyniki przesyłania i link do zadania są dostępne w oknie wyników narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d17a5-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="d17a5-152">Zaczekaj, aż zadanie zakończyło się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d17a5-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="d17a5-153">Jeśli zadanie nie powiodło się, prawdopodobnie brakuje pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="d17a5-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="d17a5-154">Zobacz sekcję wymagań wstępnych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d17a5-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="d17a5-155">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, zobacz [monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d17a5-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="d17a5-156">Po zakończeniu zadania jest wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="d17a5-156">When the job is completed, you shall see the following screen:</span></span>

    ![Usługa Data lake analytics analizowanie dzienników witryn sieci Web dzienników sieci Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="d17a5-158">Teraz Powtórz kroki od 7 do 10 dla **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="d17a5-159">**Aby wyświetlić dane wyjściowe zadania**</span><span class="sxs-lookup"><span data-stu-id="d17a5-159">**To see the job output**</span></span>

1. <span data-ttu-id="d17a5-160">W **Eksploratorze serwera** rozwiń węzeł **Azure**, rozwiń węzeł **Data Lake Analytics**, rozwiń konto usługi Data Lake Analytics, rozwiń węzeł **Konta magazynu**, kliknij prawym przyciskiem myszy domyślne konto usługi Data Lake Storage, a następnie kliknij przycisk **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="d17a5-161">Kliknij dwukrotnie **przykłady** do Otwórz folder, a następnie kliknij dwukrotnie **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="d17a5-162">Kliknij dwukrotnie **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="d17a5-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="d17a5-163">Możesz również dwukrotnie pliku wyjściowego, w widoku wykresu zadania, aby przejść bezpośrednio do wyjścia.</span><span class="sxs-lookup"><span data-stu-id="d17a5-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="d17a5-164">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d17a5-164">See also</span></span>
<span data-ttu-id="d17a5-165">Aby rozpocząć pracę z usługą Data Lake Analytics przy użyciu różnych narzędzi, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d17a5-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="d17a5-166">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d17a5-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d17a5-167">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d17a5-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="d17a5-168">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu zestawu SDK programu .NET</span><span class="sxs-lookup"><span data-stu-id="d17a5-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
