---
title: Grupy woluminu StorSimple Snapshot Manager | Dokumentacja firmy Microsoft
description: "Informacje dotyczące używania przystawki MMC programu StorSimple Snapshot Manager do tworzenia i zarządzania grupami woluminu."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="1d7af-103">StorSimple Snapshot Manager umożliwia tworzenie i zarządzanie grupami woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="1d7af-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1d7af-104">Overview</span></span>
<span data-ttu-id="1d7af-105">Można użyć **grup woluminu** węzła na **zakres** okienko, aby przypisać woluminy do grup woluminu, Wyświetl informacje o grupie woluminu, zaplanować wykonywanie kopii zapasowych i edytować grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="1d7af-106">Wolumin grupy są pule powiązanych woluminów używanych do zapewnienia, że kopie zapasowe są spójne z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="1d7af-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="1d7af-107">Aby uzyskać więcej informacji, zobacz [woluminów i woluminów grupy](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) i [integracji z usługą kopiowania woluminów w tle Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1d7af-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1d7af-108">Wszystkie woluminy w grupie woluminu musi pochodzić od dostawcy usług w chmurze pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="1d7af-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="1d7af-109">Po skonfigurowaniu grup woluminu niemieszanie udostępnione woluminy klastra (CSV), a nie CSV w tej samej grupie woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="1d7af-110">StorSimple Snapshot Manager nie obsługuje zarówno udostępnionych woluminów klastra i z systemem innym niż udostępnionych woluminów klastra w tej samej migawki.</span><span class="sxs-lookup"><span data-stu-id="1d7af-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![Wolumin węzeł grupy](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="1d7af-112">**Rysunek 1: Węzeł StorSimple Snapshot Manager woluminu grup**</span><span class="sxs-lookup"><span data-stu-id="1d7af-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="1d7af-113">W tym samouczku wyjaśniono, jak używasz StorSimple Snapshot Manager do:</span><span class="sxs-lookup"><span data-stu-id="1d7af-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="1d7af-114">Wyświetlanie informacji o woluminie grup</span><span class="sxs-lookup"><span data-stu-id="1d7af-114">View information about your volume groups</span></span>
* <span data-ttu-id="1d7af-115">Utwórz grupę woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-115">Create a volume group</span></span>
* <span data-ttu-id="1d7af-116">Tworzenie kopii zapasowej grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-116">Back up a volume group</span></span>
* <span data-ttu-id="1d7af-117">Edytowanie grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-117">Edit a volume group</span></span>
* <span data-ttu-id="1d7af-118">Usuwanie grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-118">Delete a volume group</span></span>

<span data-ttu-id="1d7af-119">Wszystkie te działania są również dostępne na **akcje** okienka.</span><span class="sxs-lookup"><span data-stu-id="1d7af-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="1d7af-120">Wyświetlanie grup woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-120">View volume groups</span></span>
<span data-ttu-id="1d7af-121">Jeśli klikniesz przycisk **grup woluminu** węzła, **wyniki** w okienku zostaną wyświetlone następujące informacje dotyczące każdej grupy woluminu, w zależności od opcji kolumny wprowadzeniu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="1d7af-122">(W kolumnach **wyniki** okienku są konfigurowane.</span><span class="sxs-lookup"><span data-stu-id="1d7af-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="1d7af-123">Kliknij prawym przyciskiem myszy **woluminów** węzła, wybierz opcję **widoku**, a następnie wybierz **Dodaj/Usuń kolumny**.)</span><span class="sxs-lookup"><span data-stu-id="1d7af-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="1d7af-124">Kolumny wyników</span><span class="sxs-lookup"><span data-stu-id="1d7af-124">Results column</span></span> | <span data-ttu-id="1d7af-125">Opis</span><span class="sxs-lookup"><span data-stu-id="1d7af-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d7af-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1d7af-126">Name</span></span> |<span data-ttu-id="1d7af-127">**Nazwa** kolumna zawiera nazwę grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="1d7af-128">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="1d7af-128">Application</span></span> |<span data-ttu-id="1d7af-129">**Aplikacji** kolumnie jest wyświetlana liczba składniki zapisywania usługi VSS aktualnie zainstalowana i uruchomiona na hoście systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1d7af-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="1d7af-130">Wybrano</span><span class="sxs-lookup"><span data-stu-id="1d7af-130">Selected</span></span> |<span data-ttu-id="1d7af-131">**Wybrane** kolumna zawiera wiele woluminów, które są zawarte w grupie woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="1d7af-132">Wartość zero (0) oznacza, że żadna aplikacja nie jest skojarzony z woluminów w grupie woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="1d7af-133">Zaimportowany</span><span class="sxs-lookup"><span data-stu-id="1d7af-133">Imported</span></span> |<span data-ttu-id="1d7af-134">**Zaimportowane** kolumnie jest wyświetlana liczba importowanych woluminów.</span><span class="sxs-lookup"><span data-stu-id="1d7af-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="1d7af-135">Jeśli wartość **True**, ta kolumna wskazuje, że grupa woluminu została zaimportowana z portalu Azure i programu StorSimple Snapshot Manager nie został utworzony.</span><span class="sxs-lookup"><span data-stu-id="1d7af-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="1d7af-136">Grupy woluminu StorSimple Snapshot Manager również są wyświetlane na **zasady tworzenia kopii zapasowej** kartę w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7af-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="1d7af-137">Utwórz grupę woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-137">Create a volume group</span></span>
<span data-ttu-id="1d7af-138">Poniższa procedura umożliwia utworzenie grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="1d7af-139">Aby utworzyć grupę woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-139">To create a volume group</span></span>
1. <span data-ttu-id="1d7af-140">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1d7af-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1d7af-141">W **zakres** okienku kliknij prawym przyciskiem myszy **grup woluminu**, a następnie kliknij przycisk **Utwórz grupę woluminu**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Utwórz grupę woluminu](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="1d7af-143">**Utwórz grupę woluminu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1d7af-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![Tworzenie okna dialogowego grupy woluminu](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="1d7af-145">Wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1d7af-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="1d7af-146">W **nazwa** wpisz unikatową nazwę dla nowej grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="1d7af-147">W **aplikacji** polu Wybierz aplikacji skojarzonych z woluminów, które ma być dodany do grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="1d7af-148">**Aplikacji** okno wyświetla tylko te aplikacje, które korzysta z woluminów StorSimple i mieć składniki zapisywania usługi VSS są włączone dla nich.</span><span class="sxs-lookup"><span data-stu-id="1d7af-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="1d7af-149">Składnik zapisywania usługi VSS jest włączona tylko wtedy, gdy wszystkie woluminy, które moduł zapisujący zna woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d7af-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="1d7af-150">Jeśli pole aplikacji jest pusta, aplikacje, nie korzysta z woluminów Azure StorSimple, które mają być obsługiwane składniki zapisywania usługi VSS są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="1d7af-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="1d7af-151">(Aktualnie Azure StorSimple obsługuje program Microsoft Exchange i SQL Server). Aby uzyskać więcej informacji na temat zapisywania usługi VSS, zobacz [integracji z usługą kopiowania woluminów w tle Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1d7af-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="1d7af-152">Wybierz aplikację, wszystkie woluminy skojarzone z nim automatycznie zaznaczenie.</span><span class="sxs-lookup"><span data-stu-id="1d7af-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="1d7af-153">Z drugiej strony, jeśli wybrano woluminy skojarzone z określoną aplikacją, aplikacja jest automatycznie wybierany w **aplikacji** pole.</span><span class="sxs-lookup"><span data-stu-id="1d7af-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="1d7af-154">W **woluminów** wybierz woluminy StorSimple, aby dodać do grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="1d7af-155">Może zawierać woluminy z jednego lub wielu partycji.</span><span class="sxs-lookup"><span data-stu-id="1d7af-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="1d7af-156">(Wiele woluminów partycji może być dynamicznych dysków lub dysków podstawowych z wieloma partycjami.) Wolumin, który zawiera wiele partycji jest traktowany jako pojedyncza jednostka.</span><span class="sxs-lookup"><span data-stu-id="1d7af-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="1d7af-157">W związku z tym jeśli dodasz do grupy woluminu tylko jedną z partycji, wszystkie pozostałe partycje są automatycznie dodawane do tej grupy woluminu w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="1d7af-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="1d7af-158">Po dodaniu woluminu wiele partycji w grupie woluminu woluminu wiele partycji w dalszym ciągu traktowane jako pojedyncza jednostka.</span><span class="sxs-lookup"><span data-stu-id="1d7af-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="1d7af-159">Możesz tworzyć grupy pusty woluminu, przypisując nie wszystkie woluminy do nich.</span><span class="sxs-lookup"><span data-stu-id="1d7af-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="1d7af-160">Nie należy ich łączyć udostępnione woluminy klastra (CSV), a nie CSV w tej samej grupie woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="1d7af-161">StorSimple Snapshot Manager nie obsługuje zarówno woluminów CSV i woluminów CSV z systemem innym niż w tej samej migawki.</span><span class="sxs-lookup"><span data-stu-id="1d7af-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="1d7af-162">Kliknij przycisk **OK** można zapisać grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="1d7af-163">Tworzenie kopii zapasowej grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-163">Back up a volume group</span></span>
<span data-ttu-id="1d7af-164">Poniższa procedura umożliwia tworzenie kopii zapasowej grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="1d7af-165">Aby utworzyć kopię zapasową woluminu grupy</span><span class="sxs-lookup"><span data-stu-id="1d7af-165">To back up a volume group</span></span>
1. <span data-ttu-id="1d7af-166">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1d7af-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1d7af-167">W **zakres** okienku rozwiń **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **wykonać kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Natychmiast utworzyć kopię zapasową woluminu grupy](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="1d7af-169">W **wykonać kopii zapasowej** okno dialogowe, wybierz opcję **migawka lokalna** lub **migawka w chmurze**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Zająć kopii zapasowej okna dialogowego](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="1d7af-171">Aby upewnić się, że kopia zapasowa jest uruchomiony, rozwiń **zadania** węzeł, a następnie kliknij przycisk **systemem**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="1d7af-172">Tworzenie kopii zapasowej powinien być wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="1d7af-172">The backup should be listed.</span></span>
5. <span data-ttu-id="1d7af-173">Aby wyświetlić ukończone migawki, rozwiń **katalog kopii zapasowej** węzła, rozwinąć nazwę grupy woluminu, a następnie kliknij przycisk **migawka lokalna** lub **migawka w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="1d7af-174">Tworzenie kopii zapasowej będzie wyświetlane, jeśli zostało zakończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="1d7af-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="1d7af-175">Edytowanie grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-175">Edit a volume group</span></span>
<span data-ttu-id="1d7af-176">Użyj poniższej procedury do edycji grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="1d7af-177">Aby edytować grupę woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-177">To edit a volume group</span></span>
1. <span data-ttu-id="1d7af-178">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1d7af-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1d7af-179">W **zakres** okienku rozwiń **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="1d7af-180">** Utwórz grupę woluminu ** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1d7af-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="1d7af-181">Możesz zmienić **nazwa**, **aplikacji**, i **woluminów** wpisów.</span><span class="sxs-lookup"><span data-stu-id="1d7af-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="1d7af-182">Kliknij przycisk **OK**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="1d7af-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="1d7af-183">Usuwanie grupy woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-183">Delete a volume group</span></span>
<span data-ttu-id="1d7af-184">Użyj poniższej procedury można usunąć grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="1d7af-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="1d7af-185">Powoduje to również usunięcie wszystkich skojarzonych z grupą woluminu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1d7af-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="1d7af-186">Aby usunąć grupę woluminu</span><span class="sxs-lookup"><span data-stu-id="1d7af-186">To delete a volume group</span></span>
1. <span data-ttu-id="1d7af-187">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1d7af-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1d7af-188">W **zakres** okienku rozwiń **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="1d7af-189">**Usuń grupę woluminu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1d7af-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="1d7af-190">Typ **Potwierdź** w polu tekstowym, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d7af-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="1d7af-191">Grupy usunięte woluminu nieodpowiedniej z listy w **wyniki** okienko i wszystkie kopie zapasowe, które są skojarzone z tą grupą woluminu są usuwane z katalogu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1d7af-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d7af-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d7af-192">Next steps</span></span>
* <span data-ttu-id="1d7af-193">Dowiedz się, jak [zarządzać rozwiązania StorSimple przy użyciu programu StorSimple Snapshot Manager](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1d7af-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="1d7af-194">Dowiedz się, jak [StorSimple Snapshot Manager umożliwia tworzenie i zarządzanie zasadami tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1d7af-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

