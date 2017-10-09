---
title: "TooAzure Connect Raspberry pi (C) IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Node.js Pi malina hello"
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
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="e36ca-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e36ca-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="e36ca-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="e36ca-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="e36ca-106">Aplikacja Hello działa prawidłowo, ale hello LED nie jest migający</span><span class="sxs-lookup"><span data-stu-id="e36ca-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="e36ca-107">Ten problem jest zawsze powiązane toohardware obwodu łączności.</span><span class="sxs-lookup"><span data-stu-id="e36ca-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="e36ca-108">Użyj następującego kroki problemy tooidentify hello:</span><span class="sxs-lookup"><span data-stu-id="e36ca-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="e36ca-109">Sprawdź, czy wybrano poprawną hello **interfejs GPIO** na tablicy.</span><span class="sxs-lookup"><span data-stu-id="e36ca-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="e36ca-110">Witaj dwie powinny być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.</span><span class="sxs-lookup"><span data-stu-id="e36ca-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="e36ca-111">Sprawdź, czy bieguna hello z Twojej LED jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="e36ca-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="e36ca-112">etap dłużej Hello powinny wskazywać hello **dodatnią**, szczytową numeru pin.</span><span class="sxs-lookup"><span data-stu-id="e36ca-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="e36ca-113">Użyj hello **3, 3V przypiąć** i **GND Pin** malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e36ca-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="e36ca-114">Pi należy traktować jako hello zasilania kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="e36ca-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="e36ca-115">Sprawdź, czy ten hello LED działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="e36ca-115">Check that hello LED works fine.</span></span>

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="e36ca-117">Innych problemów ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="e36ca-117">Other hardware issues</span></span>
<span data-ttu-id="e36ca-118">Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz hello [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e36ca-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="e36ca-119">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="e36ca-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="e36ca-120">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="e36ca-120">No response during gulp tasks</span></span>
<span data-ttu-id="e36ca-121">Jeśli wystąpią problemy w uruchomionych zadań gulp, możesz dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="e36ca-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="e36ca-122">Spróbuj tooterminate bieżące gulp zadania przy użyciu klawiszy Ctrl + C, a następnie uruchom następujące polecenie w konsoli okna toosee debugowania wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="e36ca-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="e36ca-123">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="e36ca-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="e36ca-124">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="e36ca-124">Device discovery issues</span></span>
<span data-ttu-id="e36ca-125">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z hello `devdisco` polecenia, sprawdź hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="e36ca-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="e36ca-126">problemy z npm</span><span class="sxs-lookup"><span data-stu-id="e36ca-126">npm issues</span></span>
<span data-ttu-id="e36ca-127">Spróbuj tooupdate pakietu npm, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e36ca-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="e36ca-128">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e36ca-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="e36ca-129">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="e36ca-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="e36ca-130">Uruchom hello przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="e36ca-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="e36ca-131">Gdy aparat debugowania hello jest gotowy, powinny pojawić się ```Debugger listening on port 5858``` w danych wyjściowych konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="e36ca-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="e36ca-132">Skonfiguruj urządzenie zdalne programu Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="e36ca-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="e36ca-133">Otwórz hello **debugowania** panelu na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="e36ca-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="e36ca-134">Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="e36ca-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="e36ca-135">Visual Studio Code otwiera plik launch.json.</span><span class="sxs-lookup"><span data-stu-id="e36ca-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="e36ca-136">Plik launch.json hello aktualizacji z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="e36ca-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="e36ca-137">Zastąp `[device hostname or IP address]` z hello rzeczywistego urządzenia IP adres lub nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="e36ca-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="e36ca-138">toolearn więcej informacji na temat hello Visual Studio debugowanie, można znaleźć zbyt[debugowania w programie Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="e36ca-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="e36ca-140">Dołącz toohello aplikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="e36ca-140">Attach toohello remote application</span></span>
<span data-ttu-id="e36ca-141">Kliknij zielony hello **Rozpocznij debugowanie** debugowania toostart przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="e36ca-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="e36ca-142">Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.</span><span class="sxs-lookup"><span data-stu-id="e36ca-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Zdalne debugowanie interakcyjne](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="e36ca-144">Problemy z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e36ca-144">Azure CLI issues</span></span>
<span data-ttu-id="e36ca-145">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="e36ca-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="e36ca-146">tooseek rozwiązania, można użyć hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="e36ca-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="e36ca-147">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="e36ca-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="e36ca-148">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="e36ca-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="e36ca-149">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="e36ca-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="e36ca-150">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="e36ca-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="e36ca-151">Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="e36ca-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="e36ca-152">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="e36ca-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="e36ca-153">Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="e36ca-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="e36ca-154">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="e36ca-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="e36ca-155">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="e36ca-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="e36ca-156">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="e36ca-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="e36ca-157">Lista pakietów utworzone przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="e36ca-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="e36ca-158">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="e36ca-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="e36ca-159">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="e36ca-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="e36ca-160">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="e36ca-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="e36ca-161">Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z wiersza polecenia platformy Azure i trzeba urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujących narzędzi.</span><span class="sxs-lookup"><span data-stu-id="e36ca-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="e36ca-162">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="e36ca-162">Device explorer</span></span>
<span data-ttu-id="e36ca-163">Witaj [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) narzędzie działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e36ca-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="e36ca-164">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="e36ca-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="e36ca-165">*Zarządzanie tożsamościami urządzenia* tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e36ca-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="e36ca-166">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e36ca-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="e36ca-167">*Wyślij chmury do urządzenia* , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e36ca-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="e36ca-168">Konfigurowanie parametrów połączenia Centrum IoT w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="e36ca-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="e36ca-169">Eksplorator Centrum iothub</span><span class="sxs-lookup"><span data-stu-id="e36ca-169">iothub-explorer</span></span>
<span data-ttu-id="e36ca-170">[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e36ca-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="e36ca-171">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłać chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e36ca-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="e36ca-172">tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="e36ca-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="e36ca-173">Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:</span><span class="sxs-lookup"><span data-stu-id="e36ca-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="e36ca-174">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e36ca-174">Azure portal</span></span>
<span data-ttu-id="e36ca-175">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e36ca-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="e36ca-176">Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e36ca-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="e36ca-177">Problemy z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e36ca-177">Azure Storage issues</span></span>
<span data-ttu-id="e36ca-178">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="e36ca-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="e36ca-179">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="e36ca-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="e36ca-180">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e36ca-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

