---
title: "Używanie automatyzacji Azure do wyzwalania zadania za | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Automatyzacja Azure służącą do wyzwalania zadania Menedżer StorSimple danych (w podglądzie prywatnym)"
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="2d37c-103">Używanie automatyzacji Azure do wyzwalania zadania (podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="2d37c-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="2d37c-104">W tym artykule opisano, jak uruchomić zadanie Menedżer StorSimple danych przy użyciu usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="2d37c-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d37c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2d37c-105">Prerequisites</span></span>

<span data-ttu-id="2d37c-106">Przed rozpoczęciem upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="2d37c-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="2d37c-107">Zainstalowany program Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="2d37c-107">Azure Powershell installed.</span></span> <span data-ttu-id="2d37c-108">[Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="2d37c-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="2d37c-109">Ustawienia konfiguracji w celu zainicjowania zadania przekształcania danych (instrukcjami, aby uzyskać te ustawienia są uwzględnione w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="2d37c-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="2d37c-110">Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d37c-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="2d37c-111">Pobierz `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) plik z repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="2d37c-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="2d37c-112">Pobierz `Get-ConfigurationParams.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) z repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="2d37c-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="2d37c-113">Pobierz `Trigger-DataTransformation-Job.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) z repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="2d37c-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="2d37c-114">Krok po kroku</span><span class="sxs-lookup"><span data-stu-id="2d37c-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="2d37c-115">Uprawnienia usługi Azure Active Directory dla definicji zadania uruchomienie zadania automatyzacji</span><span class="sxs-lookup"><span data-stu-id="2d37c-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="2d37c-116">Aby pobrać parametry konfiguracji usługi Active Directory, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2d37c-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="2d37c-117">Otwórz program Windows PowerShell w komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2d37c-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="2d37c-118">Upewnij się, że [programu Azure PowerShell](https://azure.microsoft.com/downloads/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="2d37c-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="2d37c-119">Uruchom `Get-ConfigurationParams.ps1` skryptu (w folderze pobrane powyżej).</span><span class="sxs-lookup"><span data-stu-id="2d37c-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="2d37c-120">W oknie programu PowerShell, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2d37c-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="2d37c-121">ActiveDirectoryKey to hasło, które można użyć później.</span><span class="sxs-lookup"><span data-stu-id="2d37c-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="2d37c-122">Wprowadź hasło wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d37c-122">Enter a password of your choice.</span></span> <span data-ttu-id="2d37c-123">Nazwa aplikacji może być dowolnym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="2d37c-123">AppName can be any string.</span></span>

2. <span data-ttu-id="2d37c-124">Ten skrypt generuje następujące wartości, które mają być używane podczas wyzwalania elementu runbook automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="2d37c-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="2d37c-125">Zanotuj te wartości.</span><span class="sxs-lookup"><span data-stu-id="2d37c-125">Make a note of these values.</span></span>

    - <span data-ttu-id="2d37c-126">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="2d37c-126">Client ID</span></span>
    - <span data-ttu-id="2d37c-127">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="2d37c-127">Tenant ID</span></span>
    - <span data-ttu-id="2d37c-128">Kluczy Active Directory (tak samo, jak to objęte powyżej)</span><span class="sxs-lookup"><span data-stu-id="2d37c-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="2d37c-129">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2d37c-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="2d37c-130">Skonfiguruj konto automatyzacji</span><span class="sxs-lookup"><span data-stu-id="2d37c-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="2d37c-131">Zaloguj się do platformy Azure i otwórz konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="2d37c-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="2d37c-132">Kliknij przycisk **zasoby** Kafelek, aby otworzyć listę zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d37c-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="2d37c-133">Kliknij przycisk **modułów** Kafelek, aby otworzyć listę modułów.</span><span class="sxs-lookup"><span data-stu-id="2d37c-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="2d37c-134">Kliknij przycisk **+ Dodaj moduł** przycisk i Dodaj blok modułu jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="2d37c-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="2d37c-136">Po wybraniu `DataTransformationApp.zip` plików z komputera lokalnego, kliknij **OK** zaimportować modułu.</span><span class="sxs-lookup"><span data-stu-id="2d37c-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="2d37c-137">Automatyzacja Azure importuje moduł do swojego konta, umożliwia wyodrębnianie metadanych dotyczących modułu.</span><span class="sxs-lookup"><span data-stu-id="2d37c-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="2d37c-138">Ta operacja może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="2d37c-138">This operation may take a couple of minutes.</span></span>

   ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="2d37c-140">Pojawi się powiadomienie jest wdrażany modułu i kolejne powiadomienie po zakończeniu procesu.</span><span class="sxs-lookup"><span data-stu-id="2d37c-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="2d37c-141">Można również sprawdzić stan **modułów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="2d37c-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="2d37c-142">Aby zaimportować element runbook, który wyzwala definicji zadania</span><span class="sxs-lookup"><span data-stu-id="2d37c-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="2d37c-143">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="2d37c-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="2d37c-144">Kliknij przycisk **Runbook** Kafelek, aby otworzyć listę elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="2d37c-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="2d37c-145">Kliknij przycisk **+ Dodaj element runbook** , a następnie **importowanie istniejącego elementu runbook**.</span><span class="sxs-lookup"><span data-stu-id="2d37c-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importuj istniejący element runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="2d37c-147">Kliknij przycisk **pliku Runbook** i wybierz plik do zaimportowania `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="2d37c-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="2d37c-148">Kliknij przycisk **Utwórz** można zaimportować elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="2d37c-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="2d37c-149">Nowy element runbook zostanie wyświetlony na liście elementów runbook dla konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="2d37c-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="2d37c-150">Kliknij przycisk **wyzwalacza DataTransformation zadania** runbook, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="2d37c-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="2d37c-151">Kliknij przycisk **publikowania** , a następnie **tak** po wyświetleniu monitu o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="2d37c-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="2d37c-152">Aby uruchomić element runbook:</span><span class="sxs-lookup"><span data-stu-id="2d37c-152">To run the runbook:</span></span>
1. <span data-ttu-id="2d37c-153">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="2d37c-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="2d37c-154">Kliknij kafelek **Elementy runbook**, aby otworzyć listę elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="2d37c-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="2d37c-155">Kliknij przycisk **wyzwalacza DataTransformation zadania**.</span><span class="sxs-lookup"><span data-stu-id="2d37c-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="2d37c-156">Kliknij pozycję **Uruchom**, aby uruchomić element Runbook.</span><span class="sxs-lookup"><span data-stu-id="2d37c-156">Click **Start** to start the runbook.</span></span>

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="2d37c-158">W **uruchomić elementu runbook** bloku, wprowadź wszystkie parametry.</span><span class="sxs-lookup"><span data-stu-id="2d37c-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="2d37c-159">Kliknij przycisk **OK** można przesłać zadania przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="2d37c-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="2d37c-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d37c-161">Next steps</span></span>

<span data-ttu-id="2d37c-162">[Użyj Menedżera danych StorSimple interfejsu użytkownika Służącego do przekształcenia danych](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2d37c-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>