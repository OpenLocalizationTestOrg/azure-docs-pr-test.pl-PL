---
title: Zasady tworzenia kopii zapasowej programu StorSimple Snapshot Manager | Dokumentacja firmy Microsoft
description: "Informacje dotyczące używania przystawki MMC programu StorSimple Snapshot Manager do tworzenia i obsługi zasad tworzenia kopii zapasowych, które kontrolują zaplanowanych kopii zapasowych."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="be878-103">StorSimple Snapshot Manager umożliwia tworzenie i zarządzanie zasadami tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="be878-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="be878-104">Overview</span></span>
<span data-ttu-id="be878-105">Zasady tworzenia kopii zapasowej tworzy harmonogram tworzenia kopii zapasowych danych woluminu lokalnie lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="be878-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="be878-106">Podczas tworzenia zasad tworzenia kopii zapasowej, można także określić zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="be878-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="be878-107">(Można zachować maksymalnie 64 migawki). Aby uzyskać więcej informacji na temat zasad tworzenia kopii zapasowych, zobacz [kopii zapasowej typy](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) w [z serii StorSimple 8000: rozwiązanie chmury hybrydowej](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be878-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="be878-108">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="be878-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="be878-109">Tworzenie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-109">Create a backup policy</span></span>
* <span data-ttu-id="be878-110">Edytowanie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-110">Edit a backup policy</span></span>
* <span data-ttu-id="be878-111">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="be878-112">Tworzenie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-112">Create a backup policy</span></span>
<span data-ttu-id="be878-113">Poniższa procedura umożliwia utworzenie nowych zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="be878-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="be878-114">Aby utworzyć zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-114">To create a backup policy</span></span>
1. <span data-ttu-id="be878-115">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="be878-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="be878-116">W **zakres** okienku kliknij prawym przyciskiem myszy **zasady tworzenia kopii zapasowej**i kliknij przycisk **zasad tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="be878-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Tworzenie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="be878-118">**Utworzyć zasadę** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="be878-118">The **Create a Policy** dialog box appears.</span></span>

    ![Utwórz zasadę — karta Ogólne](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="be878-120">Na **ogólne** karcie, wykonaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="be878-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="be878-121">W **nazwa** polu tekstowym, wpisz nazwę zasady.</span><span class="sxs-lookup"><span data-stu-id="be878-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="be878-122">W **grupy woluminu** polu tekstowym, wpisz nazwę grupy woluminu skojarzonych z zasadami.</span><span class="sxs-lookup"><span data-stu-id="be878-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="be878-123">Wybierz opcję **migawka lokalna** lub **migawki w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="be878-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="be878-124">Wybierz liczbę migawek do zachowania.</span><span class="sxs-lookup"><span data-stu-id="be878-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="be878-125">W przypadku wybrania **wszystkie**, będzie 64 migawki zachowane (maksymalnie).</span><span class="sxs-lookup"><span data-stu-id="be878-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="be878-126">Kliknij przycisk **harmonogram** kartę.</span><span class="sxs-lookup"><span data-stu-id="be878-126">Click the **Schedule** tab.</span></span>

    ![Utwórz zasadę — karta harmonogram](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="be878-128">Na **harmonogram** karcie, wykonaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="be878-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="be878-129">Kliknij przycisk **włączyć** pole wyboru, aby zaplanować następnej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="be878-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="be878-130">W obszarze **ustawienia**, wybierz pozycję **jeden raz**, **codzienne**, **co tydzień**, lub **miesięczne**.</span><span class="sxs-lookup"><span data-stu-id="be878-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="be878-131">W **Start** pola tekstowego, kliknij ikonę kalendarza i wybierz datę rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="be878-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="be878-132">W obszarze **Zaawansowane ustawienia**, można ustawić opcjonalny powtarzania harmonogramów oraz datę zakończenia.</span><span class="sxs-lookup"><span data-stu-id="be878-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="be878-133">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="be878-133">Click **OK**.</span></span>

<span data-ttu-id="be878-134">Po utworzeniu zasad tworzenia kopii zapasowej następujące informacje są wyświetlane w **wyniki** okienka:</span><span class="sxs-lookup"><span data-stu-id="be878-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="be878-135">**Nazwa** — Nazwa zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="be878-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="be878-136">**Typ** — migawka lokalna i migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="be878-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="be878-137">**Grupy woluminu** — skojarzonych z zasadami grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="be878-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="be878-138">**Przechowywania** — liczba migawki zachowane; maksymalna liczba to 64.</span><span class="sxs-lookup"><span data-stu-id="be878-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="be878-139">**Utworzony** — datę, która zasada została utworzona.</span><span class="sxs-lookup"><span data-stu-id="be878-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="be878-140">**Włączone** — czy zasada jest obecnie w efekcie: **True** wskazuje, że jest włączona; **False** wskazuje, że nie będzie obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="be878-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="be878-141">Edytowanie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-141">Edit a backup policy</span></span>
<span data-ttu-id="be878-142">Użyj poniższej procedury do edycji istniejących zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="be878-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="be878-143">Aby edytować zasadę tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-143">To edit a backup policy</span></span>
1. <span data-ttu-id="be878-144">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="be878-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="be878-145">W **zakres** okienku, kliknij przycisk **zasady tworzenia kopii zapasowej** węzła.</span><span class="sxs-lookup"><span data-stu-id="be878-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="be878-146">Zasady tworzenia kopii zapasowej są wyświetlane w **wyniki** okienka.</span><span class="sxs-lookup"><span data-stu-id="be878-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="be878-147">Kliknij prawym przyciskiem myszy zasadę, którą chcesz edytować, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="be878-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Edytowanie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="be878-149">Gdy **utworzyć zasadę** zostanie wyświetlone okno, wprowadź zmiany, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="be878-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="be878-150">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-150">Delete a backup policy</span></span>
<span data-ttu-id="be878-151">Użyj poniższej procedury można usunąć zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="be878-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="be878-152">Aby usunąć zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="be878-152">To delete a backup policy</span></span>
1. <span data-ttu-id="be878-153">Kliknij ikonę pulpitu, aby uruchomić StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="be878-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="be878-154">W **zakres** okienku, kliknij przycisk **zasady tworzenia kopii zapasowej** węzła.</span><span class="sxs-lookup"><span data-stu-id="be878-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="be878-155">Zasady tworzenia kopii zapasowej są wyświetlane w **wyniki** okienka.</span><span class="sxs-lookup"><span data-stu-id="be878-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="be878-156">Kliknij prawym przyciskiem myszy zasady tworzenia kopii zapasowej, który chcesz usunąć, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="be878-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="be878-157">Po wyświetleniu komunikatu potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="be878-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Zasady tworzenia kopii zapasowej potwierdzenie usunięcia](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="be878-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be878-159">Next steps</span></span>
* <span data-ttu-id="be878-160">Dowiedz się, jak [zarządzać rozwiązania StorSimple przy użyciu programu StorSimple Snapshot Manager](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="be878-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="be878-161">Dowiedz się, jak [StorSimple Snapshot Manager umożliwia wyświetlanie i zarządzanie nimi zadania tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="be878-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
