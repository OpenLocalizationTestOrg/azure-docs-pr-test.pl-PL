---
title: Aktualizacje aaaInstall w macierzy wirtualne Microsoft Azure StorSimple | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toouse hello tablicy wirtualnego StorSimple web UI tooapply aktualizacji przy użyciu metody hello portalu i poprawki"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7424abc7e46d4f08b4eae1194642b263f32c4318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="58247-103">Instalowanie aktualizacji na tablica wirtualnego StorSimple - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="58247-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="58247-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="58247-104">Overview</span></span>

<span data-ttu-id="58247-105">W tym artykule opisano hello kroki tooinstall wymagane aktualizacje na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58247-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="58247-106">Należy tookeep aktualizacji lub poprawek oprogramowania tooapply tablica wirtualnego StorSimple aktualne.</span><span class="sxs-lookup"><span data-stu-id="58247-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="58247-107">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="58247-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="58247-108">Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="58247-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="58247-109">Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="58247-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="58247-110">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="58247-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58247-111">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem hello lokalnej sieci web UI tooinstall update 0.3.</span><span class="sxs-lookup"><span data-stu-id="58247-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="58247-112">Jeśli używasz wersji Update 0.2, zaleca się zainstalowanie aktualizacji hello za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58247-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="58247-113">Użyj lokalne powitania interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="58247-113">Use hello local web UI</span></span>

<span data-ttu-id="58247-114">Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="58247-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="58247-115">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="58247-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="58247-116">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="58247-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="58247-117">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="58247-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="58247-118">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="58247-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="58247-119">poprawki lub aktualizacji hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="58247-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="58247-120">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="58247-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="58247-121">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="58247-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="58247-122">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload.</span><span class="sxs-lookup"><span data-stu-id="58247-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="58247-123">Wprowadź **3182061** aktualizacja 0.3, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="58247-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="58247-124">Witaj poprawka zostanie wyświetlona na liście, na przykład **StorSimple wirtualnej tablicy Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="58247-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="58247-126">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="58247-126">Click **Add**.</span></span> <span data-ttu-id="58247-127">Witaj aktualizacja została dodana toohello koszyka.</span><span class="sxs-lookup"><span data-stu-id="58247-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="58247-128">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="58247-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="58247-129">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="58247-129">Click **Download**.</span></span> <span data-ttu-id="58247-130">Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear.</span><span class="sxs-lookup"><span data-stu-id="58247-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="58247-131">Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieszczane w podfolderze o hello takie same nazwy co hello update.</span><span class="sxs-lookup"><span data-stu-id="58247-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="58247-132">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="58247-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="58247-133">Otwórz hello skopiować folder, plik pakietu autonomicznego aktualizacji firmy Microsoft powinna zostać wyświetlona `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="58247-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="58247-134">Ten plik jest używany tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="58247-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="58247-135">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="58247-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="58247-136">Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="58247-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="58247-137">Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="58247-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="58247-138">Ta procedura ma mniej niż 2 minuty toocomplete.</span><span class="sxs-lookup"><span data-stu-id="58247-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="58247-139">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="58247-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="58247-140">poprawki lub aktualizacji hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="58247-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="58247-141">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="58247-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="58247-143">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="58247-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="58247-144">Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="58247-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="58247-145">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="58247-145">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="58247-147">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="58247-147">A warning is displayed.</span></span> <span data-ttu-id="58247-148">Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="58247-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="58247-149">Kliknij ikonę znacznika wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="58247-149">Click hello check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="58247-151">Uruchamia Hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="58247-151">hello update starts.</span></span> <span data-ttu-id="58247-152">Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="58247-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="58247-153">Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.</span><span class="sxs-lookup"><span data-stu-id="58247-153">hello local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="58247-155">Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="58247-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="58247-156">tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="58247-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="58247-157">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10288.0** for Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="58247-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="58247-158">Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58247-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="58247-159">Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10288** i hello Azure raporty portalu **10.0.10288.0** dla hello tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="58247-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure portal reports **10.0.10288.0** for hello same version.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="58247-161">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="58247-161">Use hello Azure portal</span></span>

<span data-ttu-id="58247-162">Uruchomiona Update 0.2, zaleca się zainstalowanie aktualizacji za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58247-162">If running Update 0.2, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="58247-163">Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="58247-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="58247-164">Ta procedura ma toocomplete około 7 minut.</span><span class="sxs-lookup"><span data-stu-id="58247-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="58247-165">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="58247-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="58247-166">Po hello instalacja jest pełna (co wskazuje stan zadania w skali 100%), przejdź tooyour usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="58247-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="58247-167">Wybierz **urządzeń** a następnie wybierz i kliknij urządzenie hello ma tooupdate z listy hello usługi toothis podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="58247-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="58247-168">W hello **ustawienia** bloku Przejdź zbyt**Zarządzaj** a następnie wybierz opcję **aktualizacji urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="58247-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="58247-169">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="58247-169">hello displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="58247-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58247-170">Next steps</span></span>

<span data-ttu-id="58247-171">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="58247-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

