---
title: aaaInstall aktualizacji 0,6 w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="b36de-103">Zainstaluj aktualizację 0,6 na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="b36de-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b36de-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b36de-104">Overview</span></span>

<span data-ttu-id="b36de-105">W tym artykule opisano hello kroki wymagane tooinstall aktualizacji 0,6 na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b36de-105">This article describes hello steps required tooinstall Update 0.6 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="b36de-106">Należy zastosować tookeep aktualizacji lub poprawek oprogramowania hello aktualne tablica wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b36de-106">You apply hello software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="b36de-107">Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b36de-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="b36de-108">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="b36de-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="b36de-109">Po hello woluminy lub udziały są w trybie offline, należy również wziąć ręcznego tworzenia kopii zapasowej hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b36de-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="b36de-110">Aktualizacja 0,6 odpowiada za**10.0.10293.0** wersji oprogramowania na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b36de-110">Update 0.6 corresponds too**10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="b36de-111">Dla informacji na temat nowości w ramach tej aktualizacji, przejdź zbyt[informacje o wersji dla aktualizacji 0,6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="b36de-111">For information on what is new in this update, go too[Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="b36de-112">Jeśli używasz wersji Update 0.2 lub później, zaleca się, że należy zainstalować aktualizacje hello za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b36de-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="b36de-113">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem tooinstall interfejsu użytkownika sieci web w lokalnej hello 0,6 aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b36de-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.6.</span></span>
>
> - <span data-ttu-id="b36de-114">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b36de-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="b36de-115">Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="b36de-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="b36de-116">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b36de-116">Use hello Azure portal</span></span>

<span data-ttu-id="b36de-117">Z aktualizacji, 0,2 i nowszymi wersjami, zaleca się zainstalowanie aktualizacji za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b36de-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="b36de-118">Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="b36de-119">Ta procedura ma toocomplete około 7 minut.</span><span class="sxs-lookup"><span data-stu-id="b36de-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="b36de-120">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="b36de-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="b36de-121">Po hello instalacja jest pełny, przejdź do pozycji tooyour usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b36de-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="b36de-122">Wybierz **urządzeń** a następnie wybierz opcję i kliknij urządzenie powitania po zaktualizowaniu.</span><span class="sxs-lookup"><span data-stu-id="b36de-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="b36de-123">Przejdź za**Ustawienia > Zarządzaj > aktualizacji urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="b36de-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="b36de-124">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="b36de-124">hello displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="b36de-125">Użyj lokalne powitania interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="b36de-125">Use hello local web UI</span></span>

<span data-ttu-id="b36de-126">Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="b36de-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="b36de-127">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="b36de-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="b36de-128">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="b36de-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="b36de-129">Pobierz hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="b36de-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="b36de-130">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="b36de-131">poprawki lub aktualizacji hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="b36de-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="b36de-132">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b36de-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="b36de-133">Jeśli używasz hello wykazu usługi Microsoft Update dla hello na tym komputerze po raz pierwszy, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="b36de-133">If you are using hello Microsoft Update Catalog for hello first time on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="b36de-134">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload.</span><span class="sxs-lookup"><span data-stu-id="b36de-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="b36de-135">Wprowadź **4023268** aktualizacja 0,6, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="b36de-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="b36de-136">Witaj poprawka zostanie wyświetlona na liście, na przykład **aktualizacji tablicy wirtualne StorSimple 0,6**.</span><span class="sxs-lookup"><span data-stu-id="b36de-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="b36de-138">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="b36de-138">Click **Download**.</span></span>

5. <span data-ttu-id="b36de-139">Powinny pojawić się pięć toodownload plików.</span><span class="sxs-lookup"><span data-stu-id="b36de-139">You should see five files toodownload.</span></span> <span data-ttu-id="b36de-140">Pobierz każdego folderu tooa tych plików.</span><span class="sxs-lookup"><span data-stu-id="b36de-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="b36de-141">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="b36de-142">Otwórz folder hello, w którym znajdują się pliki hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="b36de-143">![Pliki w pakiecie hello](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="b36de-143">![Files in hello package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="b36de-144">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="b36de-144">You see:</span></span>
    -  <span data-ttu-id="b36de-145">Plik pakietu autonomicznego aktualizacji firmy Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="b36de-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="b36de-146">Ten plik jest używane tooupdate hello urządzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="b36de-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="b36de-147">Plik pakietu agenta monitorowania serwera Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="b36de-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="b36de-148">Ten plik jest używany tooupdate hello monitorowania i diagnostyki usługi (MDS) agenta.</span><span class="sxs-lookup"><span data-stu-id="b36de-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="b36de-149">Kliknij dwukrotnie plik cab hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-149">Double-click hello cab file.</span></span> <span data-ttu-id="b36de-150">A _.msi_ jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="b36de-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="b36de-151">Wybierz hello pliku, kliknij prawym przyciskiem myszy, a następnie **wyodrębnić** hello pliku.</span><span class="sxs-lookup"><span data-stu-id="b36de-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="b36de-152">Użyj hello _.msi_ pliku tooupdate hello agenta.</span><span class="sxs-lookup"><span data-stu-id="b36de-152">You use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Wyodrębnij plik aktualizacji agenta usług MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="b36de-154">Nie trzeba tooupdate hello MDS agenta w przypadku korzystania z aktualizacji StorSimple 0,5 (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="b36de-154">You do not need tooupdate hello MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="b36de-155">Trzy pliki, które zawierają krytycznych aktualizacji zabezpieczeń systemu Windows, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, i `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="b36de-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="b36de-156">Zainstaluj hello aktualizacja lub poprawka hello</span><span class="sxs-lookup"><span data-stu-id="b36de-156">Install hello update or hello hotfix</span></span>

<span data-ttu-id="b36de-157">Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b36de-157">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="b36de-158">Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="b36de-158">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="b36de-159">Ta procedura trwa około 12 minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b36de-159">This procedure takes approximately 12 minutes toocomplete.</span></span> <span data-ttu-id="b36de-160">Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="b36de-160">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="b36de-161">poprawki lub aktualizacji hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="b36de-161">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="b36de-162">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="b36de-162">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="b36de-163">Zanotuj hello wersji oprogramowania, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="b36de-163">Make a note of hello software version that you are running.</span></span> <span data-ttu-id="b36de-164">Jeśli używasz **10.0.10290.0**, nie trzeba tooupdate hello MDS agenta w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="b36de-164">If you are running **10.0.10290.0**, you do not need tooupdate hello MDS agent in step 6.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="b36de-166">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-166">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="b36de-167">Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="b36de-167">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="b36de-168">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="b36de-168">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="b36de-170">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="b36de-170">A warning is displayed.</span></span> <span data-ttu-id="b36de-171">Podany hello wirtualnego tablicy jest urządzeniem jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="b36de-171">Given hello virtual array is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="b36de-172">Kliknij ikonę znacznika wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="b36de-172">Click hello check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="b36de-174">Uruchamia Hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b36de-174">hello update starts.</span></span> <span data-ttu-id="b36de-175">Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="b36de-175">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="b36de-176">Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.</span><span class="sxs-lookup"><span data-stu-id="b36de-176">hello local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="b36de-178">Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="b36de-178">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="b36de-179">tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="b36de-179">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="b36de-180">Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10293** 0,6 aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b36de-180">hello displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b36de-181">Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b36de-181">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="b36de-182">Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10293** i hello Azure raporty portalu **10.0.10293.0** dla hello tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="b36de-182">For example, hello local web UI reports **10.0.0.0.0.10293** and hello Azure portal reports **10.0.10293.0** for hello same version.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="b36de-184">Pomiń ten krok w przypadku korzystania z aktualizacji tablicy wirtualne StorSimple 0,5 (**10.0.10290.0**) przed zastosowaniem tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b36de-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="b36de-185">Należy zanotować wersji oprogramowania hello w kroku 1 przed rozpoczęciem tooupdate.</span><span class="sxs-lookup"><span data-stu-id="b36de-185">You made a note of hello software version in step 1 before you began tooupdate.</span></span> <span data-ttu-id="b36de-186">Podczas uruchamiania aktualizacji 0,5, agenta usług MDS jest już aktualny.</span><span class="sxs-lookup"><span data-stu-id="b36de-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="b36de-187">Jeśli używasz tooUpdate wcześniejszych wersji 0,5 oprogramowania hello następnego kroku dla Ciebie jest tooupdate hello MDS agenta.</span><span class="sxs-lookup"><span data-stu-id="b36de-187">If you are running a software version prior tooUpdate 0.5, hello next step for you is tooupdate hello MDS agent.</span></span> <span data-ttu-id="b36de-188">W hello **aktualizacji oprogramowania** pozycję Przejdź toohello **ścieżka pliku aktualizacji** i Przeglądaj toohello `GenevaMonitoringAgentPackageInstaller.msi` pliku.</span><span class="sxs-lookup"><span data-stu-id="b36de-188">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="b36de-189">Powtórz kroki od 2 do 4.</span><span class="sxs-lookup"><span data-stu-id="b36de-189">Repeat steps 2-4.</span></span> <span data-ttu-id="b36de-190">Po ponownym uruchomieniu hello wirtualnego tablicy, zaloguj się do lokalne powitania interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36de-190">After hello virtual array restarts, sign into hello local web UI.</span></span>

7. <span data-ttu-id="b36de-191">Powtórz kroki od poprawki zabezpieczeń systemu Windows hello tooinstall 2-4 przy użyciu plików `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, i `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="b36de-191">Repeat step 2-4 tooinstall hello Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="b36de-192">Tablica wirtualnego Hello ponownych uruchomień po zakończeniu każdej instalacji i należy toosign do lokalne powitania interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36de-192">hello virtual array restarts after each install and you need toosign into hello local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b36de-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b36de-193">Next steps</span></span>

<span data-ttu-id="b36de-194">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b36de-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

