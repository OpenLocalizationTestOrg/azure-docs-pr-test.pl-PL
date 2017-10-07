---
title: "Sensor tag urządzenia & brama IoT Azure — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony Intel NUC bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="471c8-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="471c8-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="471c8-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="471c8-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="471c8-106">Nie można połączyć analizy czasowej Sensor tag</span><span class="sxs-lookup"><span data-stu-id="471c8-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="471c8-107">problemy z łącznością Sensor tag tootroubleshoot, użyj hello [aplikacji Sensor tag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="471c8-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="471c8-108">Występuje problem z Intel NUC</span><span class="sxs-lookup"><span data-stu-id="471c8-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="471c8-109">tootroubleshoot rozruchu problemów, zapoznaj się zbyt[problemów rozruchu nie na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="471c8-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="471c8-110">problemy z systemem operacyjnym tootroubleshoot, można znaleźć zbyt[problemów systemu operacyjnego na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="471c8-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="471c8-111">tootroubleshoot inne problemy, zapoznaj się zbyt[Blink i sygnalizuje kodów dla Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="471c8-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="471c8-112">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="471c8-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="471c8-113">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="471c8-113">No response during gulp tasks</span></span>

<span data-ttu-id="471c8-114">Jeśli wystąpią problemy w uruchomionych zadań gulp, możesz dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="471c8-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="471c8-115">Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="471c8-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="471c8-116">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="471c8-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="471c8-117">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="471c8-117">Device discovery issues</span></span>

<span data-ttu-id="471c8-118">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z hello `discover-sensortag` polecenia, sprawdź hello [strona typu wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="471c8-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="471c8-119">problemy z npm</span><span class="sxs-lookup"><span data-stu-id="471c8-119">npm issues</span></span>

<span data-ttu-id="471c8-120">Spróbuj tooupdate pakietu npm, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="471c8-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="471c8-121">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="471c8-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="471c8-122">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="471c8-122">Remote Debugging</span></span>
> <span data-ttu-id="471c8-123">Poniżej instrukcje są przeznaczone do debugowania skryptów node.js używanych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="471c8-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="471c8-124">Uruchom hello przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="471c8-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="471c8-125">Uruchom hello przykładową aplikację w trybie debugowania, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="471c8-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="471c8-126">Gdy aparat debugowania hello jest gotowy, powinny pojawić się `Debugger listening on port 5858` w danych wyjściowych konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="471c8-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="471c8-127">Skonfiguruj urządzenie zdalne programu Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="471c8-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="471c8-128">Otwórz hello **debugowania** panelu na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="471c8-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="471c8-129">Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="471c8-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="471c8-130">Zostanie otwarty w programie Visual Studio Code `launch.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="471c8-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="471c8-131">Aktualizacja hello `launch.json` pliku z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="471c8-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="471c8-132">Zastąp `[device hostname or IP address]` z hello rzeczywistego urządzenia IP adres lub nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="471c8-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Konfiguracja zdalnego debugowania](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="471c8-134">Dołącz toohello aplikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="471c8-134">Attach toohello remote application</span></span>

<span data-ttu-id="471c8-135">Kliknij zielony hello **Rozpocznij debugowanie** debugowania toostart przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="471c8-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="471c8-136">Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.</span><span class="sxs-lookup"><span data-stu-id="471c8-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Debugowanie cz próbki](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="471c8-138">Problemy z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="471c8-138">Azure CLI issues</span></span>

<span data-ttu-id="471c8-139">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="471c8-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="471c8-140">tooseek rozwiązania, można użyć hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="471c8-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="471c8-141">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="471c8-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="471c8-142">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="471c8-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="471c8-143">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.</span><span class="sxs-lookup"><span data-stu-id="471c8-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="471c8-144">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="471c8-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="471c8-145">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="471c8-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="471c8-146">Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="471c8-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="471c8-147">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="471c8-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="471c8-148">Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="471c8-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="471c8-149">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="471c8-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="471c8-150">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="471c8-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="471c8-151">Przejdź za`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="471c8-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="471c8-152">Lista pakietów utworzone przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="471c8-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="471c8-153">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="471c8-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="471c8-154">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="471c8-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="471c8-155">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="471c8-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="471c8-156">Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z hello wiersza polecenia platformy Azure i trzeba urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujących narzędzi.</span><span class="sxs-lookup"><span data-stu-id="471c8-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="471c8-157">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="471c8-157">Device Explorer</span></span>

<span data-ttu-id="471c8-158">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="471c8-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="471c8-159">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="471c8-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="471c8-160">Tooprovision zarządzania tożsamości urządzenia i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="471c8-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="471c8-161">Otrzymywać urządzenia do chmury, więc można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="471c8-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="471c8-162">Wyślij chmury do urządzenia, więc można wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="471c8-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="471c8-163">Konfigurowanie parametrów połączenia Centrum IoT w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="471c8-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="471c8-164">Eksplorator Centrum iothub</span><span class="sxs-lookup"><span data-stu-id="471c8-164">iothub-explorer</span></span>

<span data-ttu-id="471c8-165">[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów.</span><span class="sxs-lookup"><span data-stu-id="471c8-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="471c8-166">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="471c8-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="471c8-167">tooinstall hello najnowszej () wersji wstępnej narzędzia Centrum iothub explorer hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="471c8-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="471c8-168">tooget dodatkową pomoc na temat wszystkich hello Centrum iothub explorer poleceń i ich parametrów, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="471c8-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="471c8-169">Witaj portalu Azure</span><span class="sxs-lookup"><span data-stu-id="471c8-169">hello Azure portal</span></span>

<span data-ttu-id="471c8-170">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="471c8-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="471c8-171">Można także toouse hello [portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="471c8-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="471c8-172">Problemy z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="471c8-172">Azure Storage issues</span></span>

<span data-ttu-id="471c8-173">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com/) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="471c8-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="471c8-174">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="471c8-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="471c8-175">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="471c8-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
