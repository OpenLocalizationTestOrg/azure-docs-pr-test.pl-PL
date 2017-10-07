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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics
Dowiedz się, jak tooanalyze dzienników witryn sieci Web przy użyciu usługi Data Lake Analytics, szczególnie w przypadku sprawdzanie odwołań, które napotkał błędy podczas próby toovisit hello witryny sieci Web.

## <a name="prerequisites"></a>Wymagania wstępne
* **Visual Studio 2015 lub Visual Studio 2013**.
* **[Data Lake Tools dla Visual Studio](http://aka.ms/adltoolsvs)**.

    Po zainstalowaniu narzędzi Data Lake Tools dla programu Visual Studio, zostanie wyświetlona **usługi Data Lake** elementu hello **narzędzia** menu w programie Visual Studio:

    ![Menu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Podstawową wiedzę na temat usługi Data Lake Analytics i hello narzędzi Data Lake Tools dla programu Visual Studio**. tooget pracę, zobacz:

  * [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Konto usługi Data Lake Analytics.**  Zobacz [Tworzenie konta usługi Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
* **Przekaż konta Data Lake Analytics toohello hello przykładowych danych.** Zobacz [pliki danych przykładowych toocopy](data-lake-analytics-get-started-portal.md).

    toorun zadania usługi Data Lake Analytics, konieczne będzie niektórych danych. Mimo że hello narzędzi Data Lake Tools obsługują przekazywanie danych, zostanie użyty hello portalu tooupload hello przykładowych danych toomake tego samouczka toofollow łatwiejsze.

## <a name="connect-tooazure"></a>Połącz tooAzure
Zanim można utworzyć i przetestować skrypty U-SQL, należy najpierw połączyć tooAzure.

**tooData tooconnect Lake — analiza**

1. Otwórz program Visual Studio.
2. Kliknij przycisk **usługi Data Lake > Opcje i ustawienia**.
3. Kliknij przycisk **logowania**, lub **Zmień użytkownika** Jeśli ktoś zalogował się i postępuj zgodnie z instrukcjami hello.
4. Kliknij przycisk **OK** tooclose hello opcji i ustawień okna dialogowego.

**toobrowse Twojego konta usługi Data Lake Analytics**

1. W programie Visual Studio Otwórz **Eksploratora serwera** przez naciśnij **CTRL + ALT + S**.
2. W **Eksploratorze serwera** rozwiń węzeł **Azure**, a następnie rozwiń węzeł **Data Lake Analytics**. Zostanie wyświetlona lista kont usługi Data Lake Analytics, o ile jakieś istnieją. Nie można utworzyć kont usługi Data Lake Analytics z hello studio. toocreate konto, zobacz [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md) lub [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Tworzenie aplikacji U-SQL
Aplikacja U-SQL jest przeważnie skrypt U-SQL. toolearn więcej informacji o języku U-SQL, zobacz [wprowadzenie do języka U-SQL](data-lake-analytics-u-sql-get-started.md).

Możesz dodać dodanie operatory zdefiniowane przez użytkownika toohello aplikacji.  Aby uzyskać więcej informacji, zobacz [operatory zadań usługi Data Lake Analytics zdefiniowane przez użytkownika opracowanie U-SQL](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate i przesłać zadanie usługi Data Lake Analytics**

1. Kliknij przycisk hello **Plik > Nowy > Projekt**.
2. Wybierz typ projektu U-SQL hello.

    ![nowy projekt U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Kliknij przycisk **OK**. Visual studio tworzy rozwiązanie z plikiem Script.usql.
4. Wprowadź hello następującego skryptu do pliku Script.usql hello:

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

    Witaj toounderstand U-SQL, zobacz [wprowadzenie do języka U-SQL w programie Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).    
5. Dodaj nowy projekt tooyour skryptu U-SQL i wprowadź następujące hello:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Przełącz wstecz toohello pierwszy skryptu U-SQL i dalej toohello **przesyłania** przycisku, określ konto usługi Analytics.
7. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Build Script** (Kompiluj skrypt). Sprawdź wyniki hello w okienku danych wyjściowych hello.
8. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Submit Script** (Prześlij skrypt).
9. Sprawdź hello **konta usługi Analytics** jest hello co gdzie toorun hello zadanie, a następnie kliknij przycisk **przesyłania**. Wyniki przesyłania i link do zadania są dostępne w hello narzędzi Data Lake Tools dla programu Visual Studio wyniki okna po zakończeniu przesyłania hello.
10. Poczekaj, aż zadanie hello zakończyło się powodzeniem.  Jeśli zadanie hello nie powiodło się, prawdopodobnie brakuje hello pliku źródłowego.  Zobacz sekcję wymagań wstępnych hello tego samouczka. Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, zobacz [monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Po zakończeniu zadania hello zostanie wyświetlona po ekranie powitania:

    ![Usługa Data lake analytics analizowanie dzienników witryn sieci Web dzienników sieci Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Teraz Powtórz kroki od 7 do 10 dla **Script1.usql**.

**dane wyjściowe zadania hello toosee**

1. Z **Eksploratora serwera**, rozwiń węzeł **Azure**, rozwiń węzeł **usługi Data Lake Analytics**, rozwiń konto usługi Data Lake Analytics, rozwiń węzeł **kont magazynu**, kliknij prawym przyciskiem myszy hello domyślnego konta usługi Data Lake Storage, a następnie kliknij przycisk **Explorer**.
2. Kliknij dwukrotnie **przykłady** tooopen hello folder, a następnie kliknij dwukrotnie **dane wyjściowe**.
3. Kliknij dwukrotnie **UnsuccessfulResponsees.log**.
4. Dwukrotne kliknięcie pliku wyjściowego hello w widoku wykresu hello hello zadania w kolejności toonavigate bezpośrednio toohello danych wyjściowych.

## <a name="see-also"></a>Zobacz też
tooget wprowadzenie do usługi Data Lake Analytics przy użyciu różnych narzędzi, zobacz:

* [Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md)
* [Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu zestawu SDK programu .NET](data-lake-analytics-get-started-net-sdk.md)
