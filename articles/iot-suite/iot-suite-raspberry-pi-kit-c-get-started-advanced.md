---
title: "Aktualizuje pakiet IoT przy użyciu oprogramowania układowego toosupport C aaaConnect tooAzure Pi malina | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i przeprowadzić aktualizację oprogramowania układowego zdalnego."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="5980d-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i Włącz aktualizacje oprogramowania układowego zdalnego za pomocą C</span><span class="sxs-lookup"><span data-stu-id="5980d-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="5980d-105">Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla 3 Pi malina do:</span><span class="sxs-lookup"><span data-stu-id="5980d-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="5980d-106">Opracowywanie czytnik temperatury i wilgotności, który może komunikować się z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="5980d-107">Włącz i wykonywanie aplikacji klienckiej hello tooupdate aktualizacji oprogramowania układowego zdalnego na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="5980d-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="5980d-108">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-108">hello tutorial uses:</span></span>

* <span data-ttu-id="5980d-109">Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="5980d-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="5980d-110">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5980d-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5980d-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5980d-111">Overview</span></span>

<span data-ttu-id="5980d-112">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5980d-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="5980d-113">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="5980d-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5980d-114">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5980d-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="5980d-115">Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5980d-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="5980d-116">Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="5980d-117">Używanie aplikacji klient hello tooupdate kodu hello próbki urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5980d-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5980d-118">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5980d-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5980d-119">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5980d-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5980d-120">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="5980d-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5980d-121">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="5980d-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5980d-122">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5980d-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="5980d-123">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="5980d-123">Download and configure hello sample</span></span>

<span data-ttu-id="5980d-124">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="5980d-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="5980d-125">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="5980d-125">Clone hello repositories</span></span>

<span data-ttu-id="5980d-126">Jeśli jeszcze tego nie zrobiono tego wcześniej, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="5980d-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="5980d-127">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="5980d-127">Update hello device connection string</span></span>

<span data-ttu-id="5980d-128">Otwórz hello przykładowy plik konfiguracyjny w hello **nano** Edytor przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5980d-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="5980d-129">Zastąp symbole zastępcze hello hello identyfikator i Centrum IoT informacji o urządzeniu utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="5980d-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="5980d-130">Gdy wszystko będzie gotowe, hello zawartość pliku deviceinfo hello powinna wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5980d-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="5980d-131">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="5980d-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="5980d-132">Przykład Witaj kompilacji</span><span class="sxs-lookup"><span data-stu-id="5980d-132">Build hello sample</span></span>

<span data-ttu-id="5980d-133">Jeśli nie zostało to jeszcze zrobione, należy zainstalować hello wymagań wstępnych pakietów hello zestawu SDK usługi Microsoft Azure IoT urządzenia dla języka C, uruchamiając następujące polecenia w terminalu na powitania Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="5980d-134">Można teraz tworzyć hello przykładowe rozwiązanie na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="5980d-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="5980d-135">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="5980d-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="5980d-136">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="5980d-137">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="5980d-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="5980d-139">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="5980d-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="5980d-140">Na pulpicie nawigacyjnym rozwiązania hello, kliknij przycisk **urządzeń** toovisit hello **urządzeń** strony.</span><span class="sxs-lookup"><span data-stu-id="5980d-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="5980d-141">Wybierz użytkownika Pi malina hello **listę urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="5980d-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="5980d-142">Następnie wybierz pozycję **metody**:</span><span class="sxs-lookup"><span data-stu-id="5980d-142">Then choose **Methods**:</span></span>

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

1. <span data-ttu-id="5980d-144">Na powitania **wywołania metody** wybierz pozycję **InitiateFirmwareUpdate** w hello **metody** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5980d-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="5980d-145">W hello **FWPackageURI** wprowadź **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="5980d-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="5980d-146">Ten plik archiwum zawiera hello implementacji oprogramowania układowego hello w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="5980d-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="5980d-147">Wybierz **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="5980d-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="5980d-148">Aplikacja Hello na powitania Pi malina wysyła pulpit nawigacyjny potwierdzenia wstecz toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5980d-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="5980d-149">Następnie uruchamia proces aktualizacji oprogramowania układowego hello pobierając hello nowej wersji oprogramowania układowego hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Pokaż historię — metoda][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="5980d-151">Obserwowanie procesu aktualizacji oprogramowania układowego hello</span><span class="sxs-lookup"><span data-stu-id="5980d-151">Observe hello firmware update process</span></span>

<span data-ttu-id="5980d-152">Można obserwować procesu aktualizacji oprogramowania układowego hello podczas jego działania na urządzeniu hello i wyświetlając hello zgłosił właściwości na pulpicie nawigacyjnym rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="5980d-153">Można wyświetlić postęp hello w proces aktualizacji hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="5980d-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Pokaż postęp aktualizacji][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="5980d-155">Witaj zdalnego monitorowania ponownych uruchomień aplikacji dyskretnie po zakończeniu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="5980d-156">Użyj polecenia hello `ps -ef` tooverify jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5980d-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="5980d-157">Proces hello tooterminate, należy użyć hello `kill` polecenia o identyfikatorze hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="5980d-158">Można wyświetlić stan hello hello aktualizacji oprogramowania układowego, zgłoszonych przez urządzenia hello, w portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="5980d-159">Witaj Poniższy zrzut ekranu przedstawia stan hello i czas trwania każdego etapu procesu aktualizacji hello i nowa wersja oprogramowania układowego hello:</span><span class="sxs-lookup"><span data-stu-id="5980d-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Pokaż stan zadania][img-job-status]

    <span data-ttu-id="5980d-161">Jeśli Przejdź wstecz toohello pulpitu nawigacyjnego, możesz sprawdzić, czy urządzenie hello nadal wysyła dane telemetryczne po aktualizacji oprogramowania układowego hello.</span><span class="sxs-lookup"><span data-stu-id="5980d-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="5980d-162">Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="5980d-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="5980d-163">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5980d-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5980d-164">Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="5980d-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5980d-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5980d-165">Next steps</span></span>

<span data-ttu-id="5980d-166">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5980d-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md