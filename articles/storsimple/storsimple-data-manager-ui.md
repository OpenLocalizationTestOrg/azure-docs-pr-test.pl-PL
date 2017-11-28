---
title: "aaaMicrosoft interfejsu użytkownika Menedżera danych StorSimple Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse usługi Menedżer StorSimple danych interfejsu użytkownika (podglądzie prywatnym)"
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
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="06b13-103">Zarządzanie przy użyciu usługi Menedżer StorSimple danych hello interfejsu użytkownika (podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="06b13-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="06b13-104">W tym artykule opisano sposób korzystania hello transformacji danych tooperform interfejsu użytkownika Menedżera danych StorSimple na danych znajdujących się na powitania urządzeń z serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="06b13-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="06b13-105">Witaj przekształcone dane może następnie być zużyte przez innych usług Azure, takich jak usługi Azure Media Services, Azure HDInsight uczenie maszynowe Azure i usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="06b13-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="06b13-106">Za pomocą przekształcania danych StorSimple</span><span class="sxs-lookup"><span data-stu-id="06b13-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="06b13-107">Witaj StorSimple Data Manager jest hello zasobów, w którym można wdrożyć transformacji danych.</span><span class="sxs-lookup"><span data-stu-id="06b13-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="06b13-108">Hello usługi Data Transformation umożliwia przenoszenie danych z programu StorSimple lokalnymi urządzeniami tooblobs w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="06b13-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="06b13-109">W związku z tym w przepływie pracy należy toospecify hello szczegóły dotyczące danych urządzenia i hello StorSimple odsetek, które mają konta magazynu toohello toomove.</span><span class="sxs-lookup"><span data-stu-id="06b13-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="06b13-110">Utwórz usługę Menedżer StorSimple danych</span><span class="sxs-lookup"><span data-stu-id="06b13-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="06b13-111">Wykonaj następujące kroki toocreate usługi Menedżer StorSimple danych hello.</span><span class="sxs-lookup"><span data-stu-id="06b13-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="06b13-112">toocreate usługi Menedżer StorSimple danych, przejdź zbyt[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="06b13-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="06b13-113">Kliknij przycisk hello  **+**  ikony, jak i wyszukiwania StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="06b13-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="06b13-114">Kliknij opcję usługi Menedżer StorSimple danych, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="06b13-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="06b13-115">Po włączeniu subskrypcji do tworzenia tej usługi zostanie wyświetlony powitania po bloku.</span><span class="sxs-lookup"><span data-stu-id="06b13-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![Utwórz zasób menedżerów danych StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="06b13-117">Wprowadź dane wejściowe hello i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="06b13-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="06b13-118">Witaj określona lokalizacja powinna być hello jedną, która przechowuje kont magazynu i usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="06b13-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="06b13-119">Obecnie są obsługiwane tylko w regionach zachodnie stany USA i Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="06b13-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="06b13-120">W związku z tym Twojej usługi Menedżer StorSimple, usługa Data Manager i hello skojarzone konto magazynu powinny być w poprzednim hello obsługiwane regiony.</span><span class="sxs-lookup"><span data-stu-id="06b13-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="06b13-121">Trwa około minuty toocreate hello usługi.</span><span class="sxs-lookup"><span data-stu-id="06b13-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="06b13-122">Tworzenie definicji zadania przekształcania danych</span><span class="sxs-lookup"><span data-stu-id="06b13-122">Create a data transformation job definition</span></span>

<span data-ttu-id="06b13-123">W ramach usługi Menedżer StorSimple danych należy toocreate definicji zadania przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="06b13-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="06b13-124">Definicji zadania określa szczegóły hello dane, które planuje się do konta magazynu w hello formatu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="06b13-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="06b13-125">Wykonaj następujące kroki toocreate nowej definicji zadania przekształcania danych hello.</span><span class="sxs-lookup"><span data-stu-id="06b13-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="06b13-126">Przejdź toohello utworzoną usługę.</span><span class="sxs-lookup"><span data-stu-id="06b13-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="06b13-127">Kliknij przycisk **+ definicji zadania**.</span><span class="sxs-lookup"><span data-stu-id="06b13-127">Click **+ Job Definition**.</span></span>

    ![Kliknij pozycję + definicji zadania](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="06b13-129">Otwiera nowy blok definicji zadania Hello.</span><span class="sxs-lookup"><span data-stu-id="06b13-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="06b13-130">Nadaj nazwę definicja zadania, a następnie kliknij przycisk **źródła**.</span><span class="sxs-lookup"><span data-stu-id="06b13-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="06b13-131">W hello **Konfigurowanie źródła danych** bloku, określ szczegóły hello urządzenia StorSimple i hello dane.</span><span class="sxs-lookup"><span data-stu-id="06b13-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![Tworzenie definicji zadania](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="06b13-133">Ponieważ jest to nowa usługa Data Manager, są skonfigurowane nie repozytoria danych.</span><span class="sxs-lookup"><span data-stu-id="06b13-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="06b13-134">tooadd Menedżera StorSimple jako repozytorium danych, kliknij przycisk **Dodaj nowe** w hello danych repozytorium z listy rozwijanej, a następnie kliknij przycisk **Dodaj repozytorium danych**.</span><span class="sxs-lookup"><span data-stu-id="06b13-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="06b13-135">Wybierz **serii StorSimple 8000 Menedżera** jako repozytorium hello typu, a następnie wprowadź właściwości hello Twojej **Menedżer StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="06b13-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="06b13-136">Dla hello **identyfikator zasobu** pole, należy numer hello tooenter przed hello **:** w kluczu rejestracji hello Menedżera StorSimple.</span><span class="sxs-lookup"><span data-stu-id="06b13-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![Utwórz źródło danych](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="06b13-138">Kliknij przycisk **OK** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="06b13-138">Click **OK** when done.</span></span> <span data-ttu-id="06b13-139">Spowoduje to zapisanie danych repozytorium, a ten Menedżer StorSimple mogą być ponownie używane w innych definicje zadań bez konieczności ponownego wprowadzania tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="06b13-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="06b13-140">Trwa kilka sekund po kliknięciu **OK** dla hello tooshow Menedżer StorSimple się w hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="06b13-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="06b13-141">W hello **Konfigurowanie źródła danych** bloku, wprowadź nazwę urządzenia hello i hello nazwa woluminu, zawierający dane zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="06b13-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="06b13-142">W hello **filtru** podsekcji, wprowadź katalog główny hello zawierającego dane odsetek (w tym polu powinny rozpoczynać się od `\`).</span><span class="sxs-lookup"><span data-stu-id="06b13-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="06b13-143">Można również dodać wszystkie filtry plików.</span><span class="sxs-lookup"><span data-stu-id="06b13-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="06b13-144">Usługa przekształcania danych Hello działa na dane hello spoczywa się toohello Azure za pomocą migawki.</span><span class="sxs-lookup"><span data-stu-id="06b13-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="06b13-145">Podczas wykonywania tego zadania, można tootake kopii zapasowej każdorazowo to zadanie jest uruchamiane (toowork na najnowszych danych) lub toouse hello ostatniego istniejącej kopii zapasowej w chmurze hello (Jeśli pracujesz nad niektórych danych archiwalnych).</span><span class="sxs-lookup"><span data-stu-id="06b13-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![Nowe szczegóły źródła danych](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="06b13-147">Następnie ustawień obiektu docelowego hello muszą toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="06b13-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="06b13-148">Istnieją 2 typy elementów docelowych obsługiwanych — kont usługi Azure Storage i Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="06b13-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="06b13-149">Wybieranie kont magazynu tooput pliki do obiektów blob w tym kontem.</span><span class="sxs-lookup"><span data-stu-id="06b13-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="06b13-150">Wybierz konta usługi media services pliki tooput do zasobów na tym koncie.</span><span class="sxs-lookup"><span data-stu-id="06b13-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="06b13-151">Ponownie potrzebujemy tooadd repozytorium.</span><span class="sxs-lookup"><span data-stu-id="06b13-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="06b13-152">Z listy rozwijanej hello, wybierz **Dodaj nowe** , a następnie **skonfigurować ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="06b13-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Utwórz ujścia danych](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="06b13-154">W tym miejscu można wybrać typ hello ma tooadd i hello innych parametrów skojarzonych z repozytorium hello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="06b13-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="06b13-155">W obu przypadkach kolejki magazynu jest tworzony podczas hello zadanie jest uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="06b13-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="06b13-156">Jest ona wypełniana przy użyciu komunikatów dotyczących przekształconych obiektów blob, gdy będą gotowe.</span><span class="sxs-lookup"><span data-stu-id="06b13-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="06b13-157">Nazwa Hello tej kolejki jest hello taka sama jak nazwa hello hello definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="06b13-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="06b13-158">W przypadku wybrania **Media Services** jako typ repozytorium hello, następnie możesz też wprowadzić poświadczenia konta magazynu gdy kolejka hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="06b13-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![Nowe szczegóły ujścia danych](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="06b13-160">Po dodaniu repozytorium danych hello (która zajmuje kilka sekund), można znaleźć w listy rozwijanej hello w hello repozytorium hello **nazwa konta docelowego**.</span><span class="sxs-lookup"><span data-stu-id="06b13-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="06b13-161">Wybierz element docelowy hello, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="06b13-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="06b13-162">Kliknij przycisk **OK** definicji zadania hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="06b13-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="06b13-163">Definicja zadania jest teraz skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="06b13-163">Your job definition is now set up.</span></span> <span data-ttu-id="06b13-164">Można użyć tej definicji zadania wiele razy za pośrednictwem hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="06b13-164">You can use this job definition multiple times via hello UI.</span></span>

    ![Dodawanie nowej definicji zadania](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="06b13-166">Uruchom hello definicji zadania</span><span class="sxs-lookup"><span data-stu-id="06b13-166">Run hello job definition</span></span>

<span data-ttu-id="06b13-167">Jeśli potrzebne jest toomove dane z konta magazynu toohello StorSimple, który został określony w definicji zadania hello, konieczne będzie tooinvoke go.</span><span class="sxs-lookup"><span data-stu-id="06b13-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="06b13-168">Podczas zmieniania parametry hello każdorazowego wywołania zadania hello charakteryzuje się pewną elastycznością.</span><span class="sxs-lookup"><span data-stu-id="06b13-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="06b13-169">Witaj obejmuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="06b13-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="06b13-170">Wybierz usługę Menedżer StorSimple danych i przejść za**monitorowanie**.</span><span class="sxs-lookup"><span data-stu-id="06b13-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="06b13-171">Kliknij przycisk **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="06b13-171">Click **Run Now**.</span></span>

    ![Wyzwalacz definicji zadania](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="06b13-173">Wybierz hello definicji zadania, które mają toorun.</span><span class="sxs-lookup"><span data-stu-id="06b13-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="06b13-174">Kliknij przycisk **parametrów uruchomieniowych** toomodify wszystkie ustawienia, które mają toochange wykonywania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="06b13-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![Uruchom zadania, ustawienia](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="06b13-176">Kliknij przycisk **OK** , a następnie kliknij przycisk **Uruchom** toolaunch swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="06b13-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="06b13-177">toomonitor tego zadania, przejdź toohello **zadania** strony w Menedżera StorSimple danych.</span><span class="sxs-lookup"><span data-stu-id="06b13-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Lista zadań i stanu](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="06b13-179">W przypadku dodawania toomonitoring w hello **zadania** bloku można również wykrywać w kolejce magazynu hello, gdy wiadomość zostanie dodany za każdym razem, gdy plik zostanie przeniesiony z konta magazynu toohello StorSimple.</span><span class="sxs-lookup"><span data-stu-id="06b13-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="06b13-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06b13-180">Next steps</span></span>

<span data-ttu-id="06b13-181">[Użyj zestawu SDK .NET toolaunch Menedżer StorSimple danych zadania](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="06b13-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
