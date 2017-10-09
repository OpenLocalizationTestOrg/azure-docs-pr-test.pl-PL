---
title: "skrypty aaaDevelop U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Data Lake Tools dla programu Visual Studio i jak toodevelop i testowania skryptów U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools for Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Dowiedz się, jak toouse Visual Studio toocreate kont usługi Azure Data Lake Analytics, definiowania zadań w [U-SQL](data-lake-analytics-u-sql-get-started.md)i przesyłanie usługi Data Lake Analytics toohello zadania. Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Wymagania wstępne

* **Visual Studio**: obsługiwane są wszystkie wersje z wyjątkiem Express.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Zestaw Microsoft Azure SDK dla platformy .NET** w wersji 2.7.1 lub nowszej.  Zainstalować go za pomocą hello [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Konto usługi **Data Lake Analytics**. toocreate konto, zobacz [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Instalowanie narzędzi Azure Data Lake Tools for Visual Studio 

Pobierz i zainstaluj usługi Azure Data Lake Tools dla Visual Studio [z Centrum pobierania hello](http://aka.ms/adltoolsvs). Po instalacji pamiętaj, że:
* Witaj **Eksploratora serwera** > **Azure** zawiera węzeł **usługi Data Lake Analytics** węzła. 
* Witaj **narzędzia** menu ma **usługi Data Lake** elementu.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Połącz tooan konta usługi Azure Data Lake Analytics

1. Otwórz program Visual Studio.
2. Otwórz Eksplorator serwera, wybierając pozycje **Widok** > **Eksplorator serwera**.
3. Kliknij prawym przyciskiem myszy pozycję **Azure**. Następnie wybierz **połączyć tooMicrosoft subskrypcji Azure** i postępuj zgodnie z instrukcjami hello.
4. W Eksploratorze serwera wybierz pozycje **Azure** > **Data Lake Analytics**. Zobaczysz listę swoich kont usługi Data Lake Analytics.


## <a name="write-your-first-u-sql-script"></a>Pisanie pierwszego skryptu U-SQL

powitania po tekst jest prosty skrypt U-SQL. Definiuje małym zestawie danych i operacji zapisu, które dataset toohello domyślne Data Lake Store jako plik o nazwie `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>Przesyłanie zadania usługi Data Lake Analytics

1. Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**.

2. Wybierz hello **projektu U-SQL** typu, a następnie kliknij przycisk **OK**. Program Visual Studio utworzy rozwiązanie z użyciem pliku **Script.usql**.

3. Wklej hello poprzedni skrypt do hello **Script.usql** okna.

4. W lewym górnym narożniku hello hello **Script.usql** okna, określ konto usługi Data Lake Analytics hello.

    ![Przesyłanie projektu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. W lewym górnym narożniku hello hello **Script.usql** wybierz **przesyłania**.
6. Sprawdź hello **konta usługi Analytics**, a następnie wybierz **przesyłania**. Wyniki przesyłania są dostępne w hello narzędzi Data Lake Tools dla programu Visual Studio wyników, po zakończeniu przesyłania hello.

    ![Przesyłanie projektu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello najnowszego zadania stanu i Odśwież hello ekran, kliknij przycisk **Odśwież**. Zadanie hello zakończy się powodzeniem, wyświetlane hello **wykres zadania**, **operacji na metadanych**, **historii stanu**, i **diagnostyki**:

    ![Wykres wydajności zadania skryptu U-SQL programu Visual Studio w usłudze Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Zadanie podsumowania** pokazuje hello podsumowanie hello zadania.   
   * **Szczegóły zadania** przedstawiono bardziej szczegółowe informacje o zadaniu hello, w tym hello skryptu, zasobów i wierzchołków.
   * **Wykres zadania** wizualizuje hello postęp zadania hello.
   * **Operacji na metadanych** pokazuje wszystkie akcje hello w wykazie hello U-SQL.
   * **Dane** pokazuje wszystkie hello wejścia i wyjścia.
   * Karta **Diagnostyka** udostępnia zaawansowaną analizę wykonywania zadania i optymalizacji wydajności.

### <a name="toocheck-job-state"></a>Stan zadania toocheck

1. W Eksploratorze serwera wybierz pozycje **Azure** > **Data Lake Analytics**. 
2. Rozwiń nazwę konta usługi Data Lake Analytics hello.
3. Kliknij dwukrotnie pozycję **Zadania**.
4. Wybierz zadanie hello, które wcześniej zostały przesłane.

### <a name="toosee-hello-output-of-a-job"></a>toosee hello dane wyjściowe zadania

1. W Eksploratorze serwera Przeglądaj toohello zadanie, które zostało przesłane.
2. Kliknij przycisk hello **danych** kartę.
3. W hello **dane wyjściowe zadania** kartę, zaznacz hello `"/data.csv"` pliku.

## <a name="next-steps"></a>Następne kroki

* [Uruchamianie skryptów U-SQL na swojej stacji roboczej w celu testowania i debugowania](data-lake-analytics-data-lake-tools-local-run.md)
* [Debugowanie kodu C# w zadaniach U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Użyj hello Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
