---
title: "Połącz malinowe Pi (C) do platformy Azure IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Node.js Pi malina"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="67a88-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="67a88-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="67a88-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="67a88-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="67a88-106">Aplikacja działa prawidłowo, ale nie jest migający LED</span><span class="sxs-lookup"><span data-stu-id="67a88-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="67a88-107">Ten problem dotyczy zawsze łączności obwodu sprzętu.</span><span class="sxs-lookup"><span data-stu-id="67a88-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="67a88-108">Wykonaj następujące kroki, aby zidentyfikować problemy:</span><span class="sxs-lookup"><span data-stu-id="67a88-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="67a88-109">Sprawdź, czy wybrano poprawny **interfejs GPIO** na tablicy.</span><span class="sxs-lookup"><span data-stu-id="67a88-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="67a88-110">Dwa porty powinna być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.</span><span class="sxs-lookup"><span data-stu-id="67a88-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="67a88-111">Sprawdź, czy bieguna z Twojej LED jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="67a88-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="67a88-112">Etap dłużej powinny wskazywać **dodatnią**, szczytową numeru pin.</span><span class="sxs-lookup"><span data-stu-id="67a88-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="67a88-113">Użyj **3, 3V przypiąć** i **GND Pin** na malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="67a88-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="67a88-114">Pi należy traktować jako potęgi kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="67a88-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="67a88-115">Sprawdź, czy LED działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="67a88-115">Check that the LED works fine.</span></span>

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="67a88-117">Innych problemów ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="67a88-117">Other hardware issues</span></span>
<span data-ttu-id="67a88-118">Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="67a88-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="67a88-119">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="67a88-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="67a88-120">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="67a88-120">No response during gulp tasks</span></span>
<span data-ttu-id="67a88-121">Jeśli wystąpią problemy z uruchomionych zadań gulp, można dodać `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="67a88-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="67a88-122">Spróbuj zakończenie bieżącego zadania gulp przy użyciu klawiszy Ctrl + C, a następnie uruchom następujące polecenie w oknie konsoli wyświetlić komunikaty debugowania.</span><span class="sxs-lookup"><span data-stu-id="67a88-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="67a88-123">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="67a88-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="67a88-124">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="67a88-124">Device discovery issues</span></span>
<span data-ttu-id="67a88-125">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z `devdisco` polecenia, wyboru [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="67a88-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="67a88-126">problemy z npm</span><span class="sxs-lookup"><span data-stu-id="67a88-126">npm issues</span></span>
<span data-ttu-id="67a88-127">Spróbuj zaktualizować pakiet npm za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="67a88-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="67a88-128">Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="67a88-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="67a88-129">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="67a88-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="67a88-130">Uruchom przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="67a88-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="67a88-131">Gdy aparat debugowania jest gotowy, powinny pojawić się ```Debugger listening on port 5858``` w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="67a88-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="67a88-132">Konfigurowanie programu Visual Studio Code do nawiązania połączenia z urządzeniem zdalnym</span><span class="sxs-lookup"><span data-stu-id="67a88-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="67a88-133">Otwórz **debugowania** panelu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="67a88-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="67a88-134">Kliknij zielony **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="67a88-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="67a88-135">Visual Studio Code otwiera plik launch.json.</span><span class="sxs-lookup"><span data-stu-id="67a88-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="67a88-136">Zaktualizuj plik launch.json o następującej zawartości.</span><span class="sxs-lookup"><span data-stu-id="67a88-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="67a88-137">Zastąp `[device hostname or IP address]` z rzeczywistego urządzenia IP adres lub nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="67a88-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="67a88-138">Aby dowiedzieć się więcej na temat debugowania programu Visual Studio, zapoznaj się [debugowania w programie Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="67a88-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Konfiguracja zdalnego debugowania](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="67a88-140">Dołączanie do zdalnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="67a88-140">Attach to the remote application</span></span>
<span data-ttu-id="67a88-141">Kliknij zielony **Rozpocznij debugowanie** przycisk (F5) można rozpocząć debugowania.</span><span class="sxs-lookup"><span data-stu-id="67a88-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="67a88-142">Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) Aby dowiedzieć się więcej na temat debugera.</span><span class="sxs-lookup"><span data-stu-id="67a88-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Zdalne debugowanie interakcyjne](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="67a88-144">Problemy z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67a88-144">Azure CLI issues</span></span>
<span data-ttu-id="67a88-145">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="67a88-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="67a88-146">Aby wyszukiwać rozwiązania, można użyć [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="67a88-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="67a88-147">Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="67a88-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="67a88-148">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="67a88-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="67a88-149">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="67a88-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="67a88-150">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="67a88-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="67a88-151">Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="67a88-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="67a88-152">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="67a88-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="67a88-153">Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień.</span><span class="sxs-lookup"><span data-stu-id="67a88-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="67a88-154">Rozwiązanie, to usuń te pakiety zainstalowane przez główny.</span><span class="sxs-lookup"><span data-stu-id="67a88-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="67a88-155">Aby zakończyć to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="67a88-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="67a88-156">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="67a88-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="67a88-157">Lista pakietów utworzone przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="67a88-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="67a88-158">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="67a88-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="67a88-159">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="67a88-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="67a88-160">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="67a88-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="67a88-161">Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z wiersza polecenia platformy Azure i należy to narzędzie do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi.</span><span class="sxs-lookup"><span data-stu-id="67a88-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="67a88-162">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="67a88-162">Device explorer</span></span>
<span data-ttu-id="67a88-163">[Explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) narzędzie działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="67a88-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="67a88-164">Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="67a88-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="67a88-165">*Zarządzanie tożsamościami urządzenia* obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="67a88-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="67a88-166">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="67a88-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="67a88-167">*Wyślij chmury do urządzenia* tak wiadomości można wysyłać do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="67a88-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="67a88-168">Konfigurowanie parametrów połączenia Centrum IoT w to narzędzie, aby korzystać z jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="67a88-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="67a88-169">Eksplorator Centrum iothub</span><span class="sxs-lookup"><span data-stu-id="67a88-169">iothub-explorer</span></span>
<span data-ttu-id="67a88-170">[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="67a88-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="67a88-171">Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie komunikatów chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="67a88-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="67a88-172">Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie w wierszu polecenia środowiska:</span><span class="sxs-lookup"><span data-stu-id="67a88-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="67a88-173">Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametry służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="67a88-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="67a88-174">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="67a88-174">Azure portal</span></span>
<span data-ttu-id="67a88-175">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="67a88-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="67a88-176">Można także użyć [portalu Azure](../azure-portal-overview.md) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67a88-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="67a88-177">Problemy z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="67a88-177">Azure Storage issues</span></span>
<span data-ttu-id="67a88-178">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="67a88-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="67a88-179">Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim.</span><span class="sxs-lookup"><span data-stu-id="67a88-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="67a88-180">To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="67a88-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

