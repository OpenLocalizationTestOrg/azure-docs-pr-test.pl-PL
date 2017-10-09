---
title: aaaRestore woluminu StorSimple z kopii zapasowej | Dokumentacja firmy Microsoft
description: "W tym artykule wyjaśniono, jak toouse hello toorestore strony katalogu kopii zapasowej usługi Menedżer StorSimple woluminu StorSimple z zestawu kopii zapasowych."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="bee2e-103">Przywracania woluminu StorSimple z zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bee2e-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="bee2e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bee2e-104">Overview</span></span>
<span data-ttu-id="bee2e-105">Witaj **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane.</span><span class="sxs-lookup"><span data-stu-id="bee2e-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="bee2e-106">Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.</span><span class="sxs-lookup"><span data-stu-id="bee2e-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Strona katalogu kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="bee2e-108">Ten samouczek wyjaśnia sposób toouse hello **katalogu kopii zapasowej** strony toorestore woluminu na urządzeniu z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="bee2e-109">Jak toouse hello katalogu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bee2e-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="bee2e-110">Witaj **katalogu kopii zapasowej** strona zawiera zapytanie, które pomaga toonarrow wybór zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="bee2e-111">Można filtrować hello zestawy kopii zapasowych pobieranych oparte na powitania następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="bee2e-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="bee2e-112">**Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="bee2e-113">**Wykonaj kopię zapasową zasad** lub **woluminu** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="bee2e-114">**Z** i **do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="bee2e-115">Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="bee2e-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="bee2e-116">**Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="bee2e-117">**Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="bee2e-118">**Utworzony na** — hello Data i godzina utworzenia hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="bee2e-119">**Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bee2e-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="bee2e-120">Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bee2e-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="bee2e-121">Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="bee2e-122">**Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie zgodnie z harmonogramem tooa lub ręcznie przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bee2e-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="bee2e-123">(Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bee2e-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="bee2e-124">Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji interakcyjne kopii zapasowej.)</span><span class="sxs-lookup"><span data-stu-id="bee2e-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="bee2e-125">Jak toorestore woluminu StorSimple z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bee2e-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="bee2e-126">Można użyć hello **katalogu kopii zapasowej** strony toorestore woluminu StorSimple z określonej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bee2e-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="bee2e-127">Przywracanie z kopii zapasowej spowoduje zastąpienie istniejących woluminów hello z kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="bee2e-128">Może to spowodować utratę hello żadnych danych, które zostało zapisane po wykonaniu kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="bee2e-129">Przed rozpoczęciem przywracania na woluminie upewnij się, że wolumin hello jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="bee2e-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="bee2e-130">Najpierw należy tootake hello woluminu w trybie offline na hoście hello, a następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bee2e-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="bee2e-131">Wykonaj kroki hello w [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="bee2e-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="bee2e-132">Wykonaj hello poniższych kroków toorestore woluminu z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="bee2e-133">toorestore z zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bee2e-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="bee2e-134">Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** kartę.</span><span class="sxs-lookup"><span data-stu-id="bee2e-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Katalog kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="bee2e-136">Wybierz kopię zapasową ustawione w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bee2e-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="bee2e-137">Wybierz odpowiednie urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="bee2e-138">Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.</span><span class="sxs-lookup"><span data-stu-id="bee2e-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="bee2e-139">Określ zakres czasu hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="bee2e-140">Kliknij ikonę znacznika wyboru hello</span><span class="sxs-lookup"><span data-stu-id="bee2e-140">Click hello check icon</span></span> ![ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="bee2e-142">tooexecute tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="bee2e-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="bee2e-143">Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="bee2e-144">Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów.</span><span class="sxs-lookup"><span data-stu-id="bee2e-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="bee2e-145">Te woluminy muszą być pobierane w trybie offline na hoście hello i urządzenia, zanim będzie można ich przywrócić.</span><span class="sxs-lookup"><span data-stu-id="bee2e-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="bee2e-146">Wykonaj kroki hello w [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="bee2e-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bee2e-147">Upewnij się, czy wykonano woluminów hello w tryb offline na hoście hello najpierw, przed podjęciem dalszych na urządzeniu hello hello woluminy w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="bee2e-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="bee2e-148">W przypadku niepodjęcia hello woluminy w tryb offline na hoście hello potencjalnie spowodować uszkodzenie toodata.</span><span class="sxs-lookup"><span data-stu-id="bee2e-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="bee2e-149">Wybierz zestaw kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bee2e-149">Select a backup set.</span></span> <span data-ttu-id="bee2e-150">Kliknij przycisk **przywrócić** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="bee2e-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="bee2e-151">Pojawi się monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="bee2e-151">You will be prompted for confirmation.</span></span> 
   
    ![Strona potwierdzenia](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="bee2e-153">Przejrzyj informacje o przywracania hello i kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="bee2e-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="bee2e-154">Spowoduje to zainicjowanie zadania przywracania, które można wyświetlić, uzyskując dostęp do hello **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="bee2e-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="bee2e-155">Po zakończeniu przywracania hello można sprawdzić zawartość hello woluminów zastępuje woluminy z kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="bee2e-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="bee2e-156">![Zobacz film](./media/storsimple-restore-from-backup-set/Video_icon.png) **Zobacz film**</span><span class="sxs-lookup"><span data-stu-id="bee2e-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="bee2e-157">toowatch film wideo przedstawiający sposób Użyj klonowania hello i przywracania funkcji w plikach toorecover usunięte StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="bee2e-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bee2e-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bee2e-158">Next steps</span></span>
* <span data-ttu-id="bee2e-159">Dowiedz się, jak za[woluminów StorSimple zarządzanie](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="bee2e-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="bee2e-160">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bee2e-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

