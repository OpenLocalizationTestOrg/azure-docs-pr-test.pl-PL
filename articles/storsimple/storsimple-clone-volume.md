---
title: Klonowanie woluminu StorSimple | Dokumentacja firmy Microsoft
description: "Opisano w klonowania różnych typów i ich użycie i opisano sposób korzystania z zestawu sklonować poszczególnych woluminów kopii zapasowych."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="bcaf2-103">Klonowanie woluminu przy użyciu usługi Menedżer StorSimple</span><span class="sxs-lookup"><span data-stu-id="bcaf2-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="bcaf2-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bcaf2-104">Overview</span></span>
<span data-ttu-id="bcaf2-105">Usługę Menedżer StorSimple **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="bcaf2-106">Ta strona służy do listę wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub woluminem, zaznacz lub usuń kopii zapasowych lub użyj kopii zapasowej do przywrócenia lub sklonować woluminu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![Strona katalogu kopii zapasowej](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="bcaf2-108">Ten przewodnik opisuje sposób korzystania z zestawu sklonować poszczególnych woluminów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="bcaf2-109">Objaśniono także różnice między *przejściowa* i *stałe* klonów.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="bcaf2-110">Tworzenie własnego klonu woluminu</span><span class="sxs-lookup"><span data-stu-id="bcaf2-110">Create a clone of a volume</span></span>
<span data-ttu-id="bcaf2-111">Klon na tym samym urządzeniu, innego urządzenia lub nawet maszynę wirtualną można utworzyć przy użyciu lokalnych lub migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="bcaf2-112">Klonowanie woluminów</span><span class="sxs-lookup"><span data-stu-id="bcaf2-112">To clone a volume</span></span>
1. <span data-ttu-id="bcaf2-113">Na stronie usługi Menedżer StorSimple, kliknij przycisk **katalog kopii zapasowej** i wybierz zestaw kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="bcaf2-114">Rozwiń zestaw, aby wyświetlić skojarzone woluminy kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="bcaf2-115">Kliknij i wybierz wolumin z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-115">Click and select a volume from the backup set.</span></span>
   
     ![Klonowanie woluminu](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="bcaf2-117">Kliknij przycisk **klonowania** aby rozpocząć klonowanie wybranego woluminu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="bcaf2-118">W Kreatorze klonowania woluminu w obszarze **Określ nazwę i lokalizację**:</span><span class="sxs-lookup"><span data-stu-id="bcaf2-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="bcaf2-119">Określ urządzenia docelowego.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-119">Identify a target device.</span></span> <span data-ttu-id="bcaf2-120">Jest to lokalizacja, w której zostanie utworzona klonu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="bcaf2-121">Można wybrać tego samego urządzenia lub Określ innego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="bcaf2-122">Jeśli wybierzesz woluminu skojarzony z innym dostawcom usług w chmurze (nie Azure), listy rozwijanej dla urządzenia będzie pokazywać tylko fizyczne urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="bcaf2-123">Nie można sklonować woluminu skojarzony z innym dostawcom usług w chmurze na urządzeniu wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="bcaf2-124">Upewnij się, że wydajność wymaganą dla klonu jest starsza niż pojemność dostępna na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="bcaf2-125">Określ nazwę unikatową woluminu z klonu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="bcaf2-126">Nazwa musi zawierać od 3 do 127 znaków.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="bcaf2-127">Kliknij ikonę strzałki,</span><span class="sxs-lookup"><span data-stu-id="bcaf2-127">Click the arrow icon</span></span> ![ikona strzałki](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="bcaf2-129">Aby przejść do następnej strony.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="bcaf2-130">W obszarze **określić hosty, na których można korzystać z tego woluminu**:</span><span class="sxs-lookup"><span data-stu-id="bcaf2-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="bcaf2-131">Określ rekord kontroli dostępu (ACR) dla klonu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="bcaf2-132">Można dodawać nowe ACR lub wybierz z listy.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="bcaf2-133">Kliknij ikonę znacznika wyboru</span><span class="sxs-lookup"><span data-stu-id="bcaf2-133">Click the check icon</span></span> ![ikona znacznika wyboru](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="bcaf2-135">do ukończenia tej operacji.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-135">to complete the operation.</span></span>
6. <span data-ttu-id="bcaf2-136">Zadanie klonowania zostanie rozpoczęte i użytkownik zostanie powiadomiony, gdy klonu został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="bcaf2-137">Kliknij przycisk **zadania** do monitorowania zadania sklonowany na **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="bcaf2-138">Po zakończeniu zadania klonu:</span><span class="sxs-lookup"><span data-stu-id="bcaf2-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="bcaf2-139">Przejdź do **urządzeń** i wybrać opcję **kontenery woluminów** kartę.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="bcaf2-140">Wybierz kontener woluminu, który jest skojarzony z woluminu źródłowego, który można sklonować.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="bcaf2-141">Na liście woluminów powinna zostać wyświetlona klonowania, która została właśnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="bcaf2-142">Monitorowanie i domyślnego tworzenia kopii zapasowej są automatycznie wyłączane na sklonowanym woluminie.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="bcaf2-143">Sklonowany, która jest tworzona w ten sposób jest przejściowy klonowania.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="bcaf2-144">Aby uzyskać więcej informacji na temat typów w klonowania, zobacz [przejściowej a stałe klony](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="bcaf2-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="bcaf2-145">Tego klonu jest teraz regularne woluminu, a wszelkie operacje dostępnego na woluminie będą dostępne dla sklonowanego.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="bcaf2-146">Należy skonfigurować ten wolumin do wszelkich kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="bcaf2-147">Przejściowy a klony stałych</span><span class="sxs-lookup"><span data-stu-id="bcaf2-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="bcaf2-148">Klony przejściowych i stałe są tworzone tylko wtedy, gdy są klonowania na innym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="bcaf2-149">Można sklonować określonego woluminu z kopii zapasowej ustawiona na innym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="bcaf2-150">Klon utworzone w ten sposób jest *przejściowa* klonowania.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="bcaf2-151">Przejściowa klonowania zostanie odwołania do oryginalnego woluminu i użyje tego woluminu do odczytu podczas zapisywania lokalnie.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="bcaf2-152">Po wykonaniu migawkę chmury w klonowania przejściowej klonu wynikowy będzie *stałe* klonowania.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="bcaf2-153">Stałe klonowania jest niezależna i nie zawiera żadnych odwołań do oryginalnego woluminu, który został sklonowany z.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="bcaf2-154">Scenariusze dotyczące klony przejściowych i stałe</span><span class="sxs-lookup"><span data-stu-id="bcaf2-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="bcaf2-155">W poniższych sekcjach opisano przykład sytuacji, w których można użyć klony przejściowych i stałe.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="bcaf2-156">Odzyskiwanie na poziomie elementu przejściowej klonu</span><span class="sxs-lookup"><span data-stu-id="bcaf2-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="bcaf2-157">Należy odzyskać plik prezentacji programu Microsoft PowerPoint co roku tygodniowych.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="bcaf2-158">IT administrator identyfikuje kopii zapasowej w tym czasie, a następnie filtruje woluminu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="bcaf2-159">Następnie administrator klonuje wolumin, lokalizuje plik, którego szukasz i przekazuje go do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="bcaf2-160">W tym scenariuszu jest używana przejściowej klonowania.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="bcaf2-161">![Zobacz film](./media/storsimple-clone-volume/Video_icon.png) **Zobacz film**</span><span class="sxs-lookup"><span data-stu-id="bcaf2-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="bcaf2-162">Aby obejrzeć film wideo przedstawiający sposób użycia klonu i przywrócić funkcji w programie StorSimple, aby odzyskać usunięte pliki, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="bcaf2-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="bcaf2-163">Testowanie w środowisku produkcyjnym klonu stałych</span><span class="sxs-lookup"><span data-stu-id="bcaf2-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="bcaf2-164">Należy sprawdzić usterkę testowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="bcaf2-165">Możesz Tworzenie własnego klonu woluminu w środowisku produkcyjnym, wykonując migawkę chmury dla tego klonu.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="bcaf2-166">Sklonowany woluminu jest teraz niezależne.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-166">The cloned volume is now independent.</span></span> <span data-ttu-id="bcaf2-167">W tym scenariuszu stały klonowania jest używany.</span><span class="sxs-lookup"><span data-stu-id="bcaf2-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcaf2-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcaf2-168">Next steps</span></span>
* <span data-ttu-id="bcaf2-169">Dowiedz się, jak [przywracania woluminu StorSimple z zestawu kopii zapasowych](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="bcaf2-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="bcaf2-170">Dowiedz się, jak [zarządzać urządzenia StorSimple przy użyciu usługi Menedżer StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bcaf2-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

