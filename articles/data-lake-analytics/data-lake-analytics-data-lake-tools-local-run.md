---
title: "aaaTest i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i hello zestawu SDK usługi Azure Data Lake U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania toouse Azure Data Lake Tools dla Visual Studio i hello tootest zestawu SDK usługi Azure Data Lake U-SQL i debugowania skryptu U-SQL w sieci lokalnej stacji roboczej."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Testowanie i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i hello zestawu SDK usługi Azure Data Lake U-SQL

Można użyć usługi Azure Data Lake Tools dla Visual Studio i zadań U-SQL toorun zestawu SDK usługi Azure Data Lake U-SQL hello na stacji roboczej, tak samo jak w usłudze Azure Data Lake hello. Te dwie funkcje uruchamiania lokalnego pozwalają zaoszczędzić czas poświęcony na testowanie i debugowanie zadań U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Folder główny danych hello i ścieżka pliku hello

Zarówno przebiegu lokalnego, jak i hello SDK U-SQL wymagają folderu głównego danych. folder główny danych Hello dotyczy konto obliczeniowe lokalne powitania "Magazyn lokalny". To konto usługi Azure Data Lake Store równoważne toohello konto usługi Data Lake Analytics. Przełączanie tooa folder różnych głównych danych jest podobnie jak przełączanie tooa magazynu innego konta. Jeśli chcesz tooaccess często udostępnionych danych z różnych głównych danych folderów, należy użyć ścieżek bezwzględnych w skryptach. Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w obszarze hello danych głównych folder toopoint toohello udostępnionych danych.

folder główny danych Hello jest używany do:

- Przechowywania metadanych, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawów.
- Wyszukiwanie hello danych wejściowych i wyjściowych ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL. Używanie ścieżek względnych umożliwia łatwiejsze toodeploy Twojego tooAzure projektów języka U-SQL.

W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną. Ścieżka względna Hello jest ścieżka folderu względna toohello określony katalog główny danych. Zaleca się, że można użyć "/" jako hello toomake separatora ścieżki skryptów zgodny z powitania po stronie serwera. Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej. W tym przykładzie C:\LocalRunDataRoot jest folder główny danych hello.

|Ścieżka względna|Ścieżki bezwzględne|
|-------------|-------------|
|/ABC/DEF/Input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/Input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/Input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Użyj lokalnego uruchomienia z programu Visual Studio

Narzędzia Data Lake Tools dla programu Visual Studio zapewnia obsługę lokalnej — Uruchom U-SQL w programie Visual Studio. Za pomocą tej funkcji, można:

- Uruchom skrypt U-SQL lokalnie, wraz z zestawami języka C#.
- Debugowanie zestawu języka C# lokalnie.
- Tworzenie, wyświetlanie i usuwanie katalogów U-SQL (lokalnych baz danych, zestawy, schematy i tabele) z poziomu Eksploratora serwera. Znajduje się też katalogu lokalnego hello także z poziomu Eksploratora serwera.

    ![Narzędzia Data Lake Tools dla katalogu lokalnego lokalnego uruchomienia programu Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Witaj narzędzi Data Lake Tools Instalator tworzy toobe folderu C:\LocalRunRoot, używane jako hello domyślny folder główny danych. Równoległość lokalnego uruchomienia domyślne Hello jest 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure lokalnego uruchamiania programu Visual Studio

1. Otwórz program Visual Studio.
2. Otwórz **Eksploratora serwera**.
3. Rozwiń węzeł **Azure** > **usługi Data Lake Analytics**.
4. Kliknij przycisk hello **usługi Data Lake** menu, a następnie kliknij przycisk **opcje i ustawienia**.
5. W drzewie po lewej stronie powitania rozwiń **usługi Azure Data Lake**, a następnie rozwiń węzeł **ogólne**.

    ![Narzędzia Data Lake Tools dla programu Visual Studio Uruchom lokalny Konfigurowanie ustawień](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Projektu programu Visual Studio U-SQL jest wymagana do wykonania lokalnego uruchamiania. Ta część różni się od uruchamiania skryptów U-SQL na platformie Azure.

### <a name="toorun-a-u-sql-script-locally"></a>skrypt toorun U-SQL lokalnie
1. W programie Visual Studio Otwórz projekt U-SQL.   
2. Kliknij prawym przyciskiem myszy skrypt U-SQL w Eksploratorze rozwiązań, a następnie kliknij przycisk **Prześlij skrypt**.
3. Wybierz **(Local)** jako hello Analytics konta toorun skrypt lokalnie.
Możesz również kliknąć hello **(Local)** konta na powitania u góry okna Skrypt, a następnie kliknij przycisk **przesyłania** (lub użyj Witaj Ctrl + F5 skrótu klawiaturowego).

    ![Narzędzia Data Lake Tools dla Visual Studio lokalnego uruchomienia przesyłania zadań](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Debugowanie skryptów i zestawów języka C# lokalnie

Można debugować zestawy języka C# bez przesyłania i rejestrowania ich tooAzure Data Lake Analytics usługi. Można ustawić punktów przerwania w kodzie pliku zarówno hello i w odwołaniu projekcie C#.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug kod lokalny w kodzie pliku

1. Ustaw punkty przerwania w kodzie hello pliku.
2. Naciśnij klawisz F5 toodebug hello skrypt lokalnie.

> [!NOTE]
   > Witaj następujące procedury działa tylko w programie Visual Studio 2015. W starszych Visual Studio może być konieczne toomanually Dodaj hello pliki pdb.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug kod lokalny w odwołaniu projekcie C#

1. Utwórz projekt zestawu języka C# i skompiluj go toogenerate hello wyjściowy plik dll.
2. Zarejestruj hello biblioteki dll przy użyciu instrukcji U-SQL:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Ustaw punkty przerwania w hello kod w języku C#.
4. Naciśnij klawisz F5 toodebug hello skryptu z wywoływanym dll hello C# lokalnie.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Użyj lokalnego uruchamiania z hello SDK Data Lake U-SQL

Ponadto skrypty toorunning U-SQL lokalnie, używając programu Visual Studio, za pomocą skryptów U-SQL toorun hello w zestawie SDK usługi Azure Data Lake U-SQL lokalnie interfejsów programowania i z wierszem polecenia. Za pomocą tych opcji można skalować test lokalnego skryptu U-SQL.

Dowiedz się więcej o [zestawu SDK usługi Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Następne kroki

* toosee bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).
* widoku wykonania wierzchołka hello toouse, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
