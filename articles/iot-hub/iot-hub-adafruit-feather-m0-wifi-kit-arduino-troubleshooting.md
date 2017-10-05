---
title: "Połącz Arduino (C) do platformy Azure IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony Adafruit piór M0 sieci Wi-Fi Arduino środowisko"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Rozwiązywanie problemów z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="045db-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="045db-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="045db-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="045db-105">Hardware issues</span></span>
<span data-ttu-id="045db-106">Aby uzyskać informacje o rozwiązywaniu typowych problemów na tablicy Adafruit piór M0 sieci Wi-Fi Arduino, zobacz [oficjalnego stronę rozwiązywania problemów](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="045db-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="045db-107">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="045db-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="045db-108">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="045db-108">No response during gulp tasks</span></span>
<span data-ttu-id="045db-109">Jeśli wystąpią problemy z działaniem gulp zadań, możesz dodać `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="045db-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="045db-110">Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania.</span><span class="sxs-lookup"><span data-stu-id="045db-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="045db-111">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="045db-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="045db-112">Lub możesz dodać `--listen` do otwarcia portu szeregowego do informacji dziennika urządzenia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="045db-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="045db-113">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="045db-113">NPM issues</span></span>
<span data-ttu-id="045db-114">Spróbuj zaktualizować pakiet NPM przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="045db-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="045db-115">Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="045db-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="045db-116">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="045db-116">Azure-CLI issues</span></span>
<span data-ttu-id="045db-117">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="045db-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="045db-118">Wyszukaj rozwiązanie w [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) poszukiwanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="045db-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="045db-119">Spróbuj uaktualnić wiersza polecenia platformy Azure do najnowszej wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="045db-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="045db-120">Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="045db-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="045db-121">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="045db-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="045db-122">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania", uruchom następujące polecenie, aby uaktualnić narzędzie pip do najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="045db-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="045db-123">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="045db-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="045db-124">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="045db-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="045db-125">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="045db-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="045db-126">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="045db-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="045db-127">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień.</span><span class="sxs-lookup"><span data-stu-id="045db-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="045db-128">Rozwiązanie, to usuń te pakiety zainstalowane przez główny.</span><span class="sxs-lookup"><span data-stu-id="045db-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="045db-129">Aby zakończyć to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="045db-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="045db-130">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="045db-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="045db-131">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="045db-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="045db-132">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="045db-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="045db-133">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="045db-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="045db-134">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="045db-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="045db-135">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają narzędzia do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi:</span><span class="sxs-lookup"><span data-stu-id="045db-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="045db-136">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="045db-136">Device Explorer</span></span>
<span data-ttu-id="045db-137">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="045db-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="045db-138">Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="045db-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="045db-139">*Zarządzanie tożsamościami urządzenia* obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="045db-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="045db-140">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="045db-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="045db-141">*Wyślij chmury do urządzenia* tak wiadomości można wysyłać do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="045db-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="045db-142">Konfigurowanie sieci `IoT hub connection string` w to narzędzie, aby korzystać z jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="045db-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="045db-143">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="045db-143">IoT hub Explorer</span></span>
<span data-ttu-id="045db-144">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania klientami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="045db-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="045db-145">Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="045db-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="045db-146">Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie w wierszu polecenia środowiska:</span><span class="sxs-lookup"><span data-stu-id="045db-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="045db-147">Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametry służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="045db-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="045db-148">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="045db-148">Azure portal</span></span>
<span data-ttu-id="045db-149">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="045db-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="045db-150">Można także użyć [portalu Azure](../azure-portal-overview.md) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="045db-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="045db-151">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="045db-151">Azure storage issues</span></span>
<span data-ttu-id="045db-152">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="045db-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="045db-153">Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim.</span><span class="sxs-lookup"><span data-stu-id="045db-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="045db-154">To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="045db-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md