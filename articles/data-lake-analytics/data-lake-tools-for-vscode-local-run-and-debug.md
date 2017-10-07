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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="16585-104">Uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16585-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16585-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16585-105">Prerequisites</span></span>
<span data-ttu-id="16585-106">Upewnij się, że masz następujące wymagania wstępne w miejscu, przed rozpoczęciem wykonywania tych procedur hello:</span><span class="sxs-lookup"><span data-stu-id="16585-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="16585-107">Usługi Azure Data Lake narzędzie dla kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16585-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="16585-108">Aby uzyskać instrukcje, zobacz [narzędzi użycia usługi Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="16585-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="16585-109">C# dla programu Visual Studio Code (jeśli ma lokalnego debugowania tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="16585-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Zainstaluj C# w narzędzi Data Lake Tools dla programu Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="16585-111">Witaj przebiegu lokalnego skryptu U-SQL i funkcji debugowania aktualnie obsługują tylko użytkownicy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="16585-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="16585-112">Konfigurowanie lokalnego środowiska uruchamiania hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="16585-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="16585-113">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Pobierz zależności LocalRun** toodownload hello pakietów.</span><span class="sxs-lookup"><span data-stu-id="16585-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Pobieranie hello ADL LocalRun zależności pakietów](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="16585-115">Zlokalizuj pakiety zależności hello ze ścieżki hello pokazano hello **dane wyjściowe** okienku, a następnie zainstaluj BuildTools i Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="16585-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="16585-116">Oto przykład ścieżki:</span><span class="sxs-lookup"><span data-stu-id="16585-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="16585-117">![Zlokalizuj hello zależności pakietów](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="16585-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="16585-118">a.</span><span class="sxs-lookup"><span data-stu-id="16585-118">a.</span></span> <span data-ttu-id="16585-119">tooinstall BuildTools, postępuj zgodnie z instrukcjami kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="16585-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Zainstaluj BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="16585-121">b.</span><span class="sxs-lookup"><span data-stu-id="16585-121">b.</span></span> <span data-ttu-id="16585-122">tooinstall Win10SDK 10240 postępuj zgodnie z instrukcjami kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="16585-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Zainstaluj Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="16585-124">Ustawienie zmiennej środowiskowej hello.</span><span class="sxs-lookup"><span data-stu-id="16585-124">Set up hello environment variable.</span></span> <span data-ttu-id="16585-125">Zestaw hello **SCOPE_CPP_SDK** zmiennej środowiskowej:</span><span class="sxs-lookup"><span data-stu-id="16585-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="16585-126">Uruchom ponownie się upewnić, że ustawień zmiennych środowiskowych hello wprowadzone toomake hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="16585-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Upewnij się, że zmienna środowiskowa SCOPE_CPP_SDK hello jest zainstalowany](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="16585-128">Uruchom usługę wykonywania lokalne powitania i przesyłanie konta lokalnego zadanie tooa hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="16585-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="16585-129">Powitania po raz pierwszy użytkownik, jest monitem toodownload hello ADL: Pobierz LocalRun zależności pakietów, jeśli nie są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="16585-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="16585-130">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Uruchom usługę lokalnego uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="16585-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="16585-131">Wybierz **Akceptuj** tooaccept hello postanowienia licencyjne dotyczące oprogramowania firmy Microsoft dla powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="16585-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="16585-133">zostanie otwarta konsola cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="16585-133">hello cmd console opens.</span></span> <span data-ttu-id="16585-134">Dla użytkowników po raz pierwszy, należy tooenter **3**, a następnie zlokalizuj hello ścieżkę folderu lokalnego dla danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="16585-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="16585-135">Inne opcje można użyć wartości domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="16585-135">For other options, you can use hello default values.</span></span> 

   ![Narzędzia Data Lake Tools dla Visual Studio Code lokalnego uruchamiania cmd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="16585-137">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, wprowadź **ADL: Prześlij zadanie**, a następnie wybierz **lokalnego** konta lokalnego zadanie tooyour toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="16585-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz lokalnego](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="16585-139">Po przesłaniu zadania hello można wyświetlić szczegóły przesłanie hello.</span><span class="sxs-lookup"><span data-stu-id="16585-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="16585-140">przesłanie hello tooview szczegółów wybierz **jobUrl** w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="16585-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="16585-141">Można również wyświetlić stan przesyłania zadania hello hello cmd konsoli.</span><span class="sxs-lookup"><span data-stu-id="16585-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="16585-142">Wprowadź **7** w konsoli cmd hello Chcąc tooknow więcej szczegółów zadania.</span><span class="sxs-lookup"><span data-stu-id="16585-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="16585-143">![Data Lake Tools dla Visual Studio Code lokalnego uruchamiania wyjścia](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![narzędzi Data Lake Tools dla Visual Studio Code lokalnych cmd stan uruchomienia](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="16585-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="16585-144">Uruchom lokalny debugowania dla zadania skryptu U-SQL hello</span><span class="sxs-lookup"><span data-stu-id="16585-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="16585-145">Powitania po raz pierwszy użytkownik, jest monitem toodownload hello ADL: Pobierz LocalRun zależności pakietów, jeśli nie są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="16585-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="16585-146">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety, a następnie wprowadź **ADL: Uruchom usługę lokalnego uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="16585-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="16585-147">zostanie otwarta konsola cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="16585-147">hello cmd console opens.</span></span> <span data-ttu-id="16585-148">Upewnij się, że hello **DataRoot** jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="16585-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="16585-149">Ustaw punkt przerwania w Twojej C# związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="16585-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="16585-150">W Edytorze skryptów hello wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia konsoli, a następnie wprowadź **debugowania lokalnego** toostart usługi debugowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="16585-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Narzędzia Data Lake Tools dla Visual Studio Code wyniku lokalnego debugowania](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="16585-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16585-152">Next steps</span></span>
- <span data-ttu-id="16585-153">Używanie usługi Azure Data Lake Tools dla Visual Studio Code, zobacz [narzędzi użycia usługi Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="16585-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="16585-154">Do uzyskania wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16585-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="16585-155">Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16585-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="16585-156">Witaj informacje o tworzeniu zestawów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="16585-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
