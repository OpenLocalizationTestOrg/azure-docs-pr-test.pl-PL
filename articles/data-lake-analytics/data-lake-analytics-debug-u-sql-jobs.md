---
title: zadania aaaDebug U-SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodebug U-SQL nie powiodło się wierzchołków przy użyciu programu Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Debugowanie zdefiniowane przez użytkownika kodu C#, dla zadań U-SQL nie powiodło się

U-SQL zapewnia modelu rozszerzalności przy użyciu języka C#, co może zapisywać Twoje kodu tooadd funkcje, takie jak niestandardowe ekstraktory lub reduktor. toolearn więcej, zobacz [Podręcznik programowania U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). W praktyce dowolny kod może być konieczne debugowania i systemy danych big data mogą dostarczać tylko ograniczone środowiska uruchomieniowego debugowania informacje, takie jak pliki dziennika.

Azure Data Lake Tools dla programu Visual Studio udostępnia funkcję **nie można debugować wierzchołków**, co umożliwia sklonować zadanie zakończone niepowodzeniem z komputera lokalnego tooyour chmury hello do debugowania. klonowanie lokalne powitania przechwytuje środowiska chmury całego hello, w tym wszystkie dane wejściowe i kod użytkownika.

Witaj poniżej film wideo przedstawia nie powiodło się wierzchołków debugowania w Azure Data Lake Tools dla programu Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Program Visual Studio wymaga powitania po dwóch aktualizacji, jeśli nie są już zainstalowane: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) i [Universal C środowiska uruchomieniowego systemu Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Pobieranie nie powiodło się wierzchołków toolocal maszyny

Po otwarciu zadanie zakończone niepowodzeniem w Azure Data Lake Tools dla programu Visual Studio jest wyświetlany żółty pasek alertów o szczegółowe komunikaty o błędach na karcie błąd hello.

1. Kliknij przycisk **Pobierz** toodownload hello wszystkich wymaganych zasobów i strumienie wejściowe. Jeśli pobieranie hello nie ukończone, kliknij przycisk **ponów**.

2. Kliknij przycisk **Otwórz** po ukończeniu pobierania hello toogenerate środowisku debugowania lokalnego. Nowe wystąpienie programu Visual Studio z rozwiązaniem do debugowania jest automatycznie utworzony i otwarty.

![Azure Data Lake Analytics U-SQL debugowania programu visual studio pobierania wierzchołków](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Zadania mogą obejmować źródła plików z kodem lub zarejestrowanych zestawy, a te dwa typy mają różne scenariusze debugowania.

- [Zadanie zakończone niepowodzeniem z kodem debugowania](#debug-job-failed-with-code-behind)
- [Debugowanie zakończonego niepowodzeniem zadania przy użyciu zestawów](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Debugowanie nie powiodło się z kodem — zadanie

Jeśli zadanie U-SQL zakończy się niepowodzeniem, a hello zadania obejmują kod użytkownika (zwykle o nazwie `Script.usql.cs` projektu U-SQL), aby kod źródłowy jest importowany do hello debugowanie rozwiązania.  Z tego miejsca można użyć hello Visual Studio debugowania narzędzi (czujki, zmienne, itp.) tootroubleshoot hello problem.

> [!NOTE]
> Przed debugowania, należy się toocheck **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków hello (**Ctrl + Alt + E**).

![Ustawienia programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Naciśnij klawisz **F5** toorun hello CodeBehind kodu. Zostanie on uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek.

2. Otwórz hello `ADLTool_Codebehind.usql.cs` pliku i ustaw punkty przerwania, naciśnij klawisz **F5** toodebug hello kodu krok po kroku.

    ![Wyjątek debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Zadanie nie powiodło się z zestawami debugowania

Użycie zestawów zarejestrowanych za pomocą skryptu U-SQL, hello systemu nie można pobrać kodu źródłowego hello automatycznie. W takim przypadku ręcznie dodać zestawy hello źródła kodu pliki toohello rozwiązania.

### <a name="configure-hello-solution"></a>Konfigurowanie rozwiązania hello

1. Kliknij prawym przyciskiem myszy **rozwiązania "VertexDebug" > Dodaj > istniejący projekt...**  toofind Witaj zestawy kodu źródłowego i Dodaj toohello projektu hello debugowanie rozwiązania.

    ![Dodawanie usługi Azure Data Lake Analytics U-SQL debugowania projektu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Kliknij prawym przyciskiem myszy **LocalVertexHost > właściwości** w hello rozwiązania i skopiuj hello **katalog roboczy** ścieżki.

3. Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > właściwości**, wybierz pozycję hello **kompilacji** po lewej stronie, a następnie wklej skopiowany hello ścieżkę jako **wyjściowy > Ścieżka wyjściowa**.

    ![Ścieżka pliku pdb zestawu Azure Data Lake Analytics U-SQL debugowania](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Naciśnij klawisz **Ctrl + Alt + E**, sprawdź **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków.

### <a name="start-debug"></a>Uruchom debugowania

1. Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > odbudować** toooutput .pdb, pliki toohello `LocalVertexHost` katalog roboczy.

2. Naciśnij klawisz **F5** i hello projekt zostanie uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek. Może pojawić się następujące ostrzeżenie można zignorować hello. Może potrwać tooa minuty tooget toohello debugowania ekranu.

    ![Ostrzeżenie programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Otwórz kod źródłowy i ustaw punkty przerwania, naciśnij klawisz **F5** toodebug hello kodu krok po kroku.

Umożliwia także hello Visual Studio debugowania narzędzi (czujki, zmienne, itp.) tootroubleshoot hello problem.

> [!NOTE]
> Odbuduj projekt kodu źródłowego zestawu hello każdorazowo po zmodyfikowaniu hello kodu toogenerate zaktualizowane .pdb, pliki.

Po debugowaniu, jeśli hello projektu zostało ukończone pomyślnie hello okno danych wyjściowych zawiera następujące wiadomość hello:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debugowania powiodło się](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Prześlij ponownie hello zadania

Po zakończeniu debugowania Prześlij ponownie hello zadania nie powiodło się.

1. W przypadku zadań z rozwiązaniami związane z kodem, skopiuj kod C# do pliku źródłowego związane z kodem hello (zazwyczaj `Script.usql.cs`).
2. Prac z zestawami Rejestrowanie zestawów .dll hello zaktualizowane w bazie danych ADLA:
    1. W Eksploratorze serwera lub Eksploratorze chmury, rozwiń węzeł hello **konta ADLA > baz danych** węzła.
    2. Kliknij prawym przyciskiem myszy **zestawy** i Zarejestruj ponownie nowe zestawy dll z bazą danych ADLA hello: ![debugowania Azure Data Lake Analytics U-SQL Rejestrowanie zestawów](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Prześlij swoją pracę.

## <a name="next-steps"></a>Następne kroki

- [Podręcznik programowania U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Opracowywanie operatorów zdefiniowanych przez użytkownika U-SQL do zadania usługi Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
