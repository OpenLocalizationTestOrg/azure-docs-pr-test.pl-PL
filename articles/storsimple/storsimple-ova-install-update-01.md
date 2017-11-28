---
title: Aktualizacje aaaInstall w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toouse hello tablicy wirtualnego StorSimple web UI tooapply aktualizacji przy użyciu metody hello portalu i poprawki"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="f2b6b-103">Instalowanie aktualizacji na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="f2b6b-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="f2b6b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f2b6b-104">Overview</span></span>
<span data-ttu-id="f2b6b-105">W tym artykule opisano hello kroki tooinstall wymagane aktualizacje na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="f2b6b-106">Należy tookeep aktualizacji lub poprawek oprogramowania tooapply tablica wirtualnego StorSimple aktualne.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="f2b6b-107">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="f2b6b-108">Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="f2b6b-109">Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="f2b6b-110">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2b6b-111">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem hello lokalnej sieci web UI tooinstall update 0.3.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="f2b6b-112">Jeśli używasz wersji Update 0.2, zaleca się zainstalowanie aktualizacji hello za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="f2b6b-113">Użyj lokalne powitania interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="f2b6b-113">Use hello local web UI</span></span>
<span data-ttu-id="f2b6b-114">Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="f2b6b-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="f2b6b-115">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="f2b6b-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="f2b6b-116">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="f2b6b-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="f2b6b-117">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="f2b6b-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="f2b6b-118">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="f2b6b-119">poprawki lub aktualizacji hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="f2b6b-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="f2b6b-120">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f2b6b-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f2b6b-121">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="f2b6b-122">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="f2b6b-123">Wprowadź **3182061** aktualizacja 0.3, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="f2b6b-124">Witaj poprawka zostanie wyświetlona na liście, na przykład **StorSimple wirtualnej tablicy Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="f2b6b-126">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-126">Click **Add**.</span></span> <span data-ttu-id="f2b6b-127">Witaj aktualizacja została dodana toohello koszyka.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="f2b6b-128">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="f2b6b-129">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-129">Click **Download**.</span></span> <span data-ttu-id="f2b6b-130">Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="f2b6b-131">Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieszczane w podfolderze o hello takie same nazwy co hello update.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="f2b6b-132">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="f2b6b-133">Otwórz hello skopiować folder, plik pakietu autonomicznego aktualizacji firmy Microsoft powinna zostać wyświetlona `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="f2b6b-134">Ten plik jest używany tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="f2b6b-135">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="f2b6b-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="f2b6b-136">Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="f2b6b-137">Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="f2b6b-138">Ta procedura ma mniej niż 2 minuty toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="f2b6b-139">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="f2b6b-140">poprawki lub aktualizacji hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="f2b6b-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="f2b6b-141">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="f2b6b-143">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="f2b6b-144">Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="f2b6b-145">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-145">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="f2b6b-147">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-147">A warning is displayed.</span></span> <span data-ttu-id="f2b6b-148">Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="f2b6b-149">Kliknij ikonę znacznika wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-149">Click hello check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="f2b6b-151">Uruchamia Hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-151">hello update starts.</span></span> <span data-ttu-id="f2b6b-152">Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="f2b6b-153">Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-153">hello local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="f2b6b-155">Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="f2b6b-156">tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="f2b6b-157">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10288.0** for Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f2b6b-158">Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="f2b6b-159">Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10288** i hello Azure raporty portalu klasycznego **10.0.10288.0** dla hello tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="f2b6b-161">Witaj Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f2b6b-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="f2b6b-162">Uruchomiona Update 0.2, zaleca się zainstalowanie aktualizacji za pomocą hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="f2b6b-163">Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="f2b6b-164">Ta procedura ma toocomplete około 7 minut.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="f2b6b-165">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="f2b6b-166">Po hello instalacja została zakończona, (określone przez stan zadania w skali 100%), przejdź zbyt**urządzenia > konserwacja > aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="f2b6b-167">Wersja oprogramowania Hello wyświetlane powinna mieć 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="f2b6b-167">hello displayed software version should be 10.0.10288.0.</span></span>

![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="f2b6b-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2b6b-169">Next steps</span></span>
<span data-ttu-id="f2b6b-170">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f2b6b-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

