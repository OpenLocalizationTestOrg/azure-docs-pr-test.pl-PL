---
title: "Symulowane urządzenie & brama IoT Azure — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony Intel NUC bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="38e00-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="38e00-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="38e00-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="38e00-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="38e00-106">Nie można połączyć analizy czasowej Sensor tag</span><span class="sxs-lookup"><span data-stu-id="38e00-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="38e00-107">Aby rozwiązać problemy z łącznością Sensor tag, użyj [aplikacji Sensor tag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="38e00-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="38e00-108">Występuje problem z Intel NUC</span><span class="sxs-lookup"><span data-stu-id="38e00-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="38e00-109">Do rozwiązywania problemów z rozruchem, zapoznaj się [problemów rozruchu nie na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="38e00-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="38e00-110">Aby rozwiązać problemy z systemem operacyjnym, zobacz [problemów systemu operacyjnego na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="38e00-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="38e00-111">Aby rozwiązać inne problemy, zapoznaj się [Blink i sygnalizuje kodów dla Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="38e00-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="38e00-112">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="38e00-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="38e00-113">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="38e00-113">No response during gulp tasks</span></span>

<span data-ttu-id="38e00-114">Jeśli wystąpią problemy z uruchomionych zadań gulp, można dodać `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="38e00-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="38e00-115">Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania.</span><span class="sxs-lookup"><span data-stu-id="38e00-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="38e00-116">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="38e00-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="38e00-117">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="38e00-117">Device discovery issues</span></span>

<span data-ttu-id="38e00-118">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z `discover-sensortag` polecenia, wyboru [strona typu wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="38e00-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="38e00-119">problemy z npm</span><span class="sxs-lookup"><span data-stu-id="38e00-119">npm issues</span></span>

<span data-ttu-id="38e00-120">Spróbuj zaktualizować pakiet npm, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="38e00-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="38e00-121">Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="38e00-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="38e00-122">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="38e00-122">Remote Debugging</span></span>
> <span data-ttu-id="38e00-123">Poniżej instrukcje są przeznaczone do debugowania skryptów node.js używanych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="38e00-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="38e00-124">Uruchom przykładową aplikację w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="38e00-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="38e00-125">Uruchom przykładową aplikację w trybie debugowania, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="38e00-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="38e00-126">Gdy aparat debugowania jest gotowy, powinny pojawić się `Debugger listening on port 5858` w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="38e00-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="38e00-127">Konfigurowanie programu Visual Studio Code do nawiązania połączenia z urządzeniem zdalnym</span><span class="sxs-lookup"><span data-stu-id="38e00-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="38e00-128">Otwórz **debugowania** panelu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="38e00-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="38e00-129">Kliknij zielony **Rozpocznij debugowanie** przycisk (F5).</span><span class="sxs-lookup"><span data-stu-id="38e00-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="38e00-130">Zostanie otwarty w programie Visual Studio Code `launch.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="38e00-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="38e00-131">Aktualizacja `launch.json` pliku o następującej zawartości.</span><span class="sxs-lookup"><span data-stu-id="38e00-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="38e00-132">Zastąp `[device hostname or IP address]` z rzeczywistego urządzenia IP adres lub nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="38e00-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="38e00-134">Dołączanie do zdalnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="38e00-134">Attach to the remote application</span></span>

<span data-ttu-id="38e00-135">Kliknij zielony **Rozpocznij debugowanie** przycisk (F5) można rozpocząć debugowania.</span><span class="sxs-lookup"><span data-stu-id="38e00-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="38e00-136">Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) Aby dowiedzieć się więcej na temat debugera.</span><span class="sxs-lookup"><span data-stu-id="38e00-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Debugowanie cz próbki](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="38e00-138">Problemy z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38e00-138">Azure CLI issues</span></span>

<span data-ttu-id="38e00-139">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="38e00-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="38e00-140">Aby wyszukiwać rozwiązania, można użyć [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="38e00-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="38e00-141">Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="38e00-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="38e00-142">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="38e00-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="38e00-143">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania", uruchom następujące polecenie, aby uaktualnić narzędzie pip do najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="38e00-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="38e00-144">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="38e00-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="38e00-145">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="38e00-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="38e00-146">Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="38e00-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="38e00-147">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="38e00-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="38e00-148">Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień.</span><span class="sxs-lookup"><span data-stu-id="38e00-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="38e00-149">Rozwiązanie, to usuń te pakiety zainstalowane przez główny.</span><span class="sxs-lookup"><span data-stu-id="38e00-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="38e00-150">Aby zakończyć to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38e00-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="38e00-151">Przejdź do strony `/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="38e00-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="38e00-152">Lista pakietów utworzone przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="38e00-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="38e00-153">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="38e00-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="38e00-154">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="38e00-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="38e00-155">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="38e00-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="38e00-156">Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z wiersza polecenia platformy Azure i należy to narzędzie do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi.</span><span class="sxs-lookup"><span data-stu-id="38e00-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="38e00-157">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="38e00-157">Device Explorer</span></span>

<span data-ttu-id="38e00-158">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="38e00-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="38e00-159">Komunikuje się z następującymi [punkty końcowe Centrum IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="38e00-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="38e00-160">Zarządzanie tożsamościami urządzenia do obsługi administracyjnej urządzeń i zarządzanie nimi jest zarejestrowany w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="38e00-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="38e00-161">Otrzymywać urządzenia do chmury, więc można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="38e00-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="38e00-162">Wyślij chmury do urządzenia, więc wiadomości można wysyłać do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="38e00-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="38e00-163">Konfigurowanie parametrów połączenia Centrum IoT w to narzędzie, aby korzystać z jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="38e00-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="38e00-164">Eksplorator Centrum iothub</span><span class="sxs-lookup"><span data-stu-id="38e00-164">iothub-explorer</span></span>

<span data-ttu-id="38e00-165">[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania klientami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="38e00-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="38e00-166">Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="38e00-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="38e00-167">Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="38e00-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="38e00-168">Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametrów, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="38e00-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="38e00-169">Portalu Azure</span><span class="sxs-lookup"><span data-stu-id="38e00-169">The Azure portal</span></span>

<span data-ttu-id="38e00-170">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="38e00-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="38e00-171">Można także użyć [portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38e00-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="38e00-172">Problemy z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38e00-172">Azure Storage issues</span></span>

<span data-ttu-id="38e00-173">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com/) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="38e00-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="38e00-174">Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim.</span><span class="sxs-lookup"><span data-stu-id="38e00-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="38e00-175">To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="38e00-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
