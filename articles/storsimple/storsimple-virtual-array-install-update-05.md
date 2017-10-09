---
title: aaaInstall aktualizacji 0,5 w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toouse hello tablicy wirtualnego StorSimple web UI tooapply aktualizacji za pomocą hello Azure portal i poprawki — metoda"
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="4d3ba-103">Zainstaluj aktualizację 0,5 na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="4d3ba-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="4d3ba-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4d3ba-104">Overview</span></span>

<span data-ttu-id="4d3ba-105">W tym artykule opisano hello kroki wymagane tooinstall aktualizacji 0,5 na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="4d3ba-106">Należy tookeep aktualizacji lub poprawek oprogramowania tooapply tablica wirtualnego StorSimple aktualne.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="4d3ba-107">Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="4d3ba-108">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="4d3ba-109">Po hello woluminy lub udziały są w trybie offline, należy również wziąć ręcznego tworzenia kopii zapasowej hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="4d3ba-110">Aktualizacja 0,5 odpowiada za**10.0.10290.0** wersji oprogramowania na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="4d3ba-111">Dla informacji na temat nowości w ramach tej aktualizacji, przejdź zbyt[informacje o wersji dla aktualizacji 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="4d3ba-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="4d3ba-112">Jeśli używasz wersji Update 0.2 lub później, zaleca się, że należy zainstalować aktualizacje hello za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="4d3ba-113">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem tooinstall interfejsu użytkownika sieci web lokalnego hello aktualizacji 0,5.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="4d3ba-114">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="4d3ba-115">Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="4d3ba-116">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4d3ba-116">Use hello Azure portal</span></span>

<span data-ttu-id="4d3ba-117">Z aktualizacji, 0,2 i nowszymi wersjami, zaleca się zainstalowanie aktualizacji za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="4d3ba-118">Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="4d3ba-119">Ta procedura ma toocomplete około 7 minut.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="4d3ba-120">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="4d3ba-121">Po hello instalacja jest pełny, przejdź do pozycji tooyour usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4d3ba-122">Wybierz **urządzeń** a następnie wybierz opcję i kliknij urządzenie powitania po zaktualizowaniu.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="4d3ba-123">Przejdź za**Ustawienia > Zarządzaj > aktualizacji urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="4d3ba-124">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="4d3ba-125">Użyj lokalne powitania interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="4d3ba-125">Use hello local web UI</span></span>

<span data-ttu-id="4d3ba-126">Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="4d3ba-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="4d3ba-127">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="4d3ba-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="4d3ba-128">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="4d3ba-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="4d3ba-129">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="4d3ba-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="4d3ba-130">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="4d3ba-131">poprawki lub aktualizacji hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="4d3ba-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="4d3ba-132">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4d3ba-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="4d3ba-133">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="4d3ba-134">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="4d3ba-135">Wprowadź **4021576** aktualizacja 0,5, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="4d3ba-136">Witaj poprawka zostanie wyświetlona na liście, na przykład **aktualizacji tablicy wirtualne StorSimple 0,5**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="4d3ba-138">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-138">Click **Download**.</span></span> 

5. <span data-ttu-id="4d3ba-139">Powinny pojawić się dwa pliki toodownload, *msu* i *cab* pliku.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="4d3ba-140">Pobierz każdego folderu tooa tych plików.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="4d3ba-141">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="4d3ba-142">Otwórz folder hello, w którym znajdują się pliki hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="4d3ba-143">![Pliki w pakiecie hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="4d3ba-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="4d3ba-144">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="4d3ba-144">You see:</span></span>
    -  <span data-ttu-id="4d3ba-145">Plik pakietu autonomicznego aktualizacji firmy Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="4d3ba-146">Ten plik jest używane tooupdate hello urządzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="4d3ba-147">Plik pakietu agenta monitorowania serwera Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="4d3ba-148">Ten plik jest używany tooupdate hello monitorowania i diagnostyki usługi (MDS) agenta.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="4d3ba-149">Kliknij dwukrotnie plik cab hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-149">Double-click hello cab file.</span></span> <span data-ttu-id="4d3ba-150">Msi jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-150">A .msi is displayed.</span></span> <span data-ttu-id="4d3ba-151">Wybierz hello pliku, kliknij prawym przyciskiem myszy, a następnie **wyodrębnić** hello pliku.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="4d3ba-152">Użyje hello _.msi_ pliku tooupdate hello agenta.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Wyodrębnij plik aktualizacji agenta usług MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="4d3ba-154">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="4d3ba-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="4d3ba-155">Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="4d3ba-156">Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="4d3ba-157">Ta procedura ma mniej niż 2 minuty toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="4d3ba-158">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="4d3ba-159">poprawki lub aktualizacji hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="4d3ba-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="4d3ba-160">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="4d3ba-162">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="4d3ba-163">Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="4d3ba-164">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-164">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="4d3ba-166">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-166">A warning is displayed.</span></span> <span data-ttu-id="4d3ba-167">Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="4d3ba-168">Kliknij ikonę znacznika wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-168">Click hello check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="4d3ba-170">Uruchamia Hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-170">hello update starts.</span></span> <span data-ttu-id="4d3ba-171">Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="4d3ba-172">Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-172">hello local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="4d3ba-174">Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="4d3ba-175">tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="4d3ba-176">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10290.0** aktualizacji 0,5.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4d3ba-177">Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="4d3ba-178">Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10290** i hello Azure raporty portalu **10.0.10290.0** dla hello tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="4d3ba-180">Witaj następnym krokiem jest tooupdate hello MDS agenta.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="4d3ba-181">W hello **aktualizacji oprogramowania** pozycję Przejdź toohello **ścieżka pliku aktualizacji** i Przeglądaj toohello `GenevaMonitoringAgentPackageInstaller.msi` pliku.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="4d3ba-182">Powtórz kroki od 2 do 4.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-182">Repeat steps 2-4.</span></span> <span data-ttu-id="4d3ba-183">Po ponownym uruchomieniu hello wirtualnego tablicy, zaloguj się do lokalne powitania interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="4d3ba-184">Aktualizacja Hello jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="4d3ba-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d3ba-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d3ba-185">Next steps</span></span>

<span data-ttu-id="4d3ba-186">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="4d3ba-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

