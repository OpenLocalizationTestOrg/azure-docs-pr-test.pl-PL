---
title: "Zainstaluj aktualizację 0,6 w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące używania interfejsu użytkownika sieci web tablicy wirtualnego StorSimple do stosowania aktualizacji za pomocą metody Azure portal i poprawki"
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
ms.openlocfilehash: 111976cd684561f5bc63b92f09a20470fe3036d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="913a3-103">Zainstaluj aktualizację 0,6 na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="913a3-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="913a3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="913a3-104">Overview</span></span>

<span data-ttu-id="913a3-105">W tym artykule opisano kroki wymagane do zainstalowania aktualizacji 0,6 tablica wirtualnego StorSimple, za pośrednictwem lokalnego interfejsu użytkownika sieci web i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="913a3-105">This article describes the steps required to install Update 0.6 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="913a3-106">Należy zastosować aktualizacje oprogramowania lub poprawek, aby zapewnić aktualność tablica wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="913a3-106">You apply the software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="913a3-107">Przed zainstalowaniem aktualizacji zalecamy wykonanie woluminy lub udziały w trybie offline na hoście pierwszy, a następnie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="913a3-108">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="913a3-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="913a3-109">Po woluminy lub udziały są w trybie offline, należy również wziąć ręcznego tworzenia kopii zapasowych urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="913a3-110">Aktualizacja 0,6 odpowiada **10.0.10293.0** wersji oprogramowania na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="913a3-110">Update 0.6 corresponds to **10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="913a3-111">Aby uzyskać informacji na temat nowości w ramach tej aktualizacji, przejdź do [informacje o wersji dla aktualizacji 0,6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="913a3-111">For information on what is new in this update, go to [Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="913a3-112">Jeśli używasz wersji Update 0.2 lub później, zaleca się, że musisz zainstalować aktualizacje za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="913a3-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="913a3-113">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawek za pomocą lokalnego interfejsu użytkownika sieci web do zainstalowania aktualizacji 0,6.</span><span class="sxs-lookup"><span data-stu-id="913a3-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.6.</span></span>
>
> - <span data-ttu-id="913a3-114">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="913a3-115">Biorąc pod uwagę, że tablica wirtualne StorSimple jest urządzeniem jeden węzeł, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="913a3-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="913a3-116">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="913a3-116">Use the Azure portal</span></span>

<span data-ttu-id="913a3-117">Z aktualizacji, 0,2 i nowszymi wersjami, zaleca się zainstalowanie aktualizacji za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="913a3-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="913a3-118">Procedury portalu wymaga od użytkownika skanowania, Pobierz i zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="913a3-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="913a3-119">Ta procedura trwa około 7 minut do wykonania.</span><span class="sxs-lookup"><span data-stu-id="913a3-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="913a3-120">Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="913a3-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="913a3-121">Po zakończeniu instalacji, przejdź do usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="913a3-122">Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk po zaktualizowaniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="913a3-123">Przejdź do **Ustawienia > Zarządzaj > aktualizacji urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="913a3-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="913a3-124">Wersja oprogramowania wyświetlane **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="913a3-124">The displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="913a3-125">Użyj lokalnego interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="913a3-125">Use the local web UI</span></span>

<span data-ttu-id="913a3-126">Istnieją dwa kroki, korzystając z lokalnego interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="913a3-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="913a3-127">Pobieranie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="913a3-128">Zainstalowanie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="913a3-129">Pobieranie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-129">Download the update or the hotfix</span></span>

<span data-ttu-id="913a3-130">Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="913a3-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="913a3-131">Aby pobrać aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="913a3-132">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="913a3-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="913a3-133">Jeśli korzystasz z wykazu usługi Microsoft Update po raz pierwszy na tym komputerze, kliknij przycisk **zainstalować** monit o zainstalowanie dodatku wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="913a3-133">If you are using the Microsoft Update Catalog for the first time on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="913a3-134">W polu wyszukiwania z wykazu usługi Microsoft Update wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki, którą chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="913a3-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="913a3-135">Wprowadź **4023268** aktualizacja 0,6, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="913a3-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="913a3-136">Poprawka zostanie wyświetlona na liście, na przykład **aktualizacji tablicy wirtualne StorSimple 0,6**.</span><span class="sxs-lookup"><span data-stu-id="913a3-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="913a3-138">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="913a3-138">Click **Download**.</span></span>

5. <span data-ttu-id="913a3-139">Powinny pojawić się pięć plików do pobrania.</span><span class="sxs-lookup"><span data-stu-id="913a3-139">You should see five files to download.</span></span> <span data-ttu-id="913a3-140">Pobieranie każdej z tych plików w folderze.</span><span class="sxs-lookup"><span data-stu-id="913a3-140">Download each of those files to a folder.</span></span> <span data-ttu-id="913a3-141">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="913a3-142">Otwórz folder, w którym znajdują się pliki.</span><span class="sxs-lookup"><span data-stu-id="913a3-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="913a3-143">![Pliki w pakiecie](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="913a3-143">![Files in the package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="913a3-144">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="913a3-144">You see:</span></span>
    -  <span data-ttu-id="913a3-145">Plik pakietu autonomicznego aktualizacji firmy Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="913a3-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="913a3-146">Ten plik jest używany do aktualizacji oprogramowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913a3-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="913a3-147">Plik pakietu agenta monitorowania serwera Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="913a3-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="913a3-148">Ten plik jest używany do aktualizacji agenta usługi (MDS) monitorowania i diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="913a3-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="913a3-149">Kliknij dwukrotnie plik cab.</span><span class="sxs-lookup"><span data-stu-id="913a3-149">Double-click the cab file.</span></span> <span data-ttu-id="913a3-150">A _.msi_ jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="913a3-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="913a3-151">Wybierz plik, kliknij prawym przyciskiem myszy, a następnie **wyodrębnić** pliku.</span><span class="sxs-lookup"><span data-stu-id="913a3-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="913a3-152">Możesz użyć _.msi_ plik, aby zaktualizować agenta.</span><span class="sxs-lookup"><span data-stu-id="913a3-152">You use the _.msi_ file to update the agent.</span></span>

        ![Wyodrębnij plik aktualizacji agenta usług MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="913a3-154">Nie trzeba zaktualizować agenta MDS, jeśli używasz wersji StorSimple Update 0,5 (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="913a3-154">You do not need to update the MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="913a3-155">Trzy pliki, które zawierają krytycznych aktualizacji zabezpieczeń systemu Windows, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, i `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="913a3-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="913a3-156">Zainstalowanie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-156">Install the update or the hotfix</span></span>

<span data-ttu-id="913a3-157">Przed instalacją aktualizacji lub poprawki upewnij się, że aktualizacja lub poprawka pobierane lokalnie na hoście lub dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="913a3-157">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="913a3-158">Ta metoda umożliwia instalowanie aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="913a3-158">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="913a3-159">Ta procedura może zająć około 12 minut.</span><span class="sxs-lookup"><span data-stu-id="913a3-159">This procedure takes approximately 12 minutes to complete.</span></span> <span data-ttu-id="913a3-160">Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="913a3-160">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="913a3-161">Do zainstalowania aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="913a3-161">To install the update or the hotfix</span></span>

1. <span data-ttu-id="913a3-162">W lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="913a3-162">In the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="913a3-163">Zanotuj wersji oprogramowania, na którym są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="913a3-163">Make a note of the software version that you are running.</span></span> <span data-ttu-id="913a3-164">Jeśli używasz **10.0.10290.0**, nie musisz zaktualizować agenta usług MDS w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="913a3-164">If you are running **10.0.10290.0**, you do not need to update the MDS agent in step 6.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="913a3-166">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku dla aktualizacji lub poprawek.</span><span class="sxs-lookup"><span data-stu-id="913a3-166">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="913a3-167">Możesz również przejść do lokalizacji pliku instalacyjnego aktualizacja lub poprawka umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="913a3-167">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="913a3-168">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="913a3-168">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="913a3-170">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="913a3-170">A warning is displayed.</span></span> <span data-ttu-id="913a3-171">Podana tablica wirtualnego jest urządzeniem jednego węzła, po zastosowaniu aktualizacji, ponownym uruchomieniu urządzenia i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="913a3-171">Given the virtual array is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="913a3-172">Kliknij ikonę znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="913a3-172">Click the check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="913a3-174">Aktualizacja zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="913a3-174">The update starts.</span></span> <span data-ttu-id="913a3-175">Po pomyślnym zaktualizowaniu urządzenia ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="913a3-175">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="913a3-176">Lokalnego interfejsu użytkownika nie jest dostępny w tym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="913a3-176">The local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="913a3-178">Po ponownym uruchomieniu komputera, zostają przeniesieni do **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="913a3-178">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="913a3-179">Aby zweryfikować, że oprogramowanie urządzenia został zaktualizowany w lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="913a3-179">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="913a3-180">Wersja oprogramowania wyświetlane **10.0.0.0.0.10293** 0,6 aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="913a3-180">The displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="913a3-181">Wersje oprogramowania Microsoft raport w sposób nieco inne w lokalnym interfejsu użytkownika sieci web i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="913a3-181">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="913a3-182">Na przykład raporty lokalnego interfejsu użytkownika sieci web **10.0.0.0.0.10293** i raporty portalu Azure **10.0.10293.0** dla tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="913a3-182">For example, the local web UI reports **10.0.0.0.0.10293** and the Azure portal reports **10.0.10293.0** for the same version.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="913a3-184">Pomiń ten krok w przypadku korzystania z aktualizacji tablicy wirtualne StorSimple 0,5 (**10.0.10290.0**) przed zastosowaniem tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="913a3-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="913a3-185">Należy zanotować wersji oprogramowania w kroku 1 przed rozpoczęciem aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="913a3-185">You made a note of the software version in step 1 before you began to update.</span></span> <span data-ttu-id="913a3-186">Podczas uruchamiania aktualizacji 0,5, agenta usług MDS jest już aktualny.</span><span class="sxs-lookup"><span data-stu-id="913a3-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="913a3-187">Jeśli wersja oprogramowania przed aktualizacją 0,5, następnym krokiem dla Ciebie jest aktualizacja agenta usług MDS.</span><span class="sxs-lookup"><span data-stu-id="913a3-187">If you are running a software version prior to Update 0.5, the next step for you is to update the MDS agent.</span></span> <span data-ttu-id="913a3-188">W **aktualizacji oprogramowania** strony, przejdź do **ścieżka pliku aktualizacji** i przejdź do `GenevaMonitoringAgentPackageInstaller.msi` pliku.</span><span class="sxs-lookup"><span data-stu-id="913a3-188">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="913a3-189">Powtórz kroki od 2 do 4.</span><span class="sxs-lookup"><span data-stu-id="913a3-189">Repeat steps 2-4.</span></span> <span data-ttu-id="913a3-190">Po ponownym uruchomieniu wirtualnego tablicy, zaloguj się do lokalnego interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="913a3-190">After the virtual array restarts, sign into the local web UI.</span></span>

7. <span data-ttu-id="913a3-191">Powtórz kroki od 2 do 4 do zainstalowania zabezpieczenia systemu Windows poprawki przy użyciu plików `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, i `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="913a3-191">Repeat step 2-4 to install the Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="913a3-192">Wirtualne tablicy ponownych uruchomień po zakończeniu każdej instalacji i należy zalogować się do lokalnego interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="913a3-192">The virtual array restarts after each install and you need to sign into the local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="913a3-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="913a3-193">Next steps</span></span>

<span data-ttu-id="913a3-194">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="913a3-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

