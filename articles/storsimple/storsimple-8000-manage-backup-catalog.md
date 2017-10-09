---
title: aaaManage katalogu kopii zapasowej StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak hello toouse toolist strony katalogu kopii zapasowej usługi Menedżera urządzeń StorSimple, wybierz i Usuń zestawy kopii zapasowych."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="15677-103">Użyj toomanage usługi Menedżer StorSimple urządzenia hello katalogu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="15677-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="15677-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="15677-104">Overview</span></span>
<span data-ttu-id="15677-105">Witaj usługi Menedżer StorSimple urządzenia **katalogu kopii zapasowej** bloku Wyświetla wszystkie zestawy kopii zapasowych hello, tworzonych podczas ręczne lub zaplanowane kopie zapasowe są pobierane.</span><span class="sxs-lookup"><span data-stu-id="15677-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="15677-106">Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.</span><span class="sxs-lookup"><span data-stu-id="15677-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="15677-107">W tym samouczku opisano toolist, wybierz i Usuń kopię zapasową konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="15677-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="15677-108">toolearn jak toorestore urządzenia z kopii zapasowej, przejdź zbyt[przywrócenie urządzenia z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="15677-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="15677-109">toolearn jak tooclone woluminu, przejdź zbyt[sklonować woluminu StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="15677-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Katalog kopii zapasowej](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="15677-111">Witaj **katalogu kopii zapasowej** bloku zapewnia toonarrow zapytania wybór zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="15677-112">Można filtrować hello zestawy kopii zapasowych, które są pobierane, oparte na powitania następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="15677-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="15677-113">**Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="15677-114">**Zasady tworzenia kopii zapasowej lub woluminie** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="15677-115">**Od i do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="15677-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="15677-116">Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="15677-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="15677-117">**Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="15677-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="15677-118">**Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="15677-119">**Utworzone na** — hello Data i godzina utworzenia hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="15677-120">**Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="15677-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="15677-121">Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="15677-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="15677-122">Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.</span><span class="sxs-lookup"><span data-stu-id="15677-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="15677-123">**Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie według harmonogramu lub ręcznie przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15677-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="15677-124">Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="15677-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="15677-125">Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji ręcznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="15677-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="15677-126">Zestawy kopii zapasowych listy dla zasad tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="15677-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="15677-127">Wykonaj następujące kroki toolist hello wszystkie kopie zapasowe hello zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="15677-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="15677-128">zestawy kopii zapasowych toolist</span><span class="sxs-lookup"><span data-stu-id="15677-128">toolist backup sets</span></span>
1. <span data-ttu-id="15677-129">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="15677-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="15677-130">Filtrować hello wybory w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15677-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="15677-131">Określ zakres czasu hello.</span><span class="sxs-lookup"><span data-stu-id="15677-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="15677-132">Wybierz odpowiednie urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="15677-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="15677-133">Filtruj według **kopii zapasowej zasad** tooview hello odpowiedniego hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="15677-134">Z listy rozwijanej zasad tworzenia kopii zapasowej hello, wybierz **wszystkie** tooview hello wszystkie kopie zapasowe na powitania wybrane urządzenia.</span><span class="sxs-lookup"><span data-stu-id="15677-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="15677-135">Kliknij przycisk **Zastosuj** tooexecute tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="15677-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="15677-136">kopie zapasowe Hello skojarzonych z zasadami tworzenia kopii zapasowej hello wybrane powinna pojawić się na liście hello zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="15677-138">Wybierz zestaw kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="15677-138">Select a backup set</span></span>
<span data-ttu-id="15677-139">Zakończenie hello następujące kroki tooselect kopii zapasowej ustawienie zasad woluminu lub kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="15677-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="15677-140">tooselect zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="15677-140">tooselect a backup set</span></span>
1. <span data-ttu-id="15677-141">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="15677-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="15677-142">Filtrować hello wybory w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15677-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="15677-143">Określ zakres czasu hello.</span><span class="sxs-lookup"><span data-stu-id="15677-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="15677-144">Wybierz odpowiednie urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="15677-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="15677-145">Filtruj według zasad woluminu lub kopii zapasowej dla kopii zapasowej hello, że chcesz tooselect.</span><span class="sxs-lookup"><span data-stu-id="15677-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="15677-146">Kliknij przycisk **Zastosuj** tooexecute tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="15677-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="15677-147">Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="15677-149">Wybierz i rozwiń zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-149">Select and expand a backup set.</span></span> <span data-ttu-id="15677-150">Możesz teraz przeglądać hello zestawy kopii zapasowych według hello woluminów, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="15677-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="15677-151">Witaj **przywrócić** i **usunąć** opcje są dostępne za pośrednictwem menu kontekstowe hello (kliknij prawym przyciskiem myszy) dla hello zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="15677-152">Każda z tych akcji można wykonywać na powitania zestawu kopii zapasowych wybrany.</span><span class="sxs-lookup"><span data-stu-id="15677-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="15677-154">Usuń zestaw kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="15677-154">Delete a backup set</span></span>
<span data-ttu-id="15677-155">Usunięcie kopii zapasowej, jeśli nie chcesz już tooretain hello danych skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="15677-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="15677-156">Wykonaj następujące kroki toodelete zestawu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="15677-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="15677-157">toodelete zestawu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="15677-157">toodelete a backup set</span></span>
 <span data-ttu-id="15677-158">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="15677-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="15677-159">Filtrować hello wybory w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15677-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="15677-160">Określ zakres czasu hello.</span><span class="sxs-lookup"><span data-stu-id="15677-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="15677-161">Wybierz odpowiednie urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="15677-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="15677-162">Filtruj według zasad woluminu lub kopii zapasowej dla kopii zapasowej hello, że chcesz tooselect.</span><span class="sxs-lookup"><span data-stu-id="15677-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="15677-163">Kliknij przycisk **Zastosuj** tooexecute tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="15677-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="15677-164">Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="15677-166">Wybierz i rozwiń zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-166">Select and expand a backup set.</span></span> <span data-ttu-id="15677-167">Możesz teraz przeglądać hello zestawy kopii zapasowych według hello woluminów, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="15677-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="15677-168">Witaj **przywrócić** i **usunąć** opcje są dostępne za pośrednictwem menu kontekstowe hello (kliknij prawym przyciskiem myszy) dla hello zestawu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="15677-169">Kliknij prawym przyciskiem myszy wybrane hello zestawu kopii zapasowych i wybierz z menu kontekstowego hello **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="15677-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="15677-171">Po wyświetleniu monitu o potwierdzenie, przejrzyj informacje wyświetlane hello i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="15677-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="15677-172">Witaj wybranej kopii zapasowej jest trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="15677-172">hello selected backup is deleted permanently.</span></span>

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="15677-174">Podczas usuwania hello jest w toku i zostało pomyślnie zakończone, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="15677-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="15677-175">Po usunięciu hello jest wykonywana, odśwież zapytanie hello na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="15677-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="15677-176">zestaw kopii zapasowych Hello usunięte nie będzie dłużej widoczny na liście hello zestawów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15677-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="15677-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15677-178">Next steps</span></span>
* <span data-ttu-id="15677-179">Dowiedz się, jak za[Użyj hello toorestore katalogu kopii zapasowej urządzenia z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="15677-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="15677-180">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="15677-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

