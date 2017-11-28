---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT - 4 lekcji: Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Intel Edison Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Rozwiązywanie problemów z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="a5323-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="a5323-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="a5323-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="a5323-105">Hardware issues</span></span>
<span data-ttu-id="a5323-106">Aby uzyskać informacje o rozwiązywaniu typowych problemów na Intel Edison, zobacz hello [oficjalnego stronę rozwiązywania problemów](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="a5323-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="a5323-107">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="a5323-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="a5323-108">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="a5323-108">No response during gulp tasks</span></span>
<span data-ttu-id="a5323-109">Jeśli wystąpią problemy z działaniem gulp zadania, można dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="a5323-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="a5323-110">Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="a5323-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="a5323-111">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="a5323-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="a5323-112">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="a5323-112">NPM issues</span></span>
<span data-ttu-id="a5323-113">Spróbuj tooupdate pakietu NPM z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a5323-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="a5323-114">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="a5323-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="a5323-115">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="a5323-115">Remote debugging</span></span>

### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="a5323-116">Uruchom hello przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="a5323-116">Run hello sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="a5323-117">Gdy aparat debugowania hello jest gotowy, powinno być możliwe toosee ```Debugger listening on port 5858``` z hello dane wyjściowe z konsoli.</span><span class="sxs-lookup"><span data-stu-id="a5323-117">Once hello debug engine is ready, you should be able toosee ```Debugger listening on port 5858``` from hello console output.</span></span>

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="a5323-118">Skonfiguruj urządzenie zdalne toohello tooconnect kodzie VS</span><span class="sxs-lookup"><span data-stu-id="a5323-118">Configure VS Code tooconnect toohello remote device</span></span>

<span data-ttu-id="a5323-119">Otwórz hello **debugowania** panelu powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a5323-119">Open hello **Debug** panel from hello left side.</span></span>

<span data-ttu-id="a5323-120">Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="a5323-120">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="a5323-121">Zostaną otwarte w kodzie VS **launch.json** pliku, który należy tooupdate.</span><span class="sxs-lookup"><span data-stu-id="a5323-121">VS Code would open a **launch.json** file, which you need tooupdate.</span></span>

<span data-ttu-id="a5323-122">Aktualizacja hello **launch.json** zawartość pliku z następującego hello, Zastąp `[device hostname or IP address]` z adresu IP rzeczywistego urządzenia hello lub nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="a5323-122">Update hello **launch.json** file with hello following content, replace `[device hostname or IP address]` with hello actual device IP address or hostname.</span></span>  

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

![Konfiguracja zdalnego debugowania](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="a5323-124">Dołącz toohello aplikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="a5323-124">Attach toohello remote application</span></span>

<span data-ttu-id="a5323-125">Kliknij zielony hello **Rozpocznij debugowanie** (F5) znajdujący się i korzystać z debugowania.</span><span class="sxs-lookup"><span data-stu-id="a5323-125">Click hello green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="a5323-126">Możesz przeczytać [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.</span><span class="sxs-lookup"><span data-stu-id="a5323-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Zdalne debugowanie interakcyjne](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="a5323-128">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a5323-128">Azure-CLI issues</span></span>
<span data-ttu-id="a5323-129">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a5323-129">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="a5323-130">Wyszukaj rozwiązanie w hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="a5323-130">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="a5323-131">Spróbuj tooupgrade interfejsu wiersza polecenia Azure toolatest wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="a5323-131">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="a5323-132">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5323-132">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="a5323-133">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="a5323-133">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="a5323-134">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.</span><span class="sxs-lookup"><span data-stu-id="a5323-134">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="a5323-135">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="a5323-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="a5323-136">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="a5323-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="a5323-137">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="a5323-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="a5323-138">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="a5323-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="a5323-139">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="a5323-139">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="a5323-140">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="a5323-140">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="a5323-141">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="a5323-141">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="a5323-142">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="a5323-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="a5323-143">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="a5323-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="a5323-144">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="a5323-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="a5323-145">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="a5323-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="a5323-146">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a5323-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="a5323-147">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="a5323-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="a5323-148">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="a5323-148">Device Explorer</span></span>
<span data-ttu-id="a5323-149">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5323-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="a5323-150">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="a5323-150">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="a5323-151">_Zarządzanie tożsamościami urządzenia_ tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5323-151">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="a5323-152">_Odbieranie urządzenia do chmury_ , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5323-152">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="a5323-153">_Wyślij chmury do urządzenia_ , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5323-153">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="a5323-154">Konfigurowanie sieci `IoT hub connection string` w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="a5323-154">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="a5323-155">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="a5323-155">IoT hub Explorer</span></span>
<span data-ttu-id="a5323-156">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów.</span><span class="sxs-lookup"><span data-stu-id="a5323-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="a5323-157">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5323-157">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="a5323-158">tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="a5323-158">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="a5323-159">Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:</span><span class="sxs-lookup"><span data-stu-id="a5323-159">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="a5323-160">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a5323-160">Azure portal</span></span>
<span data-ttu-id="a5323-161">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5323-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="a5323-162">Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5323-162">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="a5323-163">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="a5323-163">Azure storage issues</span></span>
<span data-ttu-id="a5323-164">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, które umożliwiają toowork z [usługi Azure Storage](https://azure.microsoft.com/en-us/services/storage/) dane dotyczące systemu Windows, system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="a5323-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a5323-165">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="a5323-165">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="a5323-166">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="a5323-166">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5323-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5323-167">Next steps</span></span>
<span data-ttu-id="a5323-168">Ta strona zawiera tylko hello najbardziej typowe problemy z zestawu Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a5323-168">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="a5323-169">Można także pozostawić komentarze dolnej tooreport problemów dotyczących rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="a5323-169">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="a5323-170">Wróć za[wprowadzenie Edison firmy Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a5323-170">Go back too[Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started