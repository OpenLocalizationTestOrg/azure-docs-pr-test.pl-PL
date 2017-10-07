---
title: samouczek tworzenia kopii zapasowej Azure StorSimple wirtualnego tablicy aaaMicrosoft | Dokumentacja firmy Microsoft
description: "Opisuje sposób udziały tooback się tablicy wirtualnego StorSimple i woluminów."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="c8170-103">Tworzyć kopie zapasowe udziały lub woluminy na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="c8170-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="c8170-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c8170-104">Overview</span></span>

<span data-ttu-id="c8170-105">Witaj tablicy wirtualne StorSimple jest hybrydowe chmury magazynu lokalnego urządzenia wirtualnego skonfigurowanego jako serwer plików lub serwera iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c8170-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="c8170-106">Tablica wirtualnego Hello umożliwia toocreate użytkownika hello zaplanowanych, jak i ręczne tworzenie kopii zapasowych wszystkich hello udziały lub woluminy na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="c8170-107">Gdy skonfigurowany jako serwer plików, również umożliwia odzyskiwanie na poziomie elementu.</span><span class="sxs-lookup"><span data-stu-id="c8170-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="c8170-108">W tym samouczku opisano sposób planowania toocreate i ręcznego tworzenia kopii zapasowych i wykonać odzyskiwanie na poziomie elementu toorestore usuniętego pliku w sieci wirtualnej macierzy.</span><span class="sxs-lookup"><span data-stu-id="c8170-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="c8170-109">Ten samouczek dotyczy toohello StorSimple wirtualnego tablic tylko.</span><span class="sxs-lookup"><span data-stu-id="c8170-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="c8170-110">Informacji o serii 8000, zbyt zobaczyć[tworzenia kopii zapasowej urządzenie 8000 series](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="c8170-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="c8170-111">Wykonaj kopię zapasową woluminów i udziałów</span><span class="sxs-lookup"><span data-stu-id="c8170-111">Back up shares and volumes</span></span>

<span data-ttu-id="c8170-112">Kopie zapasowe zapewnia ochronę w momencie, ułatwia odzyskiwanie i zminimalizować czas przywracania dla woluminów i udziałów.</span><span class="sxs-lookup"><span data-stu-id="c8170-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="c8170-113">Można utworzyć kopię zapasową udziału lub wolumin w urządzeniu StorSimple na dwa sposoby: **zaplanowane** lub **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="c8170-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="c8170-114">Każdej z metod hello jest omówiona w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="c8170-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="c8170-115">Zmiana czasu rozpoczęcia tworzenia kopii zapasowej hello</span><span class="sxs-lookup"><span data-stu-id="c8170-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="c8170-116">W tej wersji zaplanowane kopie zapasowe są tworzone przez zasady domyślne, który jest uruchamiany codziennie o określonej godzinie i tworzy kopię zapasową wszystkich hello udziały lub woluminy na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="c8170-117">Nie jest możliwe toocreate zasady niestandardowe dla zaplanowanych kopii zapasowych w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="c8170-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="c8170-118">Tablica wirtualnego StorSimple ma domyślne zasady tworzenia kopii zapasowej, który rozpoczyna się o określonej godzinie dnia (22:30) i tworzy kopię zapasową wszystkich hello udziały lub woluminy na urządzeniu hello raz dziennie.</span><span class="sxs-lookup"><span data-stu-id="c8170-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="c8170-119">Możesz zmienić czas hello, na które hello kopii zapasowej zostanie uruchomiony, ale częstotliwość hello i hello przechowywania (który określa hello liczbę kopii zapasowych tooretain) nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="c8170-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="c8170-120">Podczas te kopie zapasowe całego urządzenia wirtualnego hello jest kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="c8170-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="c8170-121">To może potencjalnie wpłynąć na wydajność hello hello urządzenia i wpływać na powitania obciążeń wdrożonych na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="c8170-122">Dlatego zaleca się zaplanować te kopie zapasowe dla poza godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="c8170-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="c8170-123">toochange hello domyślnego tworzenia kopii zapasowej godzina rozpoczęcia, wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c8170-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="c8170-124">Witaj toochange godziny rozpoczęcia dla zasad tworzenia kopii zapasowej hello domyślne</span><span class="sxs-lookup"><span data-stu-id="c8170-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="c8170-125">Przejdź za**urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="c8170-125">Go too**Devices**.</span></span> <span data-ttu-id="c8170-126">zostanie wyświetlona lista Hello urządzeń zarejestrowanych przy użyciu usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8170-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Przejdź toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="c8170-128">Wybierz, a następnie kliknij urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8170-128">Select and click your device.</span></span> <span data-ttu-id="c8170-129">Witaj **ustawienia** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="c8170-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="c8170-130">Przejdź za**Zarządzaj > zasady tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c8170-130">Go too**Manage > Backup policies**.</span></span>
   
    ![Wybierz urządzenie](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="c8170-132">W hello **zasady tworzenia kopii zapasowej** bloku hello domyślny czas rozpoczęcia jest 22:30.</span><span class="sxs-lookup"><span data-stu-id="c8170-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="c8170-133">Można określić hello nową godzinę rozpoczęcia dla harmonogramu dziennego hello w strefie czasowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8170-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Przejdź toobackup zasad](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="c8170-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c8170-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="c8170-136">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="c8170-136">Take a manual backup</span></span>

<span data-ttu-id="c8170-137">Ponadto tooscheduled kopie zapasowe, można wykonać ręcznie (na żądanie) kopii zapasowej danych urządzenia w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="c8170-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="c8170-138">toocreate ręcznego tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="c8170-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="c8170-139">Przejdź za**urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="c8170-139">Go too**Devices**.</span></span> <span data-ttu-id="c8170-140">Wybierz urządzenie, a następnie kliknij prawym przyciskiem myszy **...**  w prawej hello w hello zaznaczonego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c8170-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="c8170-141">Wybierz z menu kontekstowego hello **utworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c8170-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Przejdź tootake kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="c8170-143">W hello **utworzenia kopii zapasowej** bloku, kliknij przycisk **utworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c8170-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="c8170-144">Zostanie utworzona kopia zapasowa, wszystkie udziały hello na powitania serwera plików lub wszystkie woluminy hello na serwerze iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c8170-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![Uruchamianie tworzenia kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="c8170-146">Rozpoczęcia tworzenia kopii zapasowej na żądanie i zobacz, czy zadanie tworzenia kopii zapasowej została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c8170-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![Uruchamianie tworzenia kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="c8170-148">Po pomyślnym ukończeniu zadania hello zostanie wyświetlony ponownie.</span><span class="sxs-lookup"><span data-stu-id="c8170-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="c8170-149">następnie uruchamia proces tworzenia kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-149">hello backup process then starts.</span></span>
   
    ![Utworzono zadanie kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="c8170-151">postęp hello tootrack hello kopii zapasowych i Przeglądaj hello szczegóły zadania, kliknij powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="c8170-152">Powoduje to przejście zbyt **szczegóły zadania**.</span><span class="sxs-lookup"><span data-stu-id="c8170-152">This takes you too **Job details**.</span></span>
   
     ![Szczegóły zadania kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="c8170-154">Po wykonaniu kopii zapasowej hello Przejdź zbyt**zarządzania > katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c8170-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="c8170-155">Zobaczysz migawkę chmury dla wszystkich udziałów hello (lub woluminów) na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c8170-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Zakończono tworzenie kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="c8170-157">Wyświetlanie istniejących kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="c8170-157">View existing backups</span></span>
<span data-ttu-id="c8170-158">tooview hello istniejących kopii zapasowych, wykonaj następujące kroki w portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="c8170-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="c8170-159">tooview istniejące kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="c8170-159">tooview existing backups</span></span>

1. <span data-ttu-id="c8170-160">Przejdź za**urządzeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="c8170-160">Go too**Devices** blade.</span></span> <span data-ttu-id="c8170-161">Wybierz, a następnie kliknij urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8170-161">Select and click your device.</span></span> <span data-ttu-id="c8170-162">W hello **ustawienia** bloku Przejdź zbyt**zarządzania > katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c8170-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Przejdź do katalogu toobackup](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="c8170-164">Określ powitania po toobe kryteria używane do filtrowania:</span><span class="sxs-lookup"><span data-stu-id="c8170-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="c8170-165">**Zakres czasu** — może być **ostatnich 1 godzina**, **ostatnich 24 godzin**, **ostatnie 7 dni**, **w ciągu ostatnich 30 dni**, **ciągu ostatniego roku**, i **Data niestandardowa**.</span><span class="sxs-lookup"><span data-stu-id="c8170-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="c8170-166">**Urządzenia** — wybierz z listy hello serwerów plików lub serwery iSCSI zarejestrowana przy użyciu usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8170-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="c8170-167">**Zainicjowano** — może być automatycznie **zaplanowane** (przy użyciu zasad tworzenia kopii zapasowej) lub **ręcznie** zainicjujesz ().</span><span class="sxs-lookup"><span data-stu-id="c8170-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Kopie zapasowe filtru](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="c8170-169">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="c8170-169">Click **Apply**.</span></span> <span data-ttu-id="c8170-170">Witaj wyfiltrowanej listy kopii zapasowych jest wyświetlana w hello **katalog kopii zapasowej** bloku.</span><span class="sxs-lookup"><span data-stu-id="c8170-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="c8170-171">Uwaga tylko 100 elementów kopii zapasowej mogą być wyświetlane w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="c8170-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Zaktualizowano katalogu kopii zapasowej](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="c8170-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8170-173">Next steps</span></span>

<span data-ttu-id="c8170-174">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="c8170-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

