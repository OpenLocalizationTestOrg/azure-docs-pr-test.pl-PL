---
title: zasady tworzenia kopii zapasowej Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello toocreate przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi hello zasad tworzenia kopii zapasowych, które kontrolują zaplanowanych kopii zapasowych."
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="2535c-103">Użyj toocreate StorSimple Snapshot Manager i zarządzanie zasadami tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="2535c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2535c-104">Overview</span></span>
<span data-ttu-id="2535c-105">Zasady tworzenia kopii zapasowej tworzy harmonogram tworzenia kopii zapasowych danych woluminu lokalnie lub w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="2535c-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="2535c-106">Podczas tworzenia zasad tworzenia kopii zapasowej, można także określić zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2535c-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="2535c-107">(Można zachować maksymalnie 64 migawki). Aby uzyskać więcej informacji na temat zasad tworzenia kopii zapasowych, zobacz [kopii zapasowej typy](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) w [z serii StorSimple 8000: rozwiązanie chmury hybrydowej](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2535c-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="2535c-108">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="2535c-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="2535c-109">Tworzenie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-109">Create a backup policy</span></span>
* <span data-ttu-id="2535c-110">Edytowanie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-110">Edit a backup policy</span></span>
* <span data-ttu-id="2535c-111">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="2535c-112">Tworzenie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-112">Create a backup policy</span></span>
<span data-ttu-id="2535c-113">Użyj hello następujące procedury toocreate nowych zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2535c-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="2535c-114">toocreate zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="2535c-115">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2535c-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2535c-116">W hello **zakres** okienku kliknij prawym przyciskiem myszy **zasady tworzenia kopii zapasowej**i kliknij przycisk **zasad tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="2535c-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Tworzenie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="2535c-118">Witaj **utworzyć zasadę** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2535c-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Utwórz zasadę — karta Ogólne](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="2535c-120">Na powitania **ogólne** kartę, pełną hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="2535c-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="2535c-121">W hello **nazwa** polu tekstowym, wpisz nazwę zasady hello.</span><span class="sxs-lookup"><span data-stu-id="2535c-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="2535c-122">W hello **grupy woluminu** pole tekstowe, nazwa typu hello hello woluminu grupy skojarzone z zasadą hello.</span><span class="sxs-lookup"><span data-stu-id="2535c-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="2535c-123">Wybierz opcję **migawka lokalna** lub **migawki w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="2535c-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="2535c-124">Wybierz liczbę hello tooretain migawki.</span><span class="sxs-lookup"><span data-stu-id="2535c-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="2535c-125">W przypadku wybrania **wszystkie**, zostaną zachowane 64 migawek (hello maksymalnej).</span><span class="sxs-lookup"><span data-stu-id="2535c-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="2535c-126">Kliknij przycisk hello **harmonogram** kartę.</span><span class="sxs-lookup"><span data-stu-id="2535c-126">Click hello **Schedule** tab.</span></span>

    ![Utwórz zasadę — karta harmonogram](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="2535c-128">Na powitania **harmonogram** kartę, pełną hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="2535c-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="2535c-129">Kliknij przycisk hello **włączyć** pole wyboru tooschedule hello następnej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2535c-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="2535c-130">W obszarze **ustawienia**, wybierz pozycję **jeden raz**, **codzienne**, **co tydzień**, lub **miesięczne**.</span><span class="sxs-lookup"><span data-stu-id="2535c-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="2535c-131">W hello **Start** pola tekstowego, kliknij ikonę kalendarza hello i wybierz datę rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="2535c-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="2535c-132">W obszarze **Zaawansowane ustawienia**, można ustawić opcjonalny powtarzania harmonogramów oraz datę zakończenia.</span><span class="sxs-lookup"><span data-stu-id="2535c-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="2535c-133">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2535c-133">Click **OK**.</span></span>

<span data-ttu-id="2535c-134">Po utworzeniu zasad tworzenia kopii zapasowej hello następujących informacji jest wyświetlana w hello **wyniki** okienka:</span><span class="sxs-lookup"><span data-stu-id="2535c-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="2535c-135">**Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2535c-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="2535c-136">**Typ** — migawka lokalna i migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2535c-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="2535c-137">**Grupy woluminu** — Witaj skojarzonych z zasadami hello grupy woluminu.</span><span class="sxs-lookup"><span data-stu-id="2535c-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="2535c-138">**Przechowywania** — Witaj zachowane liczby migawek; hello maksymalna 64.</span><span class="sxs-lookup"><span data-stu-id="2535c-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="2535c-139">**Utworzony** — Data hello zasada została utworzona.</span><span class="sxs-lookup"><span data-stu-id="2535c-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="2535c-140">**Włączone** — czy zasada hello jest obecnie efekt: **True** wskazuje, że jest włączona; **False** wskazuje, że nie będzie obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="2535c-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="2535c-141">Edytowanie zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-141">Edit a backup policy</span></span>
<span data-ttu-id="2535c-142">Użyj hello następujące procedury tooedit istniejących zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2535c-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="2535c-143">tooedit zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="2535c-144">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2535c-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2535c-145">W hello **zakres** okienku, kliknij przycisk hello **zasady tworzenia kopii zapasowej** węzła.</span><span class="sxs-lookup"><span data-stu-id="2535c-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="2535c-146">Wszystkie zasady tworzenia kopii zapasowej hello są wyświetlane w hello **wyniki** okienka.</span><span class="sxs-lookup"><span data-stu-id="2535c-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="2535c-147">Kliknij prawym przyciskiem myszy zasady hello mają tooedit, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="2535c-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Edytowanie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="2535c-149">Gdy hello **utworzyć zasadę** zostanie wyświetlone okno, wprowadź zmiany, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2535c-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="2535c-150">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-150">Delete a backup policy</span></span>
<span data-ttu-id="2535c-151">Użyj hello następujące procedury toodelete zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2535c-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="2535c-152">toodelete zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2535c-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="2535c-153">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2535c-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2535c-154">W hello **zakres** okienku, kliknij przycisk hello **zasady tworzenia kopii zapasowej** węzła.</span><span class="sxs-lookup"><span data-stu-id="2535c-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="2535c-155">Wszystkie zasady tworzenia kopii zapasowej hello są wyświetlane w hello **wyniki** okienka.</span><span class="sxs-lookup"><span data-stu-id="2535c-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="2535c-156">Kliknij prawym przyciskiem myszy zasady tworzenia kopii zapasowej hello mają toodelete, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2535c-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="2535c-157">Po wyświetleniu komunikatu potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="2535c-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Zasady tworzenia kopii zapasowej potwierdzenie usunięcia](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="2535c-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2535c-159">Next steps</span></span>
* <span data-ttu-id="2535c-160">Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2535c-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="2535c-161">Dowiedz się, jak za[Użyj tooview StorSimple Snapshot Manager i zarządzanie nimi zadania tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="2535c-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
