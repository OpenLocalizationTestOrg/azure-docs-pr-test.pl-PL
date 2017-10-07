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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Użyj hello .net SDK tooinitiate transformacji danych (w podglądzie prywatnym)

## <a name="overview"></a>Omówienie

W tym artykule opisano sposób korzystania z funkcji przekształcania danych hello tootransform usługi Menedżer StorSimple danych hello danych urządzenia StorSimple. Hello przekształcone dane są następnie używane przez innych usług platformy Azure w chmurze hello. Artykuł Hello zawiera również toohelp wskazówki, Utwórz tooinitiate aplikacji przykładowej .NET konsoli zadania przekształcania danych i śledzenie go do ukończenia.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:
*   System z programu Visual Studio 2012 2013, 2015 lub zainstalowany 2017 r.
*   Zainstalowany program Azure Powershell. [Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Konfiguracja ustawień tooinitialize hello transformacji danych zadania (instrukcje tooobtain te ustawienia są uwzględnione w tym miejscu).
*   Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.
*   Wszystkie wymagane hello biblioteki dll. Pobierz te biblioteki dll z hello [repozytorium GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) z repozytorium github hello.

## <a name="step-by-step"></a>Krok po kroku

Wykonaj następujące kroki toouse .NET toolaunch zadania przekształcania danych hello.

1. Parametry konfiguracji hello tooretrieve, hello następujące kroki:
    1. Pobierz hello `Get-ConfigurationParams.ps1` ze skryptu repozytorium github hello w `C:\DataTransformation` lokalizacji.
    1. Uruchom hello `Get-ConfigurationParams.ps1` skryptu z repozytorium github hello. Wpisz następujące polecenie hello:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        Dowolne wartości dla hello można przekazać ActiveDirectoryKey i AppName.


2. Ten skrypt generuje hello następujące wartości:
    * Identyfikator klienta
    * Identyfikator dzierżawy
    * Kluczy Active Directory (taki sam, jak hello jedną wprowadzony powyżej)
    * Identyfikator subskrypcji

3. Za pomocą programu Visual Studio 2012, 2013 lub 2015, Utwórz aplikację konsolową C# .NET.

    1. Uruchom **programu Visual Studio 2012/2013/2015**.
    1. Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.
    2. Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**.
    3. Wybierz **aplikacji konsoli** z hello listy typów projektu na powitania prawo.
    4. Wprowadź **DataTransformationApp** dla hello **nazwa**.
    5. Wybierz **C:\DataTransformation** dla hello **lokalizacji**.
    6. Kliknij przycisk **OK** toocreate hello projektu.

4.  Teraz Dodaj wszystkie biblioteki dll w hello [biblioteki dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder jako **odwołania** w projekcie hello, który został utworzony. pliki dll hello toodownload, hello następujące:

    1. W programie Visual Studio Przejdź zbyt**Widok > Eksploratora rozwiązań**.
    1. Kliknij przycisk toohello Strzałka hello projektu aplikacji przekształcania danych w lewo. Kliknij przycisk **odwołania** , a następnie kliknij prawym przyciskiem myszy zbyt**Dodaj odwołanie**.
    2. Przeglądaj toohello lokalizację folderu pakietów hello, wybierz wszystkie hello biblioteki dll i kliknij przycisk **Dodaj**, a następnie kliknij przycisk **OK**.

5. Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Witaj następującego kodu inicjuje wystąpienia zadania przekształcania danych hello. Dodaj ją w hello **metody Main**. Zastąp hello wartości parametrów konfiguracji uzyskany wcześniej. Podłącz wartości hello **Nazwa grupy zasobów** i **Nazwa zasobu danych hybrydowego**. Witaj **Nazwa grupy zasobów** jest hello, który obsługuje hello hybrydowego danych zasobów, na które hello skonfigurowano definicji zadania.

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

7. Określ hello uruchomienia parametrów, o których hello definicji zadania wymaga toobe

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (LUB)

    Jeśli parametrów definicji zadania hello toochange w czasie wykonywania, a następnie dodaj hello następującego kodu:

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

8. Po zainicjowaniu hello Dodaj hello następującego kodu tootrigger zadania przekształcania danych na powitania definicji zadania. Podłącz odpowiednie hello **Nazwa definicji zadania**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Tego zadania operacji przekazywania plików hello dopasowywane w katalogu głównym hello na powitania StorSimple woluminu toohello określonego kontenera. Po przekazaniu pliku w kolejce hello upuszczeniu wiadomości (w hello tego samego konta magazynu ma być kontenerem hello) z hello takie same nazwy jako hello definicji zadania. Ten komunikat może służyć jako tooinitiate wyzwalacza, wszystkie dalsze przetwarzanie hello pliku.

10. Po wyzwoleniu zadania hello Dodaj hello następujące zadania hello tootrack kod zakończenia.

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


## <a name="next-steps"></a>Następne kroki

[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).
