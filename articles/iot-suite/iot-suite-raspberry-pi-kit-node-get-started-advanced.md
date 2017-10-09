---
title: "Aktualizuje pakiet IoT przy użyciu oprogramowania układowego toosupport Node.js aaaConnect tooAzure Pi malina | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj Node.js tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i przeprowadzić aktualizację oprogramowania układowego zdalnego."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="88dc3-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i Włącz aktualizacje oprogramowania układowego zdalnego przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="88dc3-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="88dc3-105">Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla 3 Pi malina do:</span><span class="sxs-lookup"><span data-stu-id="88dc3-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="88dc3-106">Opracowywanie czytnik temperatury i wilgotności, który może komunikować się z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="88dc3-107">Włącz i wykonywanie aplikacji klienckiej hello tooupdate aktualizacji oprogramowania układowego zdalnego na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="88dc3-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="88dc3-108">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-108">hello tutorial uses:</span></span>

- <span data-ttu-id="88dc3-109">Raspbian OS hello Node.js język programowania i hello zestawu SDK usługi Microsoft Azure IoT dla tooimplement Node.js urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="88dc3-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="88dc3-110">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="88dc3-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="88dc3-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="88dc3-111">Overview</span></span>

<span data-ttu-id="88dc3-112">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="88dc3-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="88dc3-113">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="88dc3-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="88dc3-114">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88dc3-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="88dc3-115">Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="88dc3-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="88dc3-116">Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="88dc3-117">Używanie aplikacji klient hello tooupdate kodu hello próbki urządzenia.</span><span class="sxs-lookup"><span data-stu-id="88dc3-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="88dc3-118">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88dc3-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="88dc3-119">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="88dc3-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="88dc3-120">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="88dc3-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="88dc3-121">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="88dc3-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="88dc3-122">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="88dc3-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="88dc3-123">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="88dc3-123">Download and configure hello sample</span></span>

<span data-ttu-id="88dc3-124">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="88dc3-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="88dc3-125">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="88dc3-125">Install Node.js</span></span>

<span data-ttu-id="88dc3-126">Jeśli jeszcze tego nie zrobiono tego wcześniej, należy zainstalować Node.js na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="88dc3-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="88dc3-127">Witaj IoT SDK dla środowiska Node.js wymaga wersji 0.11.5 Node.js lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="88dc3-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="88dc3-128">Witaj poniższej procedurze pokazano, jak tooinstall v6.10.2 Node.js na Twoje Pi malina:</span><span class="sxs-lookup"><span data-stu-id="88dc3-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="88dc3-129">Użyj hello następujące polecenie tooupdate Twojego Pi malina:</span><span class="sxs-lookup"><span data-stu-id="88dc3-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="88dc3-130">Użyj następującego polecenia toodownload hello Node.js plików binarnych tooyour Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="88dc3-131">Użyj hello następujące pliki binarne hello tooinstall polecenia:</span><span class="sxs-lookup"><span data-stu-id="88dc3-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="88dc3-132">Użyj hello następujące polecenie tooverify Node.js v6.10.2 zostały zainstalowane pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="88dc3-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="88dc3-133">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="88dc3-133">Clone hello repositories</span></span>

<span data-ttu-id="88dc3-134">Jeśli jeszcze tego nie zrobiono tego wcześniej, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="88dc3-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="88dc3-135">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="88dc3-135">Update hello device connection string</span></span>

<span data-ttu-id="88dc3-136">Otwórz hello przykładowy plik konfiguracyjny w hello **nano** Edytor przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="88dc3-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="88dc3-137">Zastąp symbole zastępcze hello hello identyfikator urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="88dc3-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="88dc3-138">Gdy wszystko będzie gotowe, hello zawartość pliku deviceinfo hello powinna wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88dc3-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="88dc3-139">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="88dc3-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="88dc3-140">Uruchom hello próbki</span><span class="sxs-lookup"><span data-stu-id="88dc3-140">Run hello sample</span></span>

<span data-ttu-id="88dc3-141">Witaj uruchom następujące polecenia tooinstall hello pakietów wymagań wstępnych dla przykładu hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="88dc3-142">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="88dc3-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="88dc3-143">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="88dc3-144">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="88dc3-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="88dc3-146">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="88dc3-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="88dc3-147">Na pulpicie nawigacyjnym rozwiązania hello, kliknij przycisk **urządzeń** toovisit hello **urządzeń** strony.</span><span class="sxs-lookup"><span data-stu-id="88dc3-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="88dc3-148">Wybierz użytkownika Pi malina hello **listę urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="88dc3-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="88dc3-149">Następnie wybierz pozycję **metody**:</span><span class="sxs-lookup"><span data-stu-id="88dc3-149">Then choose **Methods**:</span></span>

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

1. <span data-ttu-id="88dc3-151">Na powitania **wywołania metody** wybierz pozycję **InitiateFirmwareUpdate** w hello **metody** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="88dc3-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="88dc3-152">W hello **FWPackageURI** wprowadź **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="88dc3-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="88dc3-153">Ten plik zawiera hello implementacji oprogramowania układowego hello w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="88dc3-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="88dc3-154">Wybierz **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="88dc3-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="88dc3-155">Aplikacja Hello na powitania Pi malina wysyła pulpit nawigacyjny potwierdzenia wstecz toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="88dc3-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="88dc3-156">Następnie uruchamia proces aktualizacji oprogramowania układowego hello pobierając hello nowej wersji oprogramowania układowego hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Pokaż historię — metoda][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="88dc3-158">Obserwowanie procesu aktualizacji oprogramowania układowego hello</span><span class="sxs-lookup"><span data-stu-id="88dc3-158">Observe hello firmware update process</span></span>

<span data-ttu-id="88dc3-159">Można obserwować procesu aktualizacji oprogramowania układowego hello podczas jego działania na urządzeniu hello i wyświetlając hello zgłosił właściwości na pulpicie nawigacyjnym rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="88dc3-160">Można wyświetlić postęp hello w proces aktualizacji hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="88dc3-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Pokaż postęp aktualizacji][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="88dc3-162">Witaj zdalnego monitorowania ponownych uruchomień aplikacji dyskretnie po zakończeniu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="88dc3-163">Użyj polecenia hello `ps -ef` tooverify jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="88dc3-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="88dc3-164">Proces hello tooterminate, należy użyć hello `kill` polecenia o identyfikatorze hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="88dc3-165">Można wyświetlić stan hello hello aktualizacji oprogramowania układowego, zgłoszonych przez urządzenia hello, w portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="88dc3-166">Witaj Poniższy zrzut ekranu przedstawia stan hello i czas trwania każdego etapu procesu aktualizacji hello i nowa wersja oprogramowania układowego hello:</span><span class="sxs-lookup"><span data-stu-id="88dc3-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Pokaż stan zadania][img-job-status]

    <span data-ttu-id="88dc3-168">Jeśli Przejdź wstecz toohello pulpitu nawigacyjnego, możesz sprawdzić, czy urządzenie hello nadal wysyła dane telemetryczne po aktualizacji oprogramowania układowego hello.</span><span class="sxs-lookup"><span data-stu-id="88dc3-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="88dc3-169">Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="88dc3-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="88dc3-170">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="88dc3-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="88dc3-171">Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="88dc3-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88dc3-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88dc3-172">Next steps</span></span>

<span data-ttu-id="88dc3-173">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="88dc3-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
