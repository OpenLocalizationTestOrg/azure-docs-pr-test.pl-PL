---
title: Instalowanie aktualizacji w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Informacje dotyczące używania interfejsu użytkownika sieci web tablicy wirtualnego StorSimple do stosowania aktualizacji za pomocą portalu i poprawki — metoda"
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
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="e7089-103">Instalowanie aktualizacji na tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="e7089-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="e7089-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e7089-104">Overview</span></span>
<span data-ttu-id="e7089-105">W tym artykule opisano kroki wymagane do zainstalowania aktualizacji na tablica wirtualnego StorSimple za pośrednictwem lokalnego interfejsu użytkownika sieci web i za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7089-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="e7089-106">Należy zastosować aktualizacje oprogramowania lub poprawek, aby zapewnić aktualność tablica wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e7089-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="e7089-107">Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7089-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="e7089-108">Biorąc pod uwagę, że tablica wirtualne StorSimple jest urządzeniem jeden węzeł, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.</span><span class="sxs-lookup"><span data-stu-id="e7089-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="e7089-109">Przed zainstalowaniem aktualizacji zalecamy wykonanie woluminy lub udziały w trybie offline na hoście pierwszy, a następnie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7089-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="e7089-110">Pozwala to zmniejszyć możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="e7089-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7089-111">Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawek za pomocą lokalnego interfejsu użytkownika sieci web do zainstalowania update 0.3.</span><span class="sxs-lookup"><span data-stu-id="e7089-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="e7089-112">Jeśli używasz wersji Update 0.2, zaleca się zainstalowanie aktualizacji za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7089-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="e7089-113">Użyj lokalnego interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="e7089-113">Use the local web UI</span></span>
<span data-ttu-id="e7089-114">Istnieją dwa kroki, korzystając z lokalnego interfejsu użytkownika sieci web:</span><span class="sxs-lookup"><span data-stu-id="e7089-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="e7089-115">Pobieranie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="e7089-116">Zainstalowanie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="e7089-117">Pobieranie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-117">Download the update or the hotfix</span></span>
<span data-ttu-id="e7089-118">Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="e7089-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="e7089-119">Aby pobrać aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="e7089-120">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e7089-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="e7089-121">Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="e7089-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="e7089-122">W polu wyszukiwania z wykazu usługi Microsoft Update wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki, którą chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="e7089-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="e7089-123">Wprowadź **3182061** aktualizacja 0.3, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="e7089-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="e7089-124">Poprawka zostanie wyświetlona na liście, na przykład **StorSimple wirtualnej tablicy Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="e7089-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="e7089-126">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e7089-126">Click **Add**.</span></span> <span data-ttu-id="e7089-127">Aktualizacja zostanie dodana do koszyka.</span><span class="sxs-lookup"><span data-stu-id="e7089-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="e7089-128">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="e7089-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="e7089-129">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="e7089-129">Click **Download**.</span></span> <span data-ttu-id="e7089-130">Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e7089-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="e7089-131">Aktualizacje zostaną pobrane do wskazanej lokalizacji i umieszczone w podfolderze o nazwie takiej samej jak aktualizacja.</span><span class="sxs-lookup"><span data-stu-id="e7089-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="e7089-132">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7089-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="e7089-133">Otwórz skopiowany folder, plik pakietu autonomicznego aktualizacji firmy Microsoft powinna zostać wyświetlona `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="e7089-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="e7089-134">Ten plik służy do instalowania aktualizacji lub poprawek.</span><span class="sxs-lookup"><span data-stu-id="e7089-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="e7089-135">Zainstalowanie aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-135">Install the update or the hotfix</span></span>
<span data-ttu-id="e7089-136">Przed instalacją aktualizacji lub poprawki upewnij się, że aktualizacja lub poprawka pobierane lokalnie na hoście lub dostępny za pośrednictwem udziału sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e7089-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="e7089-137">Ta metoda umożliwia instalowanie aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="e7089-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="e7089-138">Ta procedura może zająć mniej niż 2 minut.</span><span class="sxs-lookup"><span data-stu-id="e7089-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="e7089-139">Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="e7089-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="e7089-140">Do zainstalowania aktualizacji lub poprawek</span><span class="sxs-lookup"><span data-stu-id="e7089-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="e7089-141">W lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="e7089-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="e7089-143">W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku dla aktualizacji lub poprawek.</span><span class="sxs-lookup"><span data-stu-id="e7089-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="e7089-144">Możesz również przejść do lokalizacji pliku instalacyjnego aktualizacja lub poprawka umieszczony w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="e7089-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="e7089-145">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="e7089-145">Click **Apply**.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="e7089-147">Zostanie wyświetlone ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="e7089-147">A warning is displayed.</span></span> <span data-ttu-id="e7089-148">Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji, ponownym uruchomieniu urządzenia i brak przestojów.</span><span class="sxs-lookup"><span data-stu-id="e7089-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="e7089-149">Kliknij ikonę znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="e7089-149">Click the check icon.</span></span>
   
   ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="e7089-151">Aktualizacja zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="e7089-151">The update starts.</span></span> <span data-ttu-id="e7089-152">Po pomyślnym zaktualizowaniu urządzenia ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e7089-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="e7089-153">Lokalnego interfejsu użytkownika nie jest dostępny w tym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="e7089-153">The local UI is not accessible in this duration.</span></span>
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="e7089-155">Po ponownym uruchomieniu komputera, zostają przeniesieni do **Zaloguj** strony.</span><span class="sxs-lookup"><span data-stu-id="e7089-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="e7089-156">Aby zweryfikować, że oprogramowanie urządzenia został zaktualizowany w lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="e7089-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="e7089-157">Wersja oprogramowania wyświetlane **10.0.0.0.0.10288.0** for Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="e7089-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7089-158">Firma Microsoft raport wersji oprogramowania w sposób nieco inne w lokalnym interfejsu użytkownika sieci web i klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7089-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="e7089-159">Na przykład raporty lokalnego interfejsu użytkownika sieci web **10.0.0.0.0.10288** i Azure raporty portalu klasycznego **10.0.10288.0** dla tej samej wersji.</span><span class="sxs-lookup"><span data-stu-id="e7089-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="e7089-161">Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e7089-161">Use the Azure classic portal</span></span>
<span data-ttu-id="e7089-162">Uruchomiona Update 0.2, zaleca się zainstalowanie aktualizacji za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7089-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="e7089-163">Procedury portalu wymaga od użytkownika skanowania, Pobierz i zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="e7089-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="e7089-164">Ta procedura trwa około 7 minut do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e7089-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="e7089-165">Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.</span><span class="sxs-lookup"><span data-stu-id="e7089-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="e7089-166">Po zakończeniu instalacji (co wskazuje stan zadania w skali 100%), przejdź do **urządzenia > konserwacja > aktualizacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="e7089-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="e7089-167">Wersja oprogramowania wyświetlane powinna mieć 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="e7089-167">The displayed software version should be 10.0.10288.0.</span></span>

![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="e7089-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7089-169">Next steps</span></span>
<span data-ttu-id="e7089-170">Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="e7089-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

