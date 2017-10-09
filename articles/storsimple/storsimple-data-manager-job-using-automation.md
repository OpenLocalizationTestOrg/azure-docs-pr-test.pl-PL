---
title: "aaaUse usługi Automatyzacja Azure tootrigger zadanie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Automatyzacja Azure służącą do wyzwalania zadania Menedżer StorSimple danych (w podglądzie prywatnym)"
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="b69be-103">Użyj usługi Automatyzacja Azure tootrigger zadania (podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="b69be-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="b69be-104">W tym artykule opisano sposób toouse usługi Automatyzacja Azure tootrigger zadania Menedżer StorSimple danych.</span><span class="sxs-lookup"><span data-stu-id="b69be-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b69be-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b69be-105">Prerequisites</span></span>

<span data-ttu-id="b69be-106">Przed rozpoczęciem upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="b69be-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="b69be-107">Zainstalowany program Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="b69be-107">Azure Powershell installed.</span></span> <span data-ttu-id="b69be-108">[Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b69be-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="b69be-109">Konfiguracja ustawień tooinitialize hello transformacji danych zadania (instrukcje tooobtain te ustawienia są uwzględnione w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="b69be-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="b69be-110">Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="b69be-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="b69be-111">Pobierz `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) plik z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="b69be-112">Pobierz `Get-ConfigurationParams.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="b69be-113">Pobierz `Trigger-DataTransformation-Job.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="b69be-114">Krok po kroku</span><span class="sxs-lookup"><span data-stu-id="b69be-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="b69be-115">Uzyskać uprawnienia w usłudze Azure Active Directory dla definicji zadania hello toorun hello automatyzacji zadań</span><span class="sxs-lookup"><span data-stu-id="b69be-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="b69be-116">tooretrieve hello parametry konfiguracji usługi Active Directory, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b69be-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="b69be-117">Otwórz program Windows PowerShell w komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b69be-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="b69be-118">Upewnij się, że [programu Azure PowerShell](https://azure.microsoft.com/downloads/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="b69be-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="b69be-119">Uruchom hello `Get-ConfigurationParams.ps1` skryptu (w folderze hello pobrane powyżej).</span><span class="sxs-lookup"><span data-stu-id="b69be-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="b69be-120">Wpisz następujące polecenie w oknie programu PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="b69be-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="b69be-121">Witaj ActiveDirectoryKey to hasło, które można użyć później.</span><span class="sxs-lookup"><span data-stu-id="b69be-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="b69be-122">Wprowadź hasło wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b69be-122">Enter a password of your choice.</span></span> <span data-ttu-id="b69be-123">Nazwa aplikacji może być dowolnym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="b69be-123">AppName can be any string.</span></span>

2. <span data-ttu-id="b69be-124">Ten skrypt generuje hello następujące wartości, które mają być używane podczas wyzwalania elementu runbook automatyzacji hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="b69be-125">Zanotuj te wartości.</span><span class="sxs-lookup"><span data-stu-id="b69be-125">Make a note of these values.</span></span>

    - <span data-ttu-id="b69be-126">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="b69be-126">Client ID</span></span>
    - <span data-ttu-id="b69be-127">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="b69be-127">Tenant ID</span></span>
    - <span data-ttu-id="b69be-128">Kluczy Active Directory (taki sam, jak hello jedną wprowadzony powyżej)</span><span class="sxs-lookup"><span data-stu-id="b69be-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="b69be-129">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b69be-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="b69be-130">Konfigurowanie hello konta automatyzacji</span><span class="sxs-lookup"><span data-stu-id="b69be-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="b69be-131">Zaloguj się na tooAzure i otwórz konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="b69be-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="b69be-132">Kliknij przycisk **zasoby** kafelka tooopen hello Lista zasobów.</span><span class="sxs-lookup"><span data-stu-id="b69be-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="b69be-133">Kliknij przycisk **modułów** kafelka tooopen hello listy modułów.</span><span class="sxs-lookup"><span data-stu-id="b69be-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="b69be-134">Kliknij przycisk **+ Dodaj moduł** bloku modułu Dodaj przycisk i hello jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="b69be-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="b69be-136">Po wybraniu hello `DataTransformationApp.zip` plików z komputera lokalnego, kliknij **OK** tooimport hello modułu.</span><span class="sxs-lookup"><span data-stu-id="b69be-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="b69be-137">Automatyzacja Azure importuje konta tooyour modułu, umożliwia wyodrębnianie metadanych dotyczących hello modułu.</span><span class="sxs-lookup"><span data-stu-id="b69be-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="b69be-138">Ta operacja może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b69be-138">This operation may take a couple of minutes.</span></span>

   ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="b69be-140">Zostanie wyświetlone powiadomienie tego modułu hello jest wdrażany i kolejne powiadomienie po zakończeniu procesu hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="b69be-141">Możesz również sprawdzić stan hello **modułów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b69be-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="b69be-142">tooimport hello runbook, które wyzwala hello definicji zadania</span><span class="sxs-lookup"><span data-stu-id="b69be-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="b69be-143">Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="b69be-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="b69be-144">Kliknij przycisk **elementów Runbook** kafelka tooopen hello listy elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="b69be-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="b69be-145">Kliknij przycisk **+ Dodaj element runbook** , a następnie **importowanie istniejącego elementu runbook**.</span><span class="sxs-lookup"><span data-stu-id="b69be-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importuj istniejący element runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="b69be-147">Kliknij przycisk **pliku Runbook** i wybierz hello pliku tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b69be-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="b69be-148">Kliknij przycisk **Utwórz** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="b69be-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="b69be-149">liście hello elementów runbook dla konta automatyzacji hello pojawi się nowy element runbook Hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="b69be-150">Kliknij przycisk **wyzwalacza DataTransformation zadania** runbook, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="b69be-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="b69be-151">Kliknij przycisk **publikowania** , a następnie **tak** po wyświetleniu monitu o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="b69be-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="b69be-152">toorun hello elementu runbook:</span><span class="sxs-lookup"><span data-stu-id="b69be-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="b69be-153">Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="b69be-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="b69be-154">Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="b69be-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="b69be-155">Kliknij przycisk **wyzwalacza DataTransformation zadania**.</span><span class="sxs-lookup"><span data-stu-id="b69be-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="b69be-156">Kliknij przycisk **Start** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="b69be-156">Click **Start** toostart hello runbook.</span></span>

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="b69be-158">W hello **uruchomić elementu runbook** bloku, wprowadź wszystkie parametry hello.</span><span class="sxs-lookup"><span data-stu-id="b69be-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="b69be-159">Kliknij przycisk **OK** toosubmit hello transformacji danych zadania.</span><span class="sxs-lookup"><span data-stu-id="b69be-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="b69be-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b69be-161">Next steps</span></span>

<span data-ttu-id="b69be-162">[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="b69be-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
