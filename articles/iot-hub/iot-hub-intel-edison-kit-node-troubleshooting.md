---
title: "Edison firmy Intel (węzeł) nawiązania połączenia platformy Azure IoT — lekcji 4: Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ddc60-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ddc60-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ddc60-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="ddc60-105">Hardware issues</span></span>
<span data-ttu-id="ddc60-106">Aby uzyskać informacje o rozwiązywaniu typowych problemów na Intel Edison, zobacz [oficjalnego stronę rozwiązywania problemów](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="ddc60-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ddc60-107">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="ddc60-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ddc60-108">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="ddc60-108">No response during gulp tasks</span></span>
<span data-ttu-id="ddc60-109">Jeśli wystąpią problemy z działaniem gulp zadań, możesz dodać `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="ddc60-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="ddc60-110">Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania.</span><span class="sxs-lookup"><span data-stu-id="ddc60-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="ddc60-111">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="ddc60-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="ddc60-112">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="ddc60-112">NPM issues</span></span>
<span data-ttu-id="ddc60-113">Spróbuj zaktualizować pakiet NPM przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ddc60-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ddc60-114">Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="ddc60-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ddc60-115">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="ddc60-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="ddc60-116">Uruchom przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="ddc60-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="ddc60-117">Gdy aparat debugowania jest gotowy, powinno być możliwe wyświetlić ```Debugger listening on port 5858``` z danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="ddc60-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="ddc60-118">Skonfiguruj kodzie VS do nawiązania połączenia z urządzeniem zdalnym</span><span class="sxs-lookup"><span data-stu-id="ddc60-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="ddc60-119">Otwórz **debugowania** panelu z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="ddc60-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="ddc60-120">Kliknij zielony **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="ddc60-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="ddc60-121">Zostaną otwarte w kodzie VS **launch.json** pliku, który należy zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="ddc60-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="ddc60-122">Aktualizacja **launch.json** pliku o następującej zawartości, Zastąp `[device hostname or IP address]` z nazwą hosta lub adres IP rzeczywistego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ddc60-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="ddc60-124">Dołączanie do zdalnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ddc60-124">Attach to the remote application</span></span>

<span data-ttu-id="ddc60-125">Kliknij zielony **Rozpocznij debugowanie** (F5) znajdujący się i korzystać z debugowania.</span><span class="sxs-lookup"><span data-stu-id="ddc60-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="ddc60-126">Możesz przeczytać [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) Aby dowiedzieć się więcej na temat debugera.</span><span class="sxs-lookup"><span data-stu-id="ddc60-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Zdalne debugowanie interakcyjne](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="ddc60-128">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ddc60-128">Azure-CLI issues</span></span>
<span data-ttu-id="ddc60-129">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="ddc60-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ddc60-130">Wyszukaj rozwiązanie w [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) poszukiwanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ddc60-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="ddc60-131">Spróbuj uaktualnić wiersza polecenia platformy Azure do najnowszej wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="ddc60-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="ddc60-132">Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="ddc60-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="ddc60-133">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="ddc60-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="ddc60-134">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania", uruchom następujące polecenie, aby uaktualnić narzędzie pip do najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="ddc60-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="ddc60-135">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="ddc60-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ddc60-136">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="ddc60-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ddc60-137">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="ddc60-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="ddc60-138">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="ddc60-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ddc60-139">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień.</span><span class="sxs-lookup"><span data-stu-id="ddc60-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="ddc60-140">Rozwiązanie, to usuń te pakiety zainstalowane przez główny.</span><span class="sxs-lookup"><span data-stu-id="ddc60-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="ddc60-141">Aby zakończyć to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ddc60-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="ddc60-142">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="ddc60-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ddc60-143">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="ddc60-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ddc60-144">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="ddc60-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ddc60-145">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="ddc60-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ddc60-146">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="ddc60-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="ddc60-147">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają narzędzia do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi:</span><span class="sxs-lookup"><span data-stu-id="ddc60-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ddc60-148">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="ddc60-148">Device Explorer</span></span>
<span data-ttu-id="ddc60-149">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc60-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="ddc60-150">Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="ddc60-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="ddc60-151">_Zarządzanie tożsamościami urządzenia_ obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ddc60-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="ddc60-152">_Odbieranie urządzenia do chmury_ , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ddc60-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="ddc60-153">_Wyślij chmury do urządzenia_ tak wiadomości można wysyłać do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ddc60-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="ddc60-154">Konfigurowanie sieci `IoT hub connection string` w to narzędzie, aby korzystać z jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="ddc60-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="ddc60-155">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="ddc60-155">IoT hub Explorer</span></span>
<span data-ttu-id="ddc60-156">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania klientami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ddc60-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="ddc60-157">Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ddc60-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="ddc60-158">Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie w wierszu polecenia środowiska:</span><span class="sxs-lookup"><span data-stu-id="ddc60-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ddc60-159">Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametry służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ddc60-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ddc60-160">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ddc60-160">Azure portal</span></span>
<span data-ttu-id="ddc60-161">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc60-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ddc60-162">Można także użyć [portalu Azure](../azure-portal-overview.md) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc60-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ddc60-163">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="ddc60-163">Azure storage issues</span></span>
<span data-ttu-id="ddc60-164">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z [usługi Azure Storage](https://azure.microsoft.com/en-us/services/storage/) dane dotyczące systemu Windows, system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="ddc60-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ddc60-165">Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim.</span><span class="sxs-lookup"><span data-stu-id="ddc60-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="ddc60-166">To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ddc60-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddc60-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ddc60-167">Next steps</span></span>
<span data-ttu-id="ddc60-168">Ta strona zawiera tylko najczęściej występujących problemów Intel Edison zestawu.</span><span class="sxs-lookup"><span data-stu-id="ddc60-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="ddc60-169">Aby zgłosić problemy dotyczące rozwiązywania problemów można także pozostawić dolnej komentarze.</span><span class="sxs-lookup"><span data-stu-id="ddc60-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="ddc60-170">Wróć do [wprowadzenie Edison firmy Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ddc60-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started