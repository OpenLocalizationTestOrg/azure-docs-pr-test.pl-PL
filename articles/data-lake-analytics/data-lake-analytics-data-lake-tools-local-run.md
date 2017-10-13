---
title: "Testowanie i debugowanie zadań U-SQL przy użyciu zestawu SDK usługi Azure Data Lake U-SQL i lokalne uruchamianie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure Data Lake Tools dla programu Visual Studio i zestaw SDK usługi Azure Data Lake U-SQL umożliwia testowanie i debugowanie zadań U-SQL w sieci lokalnej stacji roboczej."
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
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a>Testowanie i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i zestawu SDK usługi Azure Data Lake U-SQL

Przy użyciu narzędzi Azure Data Lake Tools for Visual Studio i zestawu SDK U-SQL usługi Azure Data Lake można uruchamiać zadania U-SQL na stacji roboczej, podobnie jak w usłudze Azure Data Lake. Te dwie funkcje uruchamiania lokalnego pozwalają zaoszczędzić czas poświęcony na testowanie i debugowanie zadań U-SQL.

## <a name="understand-the-data-root-folder-and-the-file-path"></a>Folder główny danych i ścieżka pliku

Zarówno przebiegu lokalnego, jak i zestawu SDK języka U-SQL wymagają folderu głównego danych. Folder główny danych jest "Magazyn lokalny" dla konta lokalnego obliczeń. Odpowiada to konto usługi Azure Data Lake Store z kontem usługi Data Lake Analytics. Przełączanie do folderu różnych głównych danych jest podobnie jak przełączanie do konta magazynu innego. Jeśli chcesz uzyskać dostęp do danych często udostępnione z innego katalogu głównym danych folderów, należy użyć ścieżek bezwzględnych w skryptach. Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w folderze głównym danych wskaż udostępnionych danych.

Folder główny danych służy do:

- Przechowywania metadanych, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawów.
- Wyszukiwanie wejściowymi i wyjściowymi ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL. Używanie ścieżek względnych ułatwia wdrażanie projektów języka U-SQL na platformie Azure.

W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną. Ścieżka względna jest względem ścieżki katalogu głównym danych określonego folderu. Firma Microsoft zaleca użycie "/" jako separatora ścieżki do sprawia, że skrypty zgodne z po stronie serwera. Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej. W tych przykładach C:\LocalRunDataRoot jest folder główny danych.

|Ścieżka względna|Ścieżki bezwzględne|
|-------------|-------------|
|/ABC/DEF/Input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/Input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/Input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Użyj lokalnego uruchomienia z programu Visual Studio

Narzędzia Data Lake Tools dla programu Visual Studio zapewnia obsługę lokalnej — Uruchom U-SQL w programie Visual Studio. Za pomocą tej funkcji, można:

- Uruchom skrypt U-SQL lokalnie, wraz z zestawami języka C#.
- Debugowanie zestawu języka C# lokalnie.
- Tworzenie, wyświetlanie i usuwanie katalogów U-SQL (lokalnych baz danych, zestawy, schematy i tabele) z poziomu Eksploratora serwera. Lokalny katalog można również znaleźć również z Eksploratora serwera.

    ![Narzędzia Data Lake Tools dla katalogu lokalnego lokalnego uruchomienia programu Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Data Lake Tools Instalator tworzy folder C:\LocalRunRoot ma być używany jako domyślny folder główny danych. Równoległość lokalnego uruchomienia domyślny to 1.

### <a name="to-configure-local-run-in-visual-studio"></a>Aby skonfigurować przebiegu lokalnego w programie Visual Studio

1. Otwórz program Visual Studio.
2. Otwórz **Eksploratora serwera**.
3. Rozwiń węzeł **Azure** > **usługi Data Lake Analytics**.
4. Kliknij przycisk **usługi Data Lake** menu, a następnie kliknij przycisk **opcje i ustawienia**.
5. W drzewie po lewej stronie rozwiń **usługi Azure Data Lake**, a następnie rozwiń węzeł **ogólne**.

    ![Narzędzia Data Lake Tools dla programu Visual Studio Uruchom lokalny Konfigurowanie ustawień](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Projektu programu Visual Studio U-SQL jest wymagana do wykonania lokalnego uruchamiania. Ta część różni się od uruchamiania skryptów U-SQL na platformie Azure.

### <a name="to-run-a-u-sql-script-locally"></a>Aby uruchomić skrypt U-SQL lokalnie
1. W programie Visual Studio Otwórz projekt U-SQL.   
2. Kliknij prawym przyciskiem myszy skrypt U-SQL w Eksploratorze rozwiązań, a następnie kliknij przycisk **Prześlij skrypt**.
3. Wybierz **(Local)** jako konta usługi Analytics, aby uruchomić skrypt lokalnie.
Możesz również kliknąć **(Local)** konta w górnej części okna Skrypt, a następnie kliknij przycisk **przesyłania** (lub użyj klawiszy Ctrl + F5 skrót klawiaturowy).

    ![Narzędzia Data Lake Tools dla Visual Studio lokalnego uruchomienia przesyłania zadań](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Debugowanie skryptów i zestawów języka C# lokalnie

Można debugować zestawy języka C# bez przesyłania i rejestrowania ich do Azure Data Lake Analytics usługi. Można ustawić punkty przerwania w kodzie pliku oraz w projekcie języka C#, do którego się odwołujesz.

#### <a name="to-debug-local-code-in-code-behind-file"></a>Aby debugować kod lokalny w kodzie pliku

1. Ustaw punkty przerwania w kodzie pliku.
2. Naciśnij klawisz F5, aby debugować skrypt lokalnie.

> [!NOTE]
   > Poniższa procedura dotyczy tylko programu Visual Studio 2015. W starszych wersjach programu Visual Studio może być konieczne ręczne dodanie plików pdb.  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a>Aby debugować kod lokalny w występującym w odwołaniu projekcie C#

1. Utwórz projekt zestawu języka C# i skompiluj go, aby wygenerować wyjściowy plik dll.
2. Zarejestruj plik dll za pomocą instrukcji U-SQL:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Ustaw punkty przerwania w kodzie C#.
4. Naciśnij klawisz F5, aby debugować skrypt z wywoływanym C# biblioteki dll lokalnie.

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a>Użyj lokalnego uruchomienia z pakietu SDK Data Lake U-SQL

Poza uruchamianiem skryptów U-SQL lokalnie, używając programu Visual Studio, zestawu SDK usługi Azure Data Lake U-SQL służy do uruchamiania skryptów U-SQL lokalnie z wiersza polecenia i programowania interfejsów. Za pomocą tych opcji można skalować test lokalnego skryptu U-SQL.

Dowiedz się więcej o [zestawu SDK usługi Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Następne kroki

* Aby wyświetlić bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* Aby wyświetlić szczegóły zadania, zobacz [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).
* Aby użyć widoku wykonania wierzchołka, zobacz [użyć widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
