---
title: "Korzystanie z zestawu SDK .NET dla programu Microsoft Azure StorSimple Data zadań | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użyć zestawu .NET SDK w celu uruchomienia zadania Menedżer StorSimple danych (w podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="c3e06-103">Użyj zestawu SDK programu .net zainicjować transformacji danych (w podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="c3e06-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="c3e06-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c3e06-104">Overview</span></span>

<span data-ttu-id="c3e06-105">W tym artykule opisano sposób korzystania z funkcji przekształcania danych w usłudze Menedżer StorSimple danych do przekształcania danych urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c3e06-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="c3e06-106">Przekształcone dane są następnie używane przez innych usług platformy Azure w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c3e06-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="c3e06-107">Artykuł ma również wskazówki ułatwiające tworzenie przykładowej aplikacji konsoli .NET zainicjować zadania przekształcania danych, a następnie ją Śledź ukończenia.</span><span class="sxs-lookup"><span data-stu-id="c3e06-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3e06-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c3e06-108">Prerequisites</span></span>

<span data-ttu-id="c3e06-109">Przed rozpoczęciem upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="c3e06-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="c3e06-110">System z programu Visual Studio 2012 2013, 2015 lub zainstalowany 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c3e06-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="c3e06-111">Zainstalowany program Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="c3e06-111">Azure Powershell installed.</span></span> <span data-ttu-id="c3e06-112">[Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="c3e06-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="c3e06-113">Ustawienia konfiguracji w celu zainicjowania zadania przekształcania danych (instrukcjami, aby uzyskać te ustawienia są uwzględnione w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="c3e06-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="c3e06-114">Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c3e06-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="c3e06-115">Wszystkie wymagane biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="c3e06-115">All the required dlls.</span></span> <span data-ttu-id="c3e06-116">Pobierz te biblioteki dll z [repozytorium GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="c3e06-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="c3e06-117">`Get-ConfigurationParams.ps1`[skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) z repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="c3e06-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="c3e06-118">Krok po kroku</span><span class="sxs-lookup"><span data-stu-id="c3e06-118">Step-by-step</span></span>

<span data-ttu-id="c3e06-119">Wykonaj poniższe kroki, aby użyć .NET w celu uruchomienia zadania przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="c3e06-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="c3e06-120">Aby pobrać parametry konfiguracji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c3e06-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="c3e06-121">Pobierz `Get-ConfigurationParams.ps1` ze skryptu repozytorium github w `C:\DataTransformation` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c3e06-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="c3e06-122">Uruchom `Get-ConfigurationParams.ps1` skryptu z repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="c3e06-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="c3e06-123">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c3e06-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="c3e06-124">Można przekazać wartości ActiveDirectoryKey i AppName.</span><span class="sxs-lookup"><span data-stu-id="c3e06-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="c3e06-125">Ten skrypt generuje następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c3e06-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="c3e06-126">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="c3e06-126">Client ID</span></span>
    * <span data-ttu-id="c3e06-127">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c3e06-127">Tenant ID</span></span>
    * <span data-ttu-id="c3e06-128">Kluczy Active Directory (tak samo, jak to objęte powyżej)</span><span class="sxs-lookup"><span data-stu-id="c3e06-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="c3e06-129">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c3e06-129">Subscription ID</span></span>

3. <span data-ttu-id="c3e06-130">Za pomocą programu Visual Studio 2012, 2013 lub 2015, Utwórz aplikację konsolową C# .NET.</span><span class="sxs-lookup"><span data-stu-id="c3e06-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="c3e06-131">Uruchom **programu Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="c3e06-132">Kliknij pozycję **Plik**, wskaż polecenie **Nowy** i kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="c3e06-133">Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="c3e06-134">Wybierz opcję **Aplikacja konsolowa** z listy typów projektów po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="c3e06-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="c3e06-135">Wprowadź **DataTransformationApp** dla **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="c3e06-136">Wybierz **C:\DataTransformation** dla **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="c3e06-137">Kliknij przycisk **OK**, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="c3e06-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="c3e06-138">Teraz Dodaj wszystkie biblioteki dll w [biblioteki dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder jako **odwołania** w projekcie, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c3e06-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="c3e06-139">Aby pobrać pliki dll, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c3e06-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="c3e06-140">W programie Visual Studio, przejdź do **Widok > Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="c3e06-141">Kliknij strzałkę w lewo projektu aplikacji przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="c3e06-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="c3e06-142">Kliknij przycisk **odwołania** , a następnie kliknij prawym przyciskiem myszy, aby **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="c3e06-143">Przejdź do lokalizacji folderu pakietów, wybierz wszystkie biblioteki dll i kliknij przycisk **Dodaj**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="c3e06-144">Dodaj następujące instrukcje **using** do pliku źródłowego (Program.cs) w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c3e06-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="c3e06-145">Poniższy kod inicjuje wystąpienie zadania przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="c3e06-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="c3e06-146">Dodaj ją w **metody Main**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-146">Add this in the **Main method**.</span></span> <span data-ttu-id="c3e06-147">Zastąp wartości parametrów konfiguracji uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c3e06-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="c3e06-148">Podłącz wartości **Nazwa grupy zasobów** i **Nazwa zasobu danych hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="c3e06-149">**Nazwa grupy zasobów** jest ten, który obsługuje hybrydowego zasobów danych, na którym skonfigurowano definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="c3e06-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="c3e06-150">Określ parametry, z których trzeba uruchomić definicji zadania</span><span class="sxs-lookup"><span data-stu-id="c3e06-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="c3e06-151">(LUB)</span><span class="sxs-lookup"><span data-stu-id="c3e06-151">(OR)</span></span>

    <span data-ttu-id="c3e06-152">Jeśli chcesz zmienić parametrów definicji zadania w czasie wykonywania, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="c3e06-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="c3e06-153">Po zainicjowaniu Dodaj następujący kod do wyzwalania zadania przekształcania danych w definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="c3e06-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="c3e06-154">Podłącz odpowiednie **Nazwa definicji zadania**.</span><span class="sxs-lookup"><span data-stu-id="c3e06-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="c3e06-155">To zadanie będzie przekazywać pasujących plików istnieje w katalogu głównym woluminu StorSimple do określonego kontenera.</span><span class="sxs-lookup"><span data-stu-id="c3e06-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="c3e06-156">Po przekazaniu pliku wiadomości zostało porzucone z taką samą nazwę jak definicji zadania w kolejce (w tym samym koncie magazynu jako kontener).</span><span class="sxs-lookup"><span data-stu-id="c3e06-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="c3e06-157">Ten komunikat może służyć jako wyzwalacz zainicjować dalszego przetwarzania pliku.</span><span class="sxs-lookup"><span data-stu-id="c3e06-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="c3e06-158">Po wyzwoleniu zadania Dodaj następujący kod, aby śledzić zadania do wykonania.</span><span class="sxs-lookup"><span data-stu-id="c3e06-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="c3e06-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3e06-159">Next steps</span></span>

<span data-ttu-id="c3e06-160">[Użyj Menedżera danych StorSimple interfejsu użytkownika Służącego do przekształcenia danych](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="c3e06-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
