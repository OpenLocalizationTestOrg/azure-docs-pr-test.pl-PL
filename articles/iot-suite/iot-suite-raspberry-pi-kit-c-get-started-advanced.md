---
title: "Pi malina nawiązać połączenie za pomocą C do obsługi aktualizacji oprogramowania układowego pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Microsoft Azure IoT Starter Kit malinowe pi 3 i pakiet Azure IoT. C używany do nawiązania połączenia zdalnego rozwiązanie monitorowania sieci Pi malina wysyłania danych telemetrycznych z czujników do chmury, a w przypadku aktualizowania zdalnego oprogramowania układowego."
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
ms.openlocfilehash: f36f6512bb30e4b109b1bd1c3cdab10300f4edc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="eb03e-104">Twoje malina Pi 3 nawiązać połączenie zdalne rozwiązanie monitorowania i Włącz aktualizacje oprogramowania układowego zdalnego za pomocą C</span><span class="sxs-lookup"><span data-stu-id="eb03e-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="eb03e-105">W tym samouczku przedstawiono sposób użycia programu Microsoft Azure IoT Starter Kit dla 3 Pi malina do:</span><span class="sxs-lookup"><span data-stu-id="eb03e-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="eb03e-106">Opracowywanie czytnik temperatury i wilgotności, który może komunikować się z chmurą.</span><span class="sxs-lookup"><span data-stu-id="eb03e-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="eb03e-107">Włącz i wykonywanie zdalnego oprogramowania układowego aktualizacja lub aktualizacja aplikacji klienckiej na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="eb03e-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="eb03e-108">W samouczku:</span><span class="sxs-lookup"><span data-stu-id="eb03e-108">The tutorial uses:</span></span>

* <span data-ttu-id="eb03e-109">Raspbian systemu operacyjnego, język programowania C i Microsoft Azure IoT SDK dla języka C do zaimplementowania urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="eb03e-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="eb03e-110">Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="eb03e-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="eb03e-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="eb03e-111">Overview</span></span>

<span data-ttu-id="eb03e-112">W tym samouczku zostaną wykonane następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb03e-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="eb03e-113">Wdrożenie wystąpienia programu zdalnego wstępnie skonfigurowane rozwiązanie monitorowania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb03e-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="eb03e-114">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb03e-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="eb03e-115">Konfigurowanie czujniki i urządzenia do komunikowania się z komputerem i zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="eb03e-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="eb03e-116">Zaktualizuj przykładowy kod urządzenia do nawiązania połączenia zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eb03e-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="eb03e-117">Aby zaktualizować aplikację klienta, należy użyć przykładowego kodu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="eb03e-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="eb03e-118">Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb03e-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="eb03e-119">Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eb03e-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="eb03e-120">Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="eb03e-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="eb03e-121">Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="eb03e-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="eb03e-122">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="eb03e-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="eb03e-123">Pobierz i skonfiguruj próbki</span><span class="sxs-lookup"><span data-stu-id="eb03e-123">Download and configure the sample</span></span>

<span data-ttu-id="eb03e-124">Można teraz pobrać i konfigurowania zdalnego monitorowania aplikacji klienckiej na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="eb03e-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="eb03e-125">Klonowanie repozytoria</span><span class="sxs-lookup"><span data-stu-id="eb03e-125">Clone the repositories</span></span>

<span data-ttu-id="eb03e-126">Jeśli jeszcze tego nie zrobiono tego wcześniej, klonowanie wymagane repozytoriów, uruchamiając następujące polecenia na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="eb03e-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="eb03e-127">Zaktualizuj parametry połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="eb03e-127">Update the device connection string</span></span>

<span data-ttu-id="eb03e-128">Otwórz przykładowy plik konfiguracji w **nano** edytora za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="eb03e-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="eb03e-129">Zastąp symbole zastępcze identyfikator i Centrum IoT informacji o urządzeniu utworzony i zapisany na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="eb03e-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="eb03e-130">Gdy wszystko będzie gotowe, zawartość pliku deviceinfo powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="eb03e-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="eb03e-131">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="eb03e-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="eb03e-132">Tworzyć przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="eb03e-132">Build the sample</span></span>

<span data-ttu-id="eb03e-133">Jeśli jeszcze nie, uruchamiając następujące polecenia w terminalu na Pi malina należy zainstalować wstępnie wymagane pakiety dla zestawu SDK programu Microsoft Azure IoT urządzenia dla języka C:</span><span class="sxs-lookup"><span data-stu-id="eb03e-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="eb03e-134">Przykładowe rozwiązanie można teraz tworzyć na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="eb03e-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="eb03e-135">Teraz możesz uruchomić program przykładowy na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="eb03e-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="eb03e-136">Wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="eb03e-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="eb03e-137">Następujące przykładowe dane wyjściowe jest przykład danych wyjściowych, widocznej na Pi malina w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="eb03e-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="eb03e-139">Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="eb03e-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="eb03e-140">Na pulpicie nawigacyjnym rozwiązania kliknij **urządzeń** do odwiedzenia **urządzeń** strony.</span><span class="sxs-lookup"><span data-stu-id="eb03e-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="eb03e-141">Wybierz użytkownika malinowe Pi w **listę urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="eb03e-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="eb03e-142">Następnie wybierz pozycję **metody**:</span><span class="sxs-lookup"><span data-stu-id="eb03e-142">Then choose **Methods**:</span></span>

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

1. <span data-ttu-id="eb03e-144">Na **wywołania metody** wybierz pozycję **InitiateFirmwareUpdate** w **metody** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="eb03e-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="eb03e-145">W **FWPackageURI** wprowadź **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="eb03e-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="eb03e-146">Ten plik archiwum zawiera implementacji oprogramowania układowego w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="eb03e-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="eb03e-147">Wybierz **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="eb03e-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="eb03e-148">Aplikacja na Pi malina wysyła potwierdzenie z powrotem do pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eb03e-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="eb03e-149">Następnie uruchamia proces aktualizacji oprogramowania układowego pobierając nowej wersji oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="eb03e-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Pokaż historię — metoda][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="eb03e-151">Obserwowanie procesu aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="eb03e-151">Observe the firmware update process</span></span>

<span data-ttu-id="eb03e-152">Można obserwować oprogramowanie układowe zaktualizować procesu, ponieważ była uruchamiana na urządzeniu i wyświetlając właściwości zgłoszony na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="eb03e-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="eb03e-153">Postęp w proces aktualizacji można wyświetlić na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="eb03e-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Pokaż postęp aktualizacji][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="eb03e-155">Zdalnej aplikacji monitorowania uruchamia ponownie dyskretnie po ukończeniu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="eb03e-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="eb03e-156">Użyj polecenia `ps -ef` można zweryfikować jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="eb03e-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="eb03e-157">Jeśli chcesz zakończyć ten proces, użyj `kill` polecenie z identyfikatorem procesu.</span><span class="sxs-lookup"><span data-stu-id="eb03e-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="eb03e-158">Można wyświetlić stan aktualizacji oprogramowania układowego, zgłoszonych przez urządzenia, w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eb03e-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="eb03e-159">Poniższy zrzut ekranu przedstawia stan i czas trwania każdego etapu procesu aktualizacji i nowa wersja oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="eb03e-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Pokaż stan zadania][img-job-status]

    <span data-ttu-id="eb03e-161">Jeśli przejdziesz do pulpitu nawigacyjnego, możesz sprawdzić, czy urządzenie jest nadal wysyła dane telemetryczne po aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="eb03e-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="eb03e-162">Pozostawienie zdalnego monitorowania działającej na koncie Azure są rozliczane dla przy uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="eb03e-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="eb03e-163">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="eb03e-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="eb03e-164">Usuwanie wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="eb03e-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb03e-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb03e-165">Next steps</span></span>

<span data-ttu-id="eb03e-166">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="eb03e-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md