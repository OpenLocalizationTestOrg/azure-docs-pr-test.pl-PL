---
title: Przywracanie z kopii zapasowej woluminu StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak strona katalogu kopii zapasowej usługi Menedżer StorSimple służy do przywracania woluminu StorSimple z zestawu kopii zapasowych."
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
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="29a70-103">Przywracania woluminu StorSimple z zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="29a70-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="29a70-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="29a70-104">Overview</span></span>
<span data-ttu-id="29a70-105">**Katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane.</span><span class="sxs-lookup"><span data-stu-id="29a70-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="29a70-106">Ta strona służy do listę wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub woluminem, zaznacz lub usuń kopii zapasowych lub użyj kopii zapasowej do przywrócenia lub sklonować woluminu.</span><span class="sxs-lookup"><span data-stu-id="29a70-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Strona katalogu kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="29a70-108">W tym samouczku wyjaśniono, jak używać **katalogu kopii zapasowej** stronę, aby odzyskać wolumin w urządzeniu z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="29a70-109">Jak używać katalogu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="29a70-109">How to use the backup catalog</span></span>
<span data-ttu-id="29a70-110">**Katalogu kopii zapasowej** strona zawiera zaznaczyć kwerendę, która pomaga ograniczyć kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="29a70-111">Można filtrować zestawy kopii zapasowych, które są pobierane na podstawie następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="29a70-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="29a70-112">**Urządzenie** — urządzenia, na którym utworzono ten zestaw kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="29a70-113">**Wykonaj kopię zapasową zasad** lub **woluminu** — zasady tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="29a70-114">**Z** i **do** — zakres dat i godzin przy tworzeniu zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="29a70-115">Następnie filtrowane zestawy kopii zapasowych wyszczególniono na podstawie następujących atrybutów:</span><span class="sxs-lookup"><span data-stu-id="29a70-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="29a70-116">**Nazwa** — Nazwa zasad tworzenia kopii zapasowej lub woluminie skojarzonym z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="29a70-117">**Rozmiar** — rzeczywisty rozmiar zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="29a70-118">**Utworzony na** — Data i godzina utworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="29a70-119">**Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="29a70-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="29a70-120">Migawka lokalna jest kopię zapasową wszystkich danych woluminu lokalnie przechowywanych na urządzeniu, migawka w chmurze odnosi się do kopii zapasowej danych woluminu znajdującej się w chmurze.</span><span class="sxs-lookup"><span data-stu-id="29a70-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="29a70-121">Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.</span><span class="sxs-lookup"><span data-stu-id="29a70-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="29a70-122">**Zainicjowane przez** — tworzenie kopii zapasowych może zostać zainicjowane automatycznie, zgodnie z harmonogramem lub ręcznie przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29a70-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="29a70-123">(Aby zaplanować tworzenie kopii zapasowych można użyć zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="29a70-124">Alternatywnie można użyć **utworzenia kopii zapasowej** opcję, aby wykonać interakcyjne kopii zapasowej.)</span><span class="sxs-lookup"><span data-stu-id="29a70-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="29a70-125">Jak przywrócić z kopii zapasowej woluminu StorSimple</span><span class="sxs-lookup"><span data-stu-id="29a70-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="29a70-126">Można użyć **katalogu kopii zapasowej** strony, aby przywrócić woluminu StorSimple z określonej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="29a70-127">Przywracanie z kopii zapasowej spowoduje zastąpienie istniejących woluminów z kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="29a70-128">Może to spowodować utratę wszystkich danych, który został zapisany po wykonaniu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="29a70-129">Przed rozpoczęciem przywracania na woluminie, upewnij się, że wolumin jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="29a70-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="29a70-130">Musisz wykonać pierwszy woluminu w trybie offline na hoście, a następnie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="29a70-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="29a70-131">Postępuj zgodnie z instrukcjami [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="29a70-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="29a70-132">Wykonaj poniższe kroki, aby odzyskać wolumin z zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="29a70-133">Przywrócenie z zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="29a70-133">To restore from a backup set</span></span>
1. <span data-ttu-id="29a70-134">Na stronie usługi Menedżer StorSimple, kliknij przycisk **katalog kopii zapasowej** kartę.</span><span class="sxs-lookup"><span data-stu-id="29a70-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Katalog kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="29a70-136">Wybierz kopię zapasową ustawione w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29a70-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="29a70-137">Wybierz odpowiednie urządzenie.</span><span class="sxs-lookup"><span data-stu-id="29a70-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="29a70-138">Na liście rozwijanej wybierz zasady woluminu lub kopii zapasowej do utworzenia kopii zapasowej, który chcesz wybrać.</span><span class="sxs-lookup"><span data-stu-id="29a70-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="29a70-139">Określ zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="29a70-139">Specify the time range.</span></span>
   4. <span data-ttu-id="29a70-140">Kliknij ikonę znacznika wyboru</span><span class="sxs-lookup"><span data-stu-id="29a70-140">Click the check icon</span></span> ![ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="29a70-142">do wykonania tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="29a70-142">to execute this query.</span></span>
      
      <span data-ttu-id="29a70-143">Tworzenie kopii zapasowych skojarzony z wybranego woluminu lub zasad tworzenia kopii zapasowej powinien zostać wyświetlony na liście zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="29a70-144">Rozwiń zestaw, aby wyświetlić skojarzone woluminy kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="29a70-145">Te woluminy muszą być pobierane w trybie offline na hoście i urządzenia, zanim będzie można ich przywrócić.</span><span class="sxs-lookup"><span data-stu-id="29a70-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="29a70-146">Postępuj zgodnie z instrukcjami [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="29a70-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="29a70-147">Upewnij się, że została wykonana woluminy w tryb offline na hoście najpierw, przed podjęciem dalszych woluminy w tryb offline na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="29a70-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="29a70-148">Jeśli nie przyjmują woluminy w tryb offline na hoście, może prowadzić do uszkodzenia danych.</span><span class="sxs-lookup"><span data-stu-id="29a70-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="29a70-149">Wybierz zestaw kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29a70-149">Select a backup set.</span></span> <span data-ttu-id="29a70-150">Kliknij przycisk **przywrócić** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="29a70-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="29a70-151">Pojawi się monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="29a70-151">You will be prompted for confirmation.</span></span> 
   
    ![Strona potwierdzenia](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="29a70-153">Przejrzyj informacje przywracania, a następnie kliknij ikonę znacznika wyboru ![Ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="29a70-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="29a70-154">Spowoduje to zainicjowanie zadania przywracania, które można wyświetlić, uzyskując dostęp do **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="29a70-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="29a70-155">Po zakończeniu przywracania można sprawdzić, czy zawartość woluminów są zastępowane przez woluminy z kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29a70-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="29a70-156">![Zobacz film](./media/storsimple-restore-from-backup-set/Video_icon.png) **Zobacz film**</span><span class="sxs-lookup"><span data-stu-id="29a70-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="29a70-157">Aby obejrzeć film wideo przedstawiający sposób użycia klonu i przywrócić funkcji w programie StorSimple, aby odzyskać usunięte pliki, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="29a70-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="29a70-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29a70-158">Next steps</span></span>
* <span data-ttu-id="29a70-159">Dowiedz się, jak [woluminów StorSimple zarządzanie](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="29a70-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="29a70-160">Dowiedz się, jak [zarządzać urządzenia StorSimple przy użyciu usługi Menedżer StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="29a70-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

