---
title: "web tablicy wirtualnego aaaStorSimple interfejsu użytkownika administracji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooperform urządzenie podstawowe zadania za pomocą hello interfejsu użytkownika sieci web tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="94289-103">Użyj tooadminister interfejsu użytkownika sieci Web hello tablica wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="94289-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![przepływ procesu instalacji](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="94289-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="94289-105">Overview</span></span>
<span data-ttu-id="94289-106">Witaj w tym artykule samouczkach toohello Microsoft Azure StorSimple wirtualnego tablicy (znanej także jako hello lokalnej urządzenia wirtualnego StorSimple) uruchomionej wersji ogólnodostępnej (GA) marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="94289-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="94289-107">W tym artykule opisano niektóre hello złożonych przepływów pracy i zadania zarządzania, które mogą być wykonywane na powitania tablicy wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94289-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="94289-108">Możesz zarządzać hello tablicę wirtualnego StorSimple przy użyciu usługi Menedżer StorSimple hello interfejsu użytkownika (portal hello tooas określonego interfejsu użytkownika) i hello lokalnego interfejsu użytkownika sieci web dla hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="94289-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="94289-109">Ten artykuł skupia się na powitania zadania czy można wykonać przy użyciu interfejsu użytkownika sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="94289-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="94289-110">Ten artykuł zawiera następujące samouczki hello:</span><span class="sxs-lookup"><span data-stu-id="94289-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="94289-111">Pobierz klucz szyfrowania danych usługi hello</span><span class="sxs-lookup"><span data-stu-id="94289-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="94289-112">Rozwiąż problemy z błędami ustawień interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="94289-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="94289-113">Generowanie pakietu dziennika</span><span class="sxs-lookup"><span data-stu-id="94289-113">Generate a log package</span></span>
* <span data-ttu-id="94289-114">Zamknięcie lub ponowne uruchomienie urządzenia</span><span class="sxs-lookup"><span data-stu-id="94289-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="94289-115">Pobierz klucz szyfrowania danych usługi hello</span><span class="sxs-lookup"><span data-stu-id="94289-115">Get hello service data encryption key</span></span>
<span data-ttu-id="94289-116">Klucz szyfrowania danych usługi jest generowany podczas rejestrowania pierwszego urządzenia z hello usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94289-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="94289-117">Ten klucz jest wymagany z hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94289-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="94289-118">Jeśli użytkownik ma Zagubione klucz szyfrowania danych usługi i musi tooretrieve, wykonaj następujące hello zarejestrowane kroki lokalne powitania interfejsu użytkownika urządzenia hello sieci web przy użyciu usługi.</span><span class="sxs-lookup"><span data-stu-id="94289-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="94289-119">klucz szyfrowania danych usługi hello tooget</span><span class="sxs-lookup"><span data-stu-id="94289-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="94289-120">Połączenie lokalne toohello interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="94289-120">Connect toohello local web UI.</span></span> <span data-ttu-id="94289-121">Przejdź za**konfiguracji** > **ustawienia chmury**.</span><span class="sxs-lookup"><span data-stu-id="94289-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="94289-122">U dołu hello hello strony, kliknij przycisk **klucza szyfrowania danych usługi Get**.</span><span class="sxs-lookup"><span data-stu-id="94289-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="94289-123">Zostanie wyświetlony klucz.</span><span class="sxs-lookup"><span data-stu-id="94289-123">A key will appear.</span></span> <span data-ttu-id="94289-124">Skopiuj i Zapisz ten klucz.</span><span class="sxs-lookup"><span data-stu-id="94289-124">Copy and save this key.</span></span>
   
    ![Pobierz klucz szyfrowania danych usługi 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="94289-126">Rozwiąż problemy z błędami ustawień interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="94289-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="94289-127">W niektórych przypadkach po skonfigurowaniu urządzenia hello za pośrednictwem sieci web lokalne powitania interfejsu użytkownika, możesz napotkać błędy.</span><span class="sxs-lookup"><span data-stu-id="94289-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="94289-128">toodiagnose i rozwiązywanie tych problemów, można uruchomić testów diagnostycznych hello.</span><span class="sxs-lookup"><span data-stu-id="94289-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="94289-129">testów diagnostycznych hello toorun</span><span class="sxs-lookup"><span data-stu-id="94289-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="94289-130">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**Rozwiązywanie problemów** > **testów diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="94289-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![Uruchom funkcję diagnostyki 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="94289-132">U dołu hello hello strony, kliknij przycisk **uruchamiania testów diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="94289-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="94289-133">Spowoduje to zainicjowanie toodiagnose testy możliwe problemy z sieci, urządzenia, serwer proxy sieci web, czas lub ustawienia chmury.</span><span class="sxs-lookup"><span data-stu-id="94289-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="94289-134">Czy urządzenie hello jest uruchomione testy, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="94289-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="94289-135">Po zakończeniu testów hello, hello wyniki będą wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="94289-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="94289-136">Witaj poniższy przykład przedstawia hello wyniki testów diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="94289-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="94289-137">Należy pamiętać, że nie skonfigurowano ustawień serwera proxy sieci web hello na tym urządzeniu i w związku z tym testu serwera proxy sieci web hello nie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="94289-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="94289-138">Witaj wszystkich innych testach dla ustawień sieci, serwer DNS i ustawienia czasu zostały pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="94289-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![Uruchom funkcję diagnostyki 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="94289-140">Generowanie pakietu dziennika</span><span class="sxs-lookup"><span data-stu-id="94289-140">Generate a log package</span></span>
<span data-ttu-id="94289-141">Pakiet dziennika obejmuje wszystkie dzienniki odpowiednich hello, które mogą pomóc Support firmy Microsoft o wszelkich rozwiązywania problemów z urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="94289-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="94289-142">W tej wersji pakietu dziennika można wygenerować za pomocą lokalne powitania interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="94289-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="94289-143">toogenerate hello dziennika pakietu</span><span class="sxs-lookup"><span data-stu-id="94289-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="94289-144">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**Rozwiązywanie problemów** > **dzienniki systemu**.</span><span class="sxs-lookup"><span data-stu-id="94289-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![Generowanie pakietu dziennika 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="94289-146">U dołu hello hello strony, kliknij przycisk **Utwórz pakiet dziennika**.</span><span class="sxs-lookup"><span data-stu-id="94289-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="94289-147">Zostanie utworzony pakiet hello dzienniki systemu.</span><span class="sxs-lookup"><span data-stu-id="94289-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="94289-148">To może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="94289-148">This will take a couple of minutes.</span></span>
   
    ![Generowanie pakietu dziennika 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="94289-150">Po pomyślnym utworzeniu pakietu hello i hello strona będzie aktualizowana tooindicate hello godzina i Data utworzenia pakietu hello, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="94289-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![Generowanie pakietu dziennika 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="94289-152">Kliknij przycisk **pakiet dziennika**.</span><span class="sxs-lookup"><span data-stu-id="94289-152">Click **Download log package**.</span></span> <span data-ttu-id="94289-153">Pakiet ZIP zostanie pobrana w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="94289-153">A zipped package will be downloaded on your system.</span></span>
   
    ![Generowanie pakietu dziennika 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="94289-155">Można rozpakować hello dziennika pobranego pakietu i wyświetlać plikach dziennika systemowego hello.</span><span class="sxs-lookup"><span data-stu-id="94289-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="94289-156">Zamykanie i ponowne uruchomienie urządzenia</span><span class="sxs-lookup"><span data-stu-id="94289-156">Shut down and restart your device</span></span>
<span data-ttu-id="94289-157">Możesz zamknąć lub ponownie uruchomić urządzenie wirtualne za pomocą lokalne powitania interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="94289-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="94289-158">Zalecamy, aby przed ponownego uruchomienia, wykonać hello woluminy lub udziały w tryb offline na hoście hello i następnie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="94289-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="94289-159">Pozwoli to zminimalizować możliwości uszkodzenie danych.</span><span class="sxs-lookup"><span data-stu-id="94289-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="94289-160">tooshut wyłączenia urządzenia wirtualnego</span><span class="sxs-lookup"><span data-stu-id="94289-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="94289-161">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **ustawienia zasilania**.</span><span class="sxs-lookup"><span data-stu-id="94289-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="94289-162">U dołu hello hello strony, kliknij przycisk **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="94289-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![zamknięcie urządzenia 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="94289-164">Zostanie wyświetlone ostrzeżenie, informujący, że wyłączenie urządzenia hello przerywa żadnych we/wy, które były w toku, co spowoduje Przestój.</span><span class="sxs-lookup"><span data-stu-id="94289-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="94289-165">Kliknij ikonę znacznika wyboru hello</span><span class="sxs-lookup"><span data-stu-id="94289-165">Click hello check icon</span></span> ![ikona znacznika wyboru](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="94289-167">.</span><span class="sxs-lookup"><span data-stu-id="94289-167">.</span></span>
   
    ![Ostrzeżenie zamknięcia urządzenia](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="94289-169">Dowiesz się, że ten shutdown hello została zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="94289-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![Rozpoczęto zamknięcia urządzenia](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="94289-171">Witaj urządzenia zostanie teraz zamknięty.</span><span class="sxs-lookup"><span data-stu-id="94289-171">hello device will now shut down.</span></span> <span data-ttu-id="94289-172">Jeśli urządzenie ma toostart należy toodo, który za pomocą hello Menedżera funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="94289-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="94289-173">toorestart urządzenia wirtualnego</span><span class="sxs-lookup"><span data-stu-id="94289-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="94289-174">W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **ustawienia zasilania**.</span><span class="sxs-lookup"><span data-stu-id="94289-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="94289-175">U dołu hello hello strony, kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="94289-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![ponowne uruchomienie urządzenia](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="94289-177">Zostanie wyświetlone ostrzeżenie, informujący, że ponownie uruchomić urządzenie hello przerywa żadnych IOs, które były w toku, co spowoduje Przestój.</span><span class="sxs-lookup"><span data-stu-id="94289-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="94289-178">Kliknij ikonę znacznika wyboru hello</span><span class="sxs-lookup"><span data-stu-id="94289-178">Click hello check icon</span></span> ![ikona znacznika wyboru](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="94289-180">.</span><span class="sxs-lookup"><span data-stu-id="94289-180">.</span></span>
   
    ![Ostrzeżenie o ponownym uruchomieniu](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="94289-182">Użytkownik będzie powiadamiany, że ponowne hello została zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="94289-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![zainicjowano ponowne uruchomienie](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="94289-184">Podczas ponownego uruchomienia hello jest w toku, utracisz hello połączenia toohello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94289-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="94289-185">Ponowne uruchomienie hello można monitorować okresowo odświeżając hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94289-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="94289-186">Alternatywnie można monitorować stan ponowne uruchomienie urządzenia hello za pomocą Menedżera funkcji Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="94289-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94289-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94289-187">Next steps</span></span>
<span data-ttu-id="94289-188">Dowiedz się, jak za[Użyj hello toomanage usługi Menedżer StorSimple, urządzenie](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="94289-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

