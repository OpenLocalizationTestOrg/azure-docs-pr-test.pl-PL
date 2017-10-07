---
title: "aaaUse zestawu .NET SDK dla programu Microsoft Azure StorSimple Data zadań | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zestawu .NET SDK toolaunch Menedżer StorSimple danych zadania (podglądzie prywatnym)"
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
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="8a8ad-103">Użyj hello .net SDK tooinitiate transformacji danych (w podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="8a8ad-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="8a8ad-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8a8ad-104">Overview</span></span>

<span data-ttu-id="8a8ad-105">W tym artykule opisano sposób korzystania z funkcji przekształcania danych hello tootransform usługi Menedżer StorSimple danych hello danych urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="8a8ad-106">Hello przekształcone dane są następnie używane przez innych usług platformy Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="8a8ad-107">Artykuł Hello zawiera również toohelp wskazówki, Utwórz tooinitiate aplikacji przykładowej .NET konsoli zadania przekształcania danych i śledzenie go do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a8ad-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a8ad-108">Prerequisites</span></span>

<span data-ttu-id="8a8ad-109">Przed rozpoczęciem upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="8a8ad-110">System z programu Visual Studio 2012 2013, 2015 lub zainstalowany 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="8a8ad-111">Zainstalowany program Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-111">Azure Powershell installed.</span></span> <span data-ttu-id="8a8ad-112">[Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="8a8ad-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="8a8ad-113">Konfiguracja ustawień tooinitialize hello transformacji danych zadania (instrukcje tooobtain te ustawienia są uwzględnione w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="8a8ad-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="8a8ad-114">Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="8a8ad-115">Wszystkie wymagane hello biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-115">All hello required dlls.</span></span> <span data-ttu-id="8a8ad-116">Pobierz te biblioteki dll z hello [repozytorium GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="8a8ad-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="8a8ad-117">`Get-ConfigurationParams.ps1`[skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="8a8ad-118">Krok po kroku</span><span class="sxs-lookup"><span data-stu-id="8a8ad-118">Step-by-step</span></span>

<span data-ttu-id="8a8ad-119">Wykonaj następujące kroki toouse .NET toolaunch zadania przekształcania danych hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="8a8ad-120">Parametry konfiguracji hello tooretrieve, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="8a8ad-121">Pobierz hello `Get-ConfigurationParams.ps1` ze skryptu repozytorium github hello w `C:\DataTransformation` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="8a8ad-122">Uruchom hello `Get-ConfigurationParams.ps1` skryptu z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="8a8ad-123">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="8a8ad-124">Dowolne wartości dla hello można przekazać ActiveDirectoryKey i AppName.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="8a8ad-125">Ten skrypt generuje hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="8a8ad-126">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8a8ad-126">Client ID</span></span>
    * <span data-ttu-id="8a8ad-127">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="8a8ad-127">Tenant ID</span></span>
    * <span data-ttu-id="8a8ad-128">Kluczy Active Directory (taki sam, jak hello jedną wprowadzony powyżej)</span><span class="sxs-lookup"><span data-stu-id="8a8ad-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="8a8ad-129">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8a8ad-129">Subscription ID</span></span>

3. <span data-ttu-id="8a8ad-130">Za pomocą programu Visual Studio 2012, 2013 lub 2015, Utwórz aplikację konsolową C# .NET.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="8a8ad-131">Uruchom **programu Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="8a8ad-132">Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="8a8ad-133">Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="8a8ad-134">Wybierz **aplikacji konsoli** z hello listy typów projektu na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="8a8ad-135">Wprowadź **DataTransformationApp** dla hello **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="8a8ad-136">Wybierz **C:\DataTransformation** dla hello **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="8a8ad-137">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="8a8ad-138">Teraz Dodaj wszystkie biblioteki dll w hello [biblioteki dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder jako **odwołania** w projekcie hello, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="8a8ad-139">pliki dll hello toodownload, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="8a8ad-140">W programie Visual Studio Przejdź zbyt**Widok > Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="8a8ad-141">Kliknij przycisk toohello Strzałka hello projektu aplikacji przekształcania danych w lewo.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="8a8ad-142">Kliknij przycisk **odwołania** , a następnie kliknij prawym przyciskiem myszy zbyt**Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="8a8ad-143">Przeglądaj toohello lokalizację folderu pakietów hello, wybierz wszystkie hello biblioteki dll i kliknij przycisk **Dodaj**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="8a8ad-144">Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="8a8ad-145">Witaj następującego kodu inicjuje wystąpienia zadania przekształcania danych hello.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="8a8ad-146">Dodaj ją w hello **metody Main**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="8a8ad-147">Zastąp hello wartości parametrów konfiguracji uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="8a8ad-148">Podłącz wartości hello **Nazwa grupy zasobów** i **Nazwa zasobu danych hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="8a8ad-149">Witaj **Nazwa grupy zasobów** jest hello, który obsługuje hello hybrydowego danych zasobów, na które hello skonfigurowano definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="8a8ad-150">Określ hello uruchomienia parametrów, o których hello definicji zadania wymaga toobe</span><span class="sxs-lookup"><span data-stu-id="8a8ad-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="8a8ad-151">(LUB)</span><span class="sxs-lookup"><span data-stu-id="8a8ad-151">(OR)</span></span>

    <span data-ttu-id="8a8ad-152">Jeśli parametrów definicji zadania hello toochange w czasie wykonywania, a następnie dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="8a8ad-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="8a8ad-153">Po zainicjowaniu hello Dodaj hello następującego kodu tootrigger zadania przekształcania danych na powitania definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="8a8ad-154">Podłącz odpowiednie hello **Nazwa definicji zadania**.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="8a8ad-155">Tego zadania operacji przekazywania plików hello dopasowywane w katalogu głównym hello na powitania StorSimple woluminu toohello określonego kontenera.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="8a8ad-156">Po przekazaniu pliku w kolejce hello upuszczeniu wiadomości (w hello tego samego konta magazynu ma być kontenerem hello) z hello takie same nazwy jako hello definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="8a8ad-157">Ten komunikat może służyć jako tooinitiate wyzwalacza, wszystkie dalsze przetwarzanie hello pliku.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="8a8ad-158">Po wyzwoleniu zadania hello Dodaj hello następujące zadania hello tootrack kod zakończenia.</span><span class="sxs-lookup"><span data-stu-id="8a8ad-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="8a8ad-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a8ad-159">Next steps</span></span>

<span data-ttu-id="8a8ad-160">[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="8a8ad-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
