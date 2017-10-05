---
title: "Połącz malinowe Pi (C) do platformy Azure IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Node.js Pi malina"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="9f7d2-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="9f7d2-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="9f7d2-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="9f7d2-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="9f7d2-106">Aplikacja działa prawidłowo, ale nie jest migający LED</span><span class="sxs-lookup"><span data-stu-id="9f7d2-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="9f7d2-107">Ten problem dotyczy zawsze łączności obwodu sprzętu.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="9f7d2-108">Wykonaj następujące kroki, aby zidentyfikować problemy.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="9f7d2-109">Sprawdź, czy wybrano poprawny **interfejs GPIO** na tablicy.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="9f7d2-110">Dwa porty powinna być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="9f7d2-111">Sprawdź, czy bieguna z Twojej LED jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="9f7d2-112">Etap dłużej powinny wskazywać **dodatnią**, szczytową numeru pin.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="9f7d2-113">Użyj **3, 3V przypiąć** i **GND Pin** na malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="9f7d2-114">Pi należy traktować jako potęgi kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="9f7d2-115">Sprawdź, czy LED działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-115">Check that the LED works fine.</span></span>

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="9f7d2-117">Innych problemów ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="9f7d2-117">Other hardware issues</span></span>
<span data-ttu-id="9f7d2-118">Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="9f7d2-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="9f7d2-119">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="9f7d2-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="9f7d2-120">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="9f7d2-120">No response during gulp tasks</span></span>
<span data-ttu-id="9f7d2-121">Jeśli wystąpią problemy z działaniem gulp zadań, możesz dodać `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="9f7d2-122">Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="9f7d2-123">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="9f7d2-124">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="9f7d2-124">Device discovery issues</span></span>
<span data-ttu-id="9f7d2-125">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z `devdisco` polecenia, wyboru [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="9f7d2-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="9f7d2-126">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="9f7d2-126">NPM issues</span></span>
<span data-ttu-id="9f7d2-127">Spróbuj zaktualizować pakiet NPM przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="9f7d2-128">Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="9f7d2-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="9f7d2-129">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="9f7d2-129">Remote debugging</span></span>

<span data-ttu-id="9f7d2-130">Zdalne debugowanie pomocy technicznej będzie dostępna wkrótce w Visual Studio kodu C/C++ rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="9f7d2-131">W jednocześnie można używać GDB za pośrednictwem Ulubione terminalu SSH:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="9f7d2-132">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9f7d2-132">Azure-CLI issues</span></span>
<span data-ttu-id="9f7d2-133">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="9f7d2-134">Wyszukaj rozwiązanie w [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) poszukiwanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="9f7d2-135">Spróbuj uaktualnić wiersza polecenia platformy Azure do najnowszej wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="9f7d2-136">Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="9f7d2-137">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="9f7d2-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="9f7d2-138">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania", uruchom następujące polecenie, aby uaktualnić narzędzie pip do najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="9f7d2-139">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="9f7d2-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="9f7d2-140">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="9f7d2-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="9f7d2-141">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="9f7d2-142">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="9f7d2-143">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="9f7d2-144">Rozwiązanie, to usuń te pakiety zainstalowane przez główny.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="9f7d2-145">Aby zakończyć to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="9f7d2-146">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="9f7d2-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="9f7d2-147">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="9f7d2-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="9f7d2-148">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="9f7d2-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="9f7d2-149">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="9f7d2-150">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="9f7d2-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="9f7d2-151">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają narzędzia do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="9f7d2-152">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="9f7d2-152">Device Explorer</span></span>
<span data-ttu-id="9f7d2-153">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="9f7d2-154">Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="9f7d2-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="9f7d2-155">*Zarządzanie tożsamościami urządzenia* obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="9f7d2-156">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="9f7d2-157">*Wyślij chmury do urządzenia* tak wiadomości można wysyłać do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="9f7d2-158">Konfigurowanie sieci `IoT hub connection string` w to narzędzie, aby korzystać z jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="9f7d2-159">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="9f7d2-159">IoT hub Explorer</span></span>
<span data-ttu-id="9f7d2-160">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania klientami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="9f7d2-161">Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="9f7d2-162">Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie w wierszu polecenia środowiska:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="9f7d2-163">Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametry służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9f7d2-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="9f7d2-164">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9f7d2-164">Azure portal</span></span>
<span data-ttu-id="9f7d2-165">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="9f7d2-166">Można także użyć [portalu Azure](../azure-portal-overview.md) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="9f7d2-167">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="9f7d2-167">Azure storage issues</span></span>
<span data-ttu-id="9f7d2-168">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="9f7d2-169">Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="9f7d2-170">To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9f7d2-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
