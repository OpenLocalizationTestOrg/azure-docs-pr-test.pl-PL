---
title: "Pi malina nawiązać połączenie przy użyciu środowiska Node.js do obsługi aktualizacji oprogramowania układowego pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Microsoft Azure IoT Starter Kit malinowe pi 3 i pakiet Azure IoT. Node.js używany do nawiązania połączenia zdalnego rozwiązanie monitorowania sieci Pi malina wysyłania danych telemetrycznych z czujników do chmury, a w przypadku aktualizowania zdalnego oprogramowania układowego."
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
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="4dadb-104">Twoje malina Pi 3 nawiązać połączenie zdalne rozwiązanie monitorowania i Włącz aktualizacje oprogramowania układowego zdalnego przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="4dadb-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="4dadb-105">W tym samouczku przedstawiono sposób użycia programu Microsoft Azure IoT Starter Kit dla 3 Pi malina do:</span><span class="sxs-lookup"><span data-stu-id="4dadb-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="4dadb-106">Opracowywanie czytnik temperatury i wilgotności, który może komunikować się z chmurą.</span><span class="sxs-lookup"><span data-stu-id="4dadb-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="4dadb-107">Włącz i wykonywanie zdalnego oprogramowania układowego aktualizacja lub aktualizacja aplikacji klienckiej na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="4dadb-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="4dadb-108">W samouczku:</span><span class="sxs-lookup"><span data-stu-id="4dadb-108">The tutorial uses:</span></span>

- <span data-ttu-id="4dadb-109">Raspbian systemu operacyjnego, język programowania Node.js i Microsoft Azure IoT SDK dla środowiska Node.js do zaimplementowania urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="4dadb-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="4dadb-110">Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="4dadb-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="4dadb-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4dadb-111">Overview</span></span>

<span data-ttu-id="4dadb-112">W tym samouczku zostaną wykonane następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4dadb-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="4dadb-113">Wdrożenie wystąpienia programu zdalnego wstępnie skonfigurowane rozwiązanie monitorowania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4dadb-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="4dadb-114">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4dadb-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="4dadb-115">Konfigurowanie czujniki i urządzenia do komunikowania się z komputerem i zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="4dadb-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="4dadb-116">Zaktualizuj przykładowy kod urządzenia do nawiązania połączenia zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4dadb-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="4dadb-117">Aby zaktualizować aplikację klienta, należy użyć przykładowego kodu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4dadb-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4dadb-118">Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4dadb-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4dadb-119">Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4dadb-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4dadb-120">Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="4dadb-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4dadb-121">Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="4dadb-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4dadb-122">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="4dadb-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="4dadb-123">Pobierz i skonfiguruj próbki</span><span class="sxs-lookup"><span data-stu-id="4dadb-123">Download and configure the sample</span></span>

<span data-ttu-id="4dadb-124">Można teraz pobrać i konfigurowania zdalnego monitorowania aplikacji klienckiej na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="4dadb-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="4dadb-125">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="4dadb-125">Install Node.js</span></span>

<span data-ttu-id="4dadb-126">Jeśli jeszcze tego nie zrobiono tego wcześniej, należy zainstalować Node.js na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="4dadb-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="4dadb-127">Zestaw SDK IoT dla środowiska Node.js wymaga wersji 0.11.5 Node.js lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4dadb-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="4dadb-128">Poniższe kroki pokazują, jak zainstalować Node.js v6.10.2 na Twoje Pi malina:</span><span class="sxs-lookup"><span data-stu-id="4dadb-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="4dadb-129">Można zaktualizować Twojego Pi malina, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dadb-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="4dadb-130">Podczas pobierania plików binarnych Node.js z Pi malina, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dadb-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="4dadb-131">Aby zainstalować pliki binarne, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dadb-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="4dadb-132">Użyj następującego polecenia, aby sprawdzić, czy pomyślnie zainstalowano Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="4dadb-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="4dadb-133">Klonowanie repozytoria</span><span class="sxs-lookup"><span data-stu-id="4dadb-133">Clone the repositories</span></span>

<span data-ttu-id="4dadb-134">Jeśli jeszcze tego nie zrobiono tego wcześniej, klonowanie wymagane repozytoriów, uruchamiając następujące polecenia na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="4dadb-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="4dadb-135">Zaktualizuj parametry połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="4dadb-135">Update the device connection string</span></span>

<span data-ttu-id="4dadb-136">Otwórz przykładowy plik konfiguracji w **nano** edytora za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dadb-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="4dadb-137">Zastąp symbole zastępcze identyfikator urządzenia i Centrum IoT informacji utworzony i zapisany na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="4dadb-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="4dadb-138">Gdy wszystko będzie gotowe, zawartość pliku deviceinfo powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4dadb-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="4dadb-139">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="4dadb-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="4dadb-140">Uruchom próbki</span><span class="sxs-lookup"><span data-stu-id="4dadb-140">Run the sample</span></span>

<span data-ttu-id="4dadb-141">Uruchom następujące polecenia, aby zainstalować wstępnie wymagane pakiety przykładowej:</span><span class="sxs-lookup"><span data-stu-id="4dadb-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="4dadb-142">Teraz możesz uruchomić program przykładowy na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="4dadb-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="4dadb-143">Wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="4dadb-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="4dadb-144">Następujące przykładowe dane wyjściowe jest przykład danych wyjściowych, widocznej na Pi malina w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dadb-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="4dadb-146">Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="4dadb-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="4dadb-147">Na pulpicie nawigacyjnym rozwiązania kliknij **urządzeń** do odwiedzenia **urządzeń** strony.</span><span class="sxs-lookup"><span data-stu-id="4dadb-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="4dadb-148">Wybierz użytkownika malinowe Pi w **listę urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="4dadb-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="4dadb-149">Następnie wybierz pozycję **metody**:</span><span class="sxs-lookup"><span data-stu-id="4dadb-149">Then choose **Methods**:</span></span>

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

1. <span data-ttu-id="4dadb-151">Na **wywołania metody** wybierz pozycję **InitiateFirmwareUpdate** w **metody** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="4dadb-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="4dadb-152">W **FWPackageURI** wprowadź **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="4dadb-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="4dadb-153">Ten plik zawiera implementacji oprogramowania układowego w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="4dadb-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="4dadb-154">Wybierz **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="4dadb-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="4dadb-155">Aplikacja na Pi malina wysyła potwierdzenie z powrotem do pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4dadb-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="4dadb-156">Następnie uruchamia proces aktualizacji oprogramowania układowego pobierając nowej wersji oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="4dadb-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Pokaż historię — metoda][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="4dadb-158">Obserwowanie procesu aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="4dadb-158">Observe the firmware update process</span></span>

<span data-ttu-id="4dadb-159">Można obserwować oprogramowanie układowe zaktualizować procesu, ponieważ była uruchamiana na urządzeniu i wyświetlając właściwości zgłoszony na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="4dadb-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="4dadb-160">Postęp w proces aktualizacji można wyświetlić na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="4dadb-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Pokaż postęp aktualizacji][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="4dadb-162">Zdalnej aplikacji monitorowania uruchamia ponownie dyskretnie po ukończeniu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="4dadb-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="4dadb-163">Użyj polecenia `ps -ef` można zweryfikować jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4dadb-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="4dadb-164">Jeśli chcesz zakończyć ten proces, użyj `kill` polecenie z identyfikatorem procesu.</span><span class="sxs-lookup"><span data-stu-id="4dadb-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="4dadb-165">Można wyświetlić stan aktualizacji oprogramowania układowego, zgłoszonych przez urządzenia, w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4dadb-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="4dadb-166">Poniższy zrzut ekranu przedstawia stan i czas trwania każdego etapu procesu aktualizacji i nowa wersja oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="4dadb-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Pokaż stan zadania][img-job-status]

    <span data-ttu-id="4dadb-168">Jeśli przejdziesz do pulpitu nawigacyjnego, możesz sprawdzić, czy urządzenie jest nadal wysyła dane telemetryczne po aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="4dadb-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="4dadb-169">Pozostawienie zdalnego monitorowania działającej na koncie Azure są rozliczane dla przy uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="4dadb-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="4dadb-170">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="4dadb-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4dadb-171">Usuwanie wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="4dadb-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dadb-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dadb-172">Next steps</span></span>

<span data-ttu-id="4dadb-173">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="4dadb-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
