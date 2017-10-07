---
title: 'Azure Data Lake Tools: Uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak debugować narzędzi toouse Azure Data Lake Tools dla Visual Studio Code toolocal wykonywania i lokalnych."
Keywords: "VScode, usługi Azure Data Lake Tools, lokalnego uruchamiania lokalnego debugowania, debugowania lokalnego pliku magazynu w wersji zapoznawczej, Przekaż toostorage ścieżki"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące wymagania wstępne w miejscu, przed rozpoczęciem wykonywania tych procedur hello:
- Usługi Azure Data Lake narzędzie dla kodu programu Visual Studio. Aby uzyskać instrukcje, zobacz [narzędzi użycia usługi Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# dla programu Visual Studio Code (jeśli ma lokalnego debugowania tooperform U-SQL).

   ![Zainstaluj C# w narzędzi Data Lake Tools dla programu Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Witaj przebiegu lokalnego skryptu U-SQL i funkcji debugowania aktualnie obsługują tylko użytkownicy systemu Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Konfigurowanie lokalnego środowiska uruchamiania hello U-SQL

1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Pobierz zależności LocalRun** toodownload hello pakietów.  

   ![Pobieranie hello ADL LocalRun zależności pakietów](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Zlokalizuj pakiety zależności hello ze ścieżki hello pokazano hello **dane wyjściowe** okienku, a następnie zainstaluj BuildTools i Win10SDK 10240. Oto przykład ścieżki:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Zlokalizuj hello zależności pakietów](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, postępuj zgodnie z instrukcjami kreatora hello.   

  ![Zainstaluj BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240 postępuj zgodnie z instrukcjami kreatora hello.  

  ![Zainstaluj Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Ustawienie zmiennej środowiskowej hello. Zestaw hello **SCOPE_CPP_SDK** zmiennej środowiskowej:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Uruchom ponownie się upewnić, że ustawień zmiennych środowiskowych hello wprowadzone toomake hello systemu operacyjnego.  

   ![Upewnij się, że zmienna środowiskowa SCOPE_CPP_SDK hello jest zainstalowany](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Uruchom usługę wykonywania lokalne powitania i przesyłanie konta lokalnego zadanie tooa hello U-SQL 
Powitania po raz pierwszy użytkownik, jest monitem toodownload hello ADL: Pobierz LocalRun zależności pakietów, jeśli nie są już zainstalowane.
1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Uruchom usługę lokalnego uruchamiania**.
2. Wybierz **Akceptuj** tooaccept hello postanowienia licencyjne dotyczące oprogramowania firmy Microsoft dla powitania po raz pierwszy. 

   ![Zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. zostanie otwarta konsola cmd Hello. Dla użytkowników po raz pierwszy, należy tooenter **3**, a następnie zlokalizuj hello ścieżkę folderu lokalnego dla danych wejściowych i wyjściowych. Inne opcje można użyć wartości domyślnych hello. 

   ![Narzędzia Data Lake Tools dla Visual Studio Code lokalnego uruchamiania cmd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, wprowadź **ADL: Prześlij zadanie**, a następnie wybierz **lokalnego** konta lokalnego zadanie tooyour toosubmit hello.

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz lokalnego](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Po przesłaniu zadania hello można wyświetlić szczegóły przesłanie hello. przesłanie hello tooview szczegółów wybierz **jobUrl** w hello **dane wyjściowe** okna. Można również wyświetlić stan przesyłania zadania hello hello cmd konsoli. Wprowadź **7** w konsoli cmd hello Chcąc tooknow więcej szczegółów zadania.

   ![Data Lake Tools dla Visual Studio Code lokalnego uruchamiania wyjścia](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![narzędzi Data Lake Tools dla Visual Studio Code lokalnych cmd stan uruchomienia](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Uruchom lokalny debugowania dla zadania skryptu U-SQL hello  
Powitania po raz pierwszy użytkownik, jest monitem toodownload hello ADL: Pobierz LocalRun zależności pakietów, jeśli nie są już zainstalowane.
  
1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Uruchom usługę lokalnego uruchamiania**. zostanie otwarta konsola cmd Hello. Upewnij się, że hello **DataRoot** jest ustawiona.
3. Ustaw punkt przerwania w Twojej C# związane z kodem.
4. W Edytorze skryptów hello wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia konsoli, a następnie wprowadź **debugowania lokalnego** toostart usługi debugowania lokalnego.

![Narzędzia Data Lake Tools dla Visual Studio Code wyniku lokalnego debugowania](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Następne kroki
- Używanie usługi Azure Data Lake Tools dla Visual Studio Code, zobacz [narzędzi użycia usługi Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Do uzyskania wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Witaj informacje o tworzeniu zestawów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).
