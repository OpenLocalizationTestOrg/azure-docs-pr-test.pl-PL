---
title: "TooAzure Connect Raspberry pi (C) IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="a9712-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="a9712-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="a9712-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="a9712-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="a9712-106">Aplikacja Hello działa prawidłowo, ale hello LED nie jest migający</span><span class="sxs-lookup"><span data-stu-id="a9712-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="a9712-107">Ten problem jest zawsze powiązane toohello sprzętu obwodu łączności.</span><span class="sxs-lookup"><span data-stu-id="a9712-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="a9712-108">Użyj następujących hello kroki problemy tooidentify.</span><span class="sxs-lookup"><span data-stu-id="a9712-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="a9712-109">Sprawdź, czy wybrano poprawną hello **interfejs GPIO** na tablicy.</span><span class="sxs-lookup"><span data-stu-id="a9712-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="a9712-110">Witaj dwie powinny być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.</span><span class="sxs-lookup"><span data-stu-id="a9712-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="a9712-111">Sprawdź, czy bieguna hello z Twojej LED jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="a9712-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="a9712-112">etap dłużej Hello powinny wskazywać hello **dodatnią**, szczytową numeru pin.</span><span class="sxs-lookup"><span data-stu-id="a9712-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="a9712-113">Użyj hello **3, 3V przypiąć** i **GND Pin** malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a9712-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="a9712-114">Pi należy traktować jako hello zasilania kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="a9712-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="a9712-115">Sprawdź, czy ten hello LED działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="a9712-115">Check that hello LED works fine.</span></span>

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="a9712-117">Innych problemów ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="a9712-117">Other hardware issues</span></span>
<span data-ttu-id="a9712-118">Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz hello [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a9712-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="a9712-119">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="a9712-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="a9712-120">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="a9712-120">No response during gulp tasks</span></span>
<span data-ttu-id="a9712-121">Jeśli wystąpią problemy z działaniem gulp zadania, można dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="a9712-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="a9712-122">Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="a9712-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="a9712-123">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="a9712-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="a9712-124">Problemy dotyczące odnajdywania urządzenia</span><span class="sxs-lookup"><span data-stu-id="a9712-124">Device discovery issues</span></span>
<span data-ttu-id="a9712-125">Aby uzyskać pomoc w rozwiązywaniu typowych problemów z hello `devdisco` polecenia, sprawdź hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="a9712-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="a9712-126">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="a9712-126">NPM issues</span></span>
<span data-ttu-id="a9712-127">Spróbuj tooupdate pakietu NPM z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a9712-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="a9712-128">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="a9712-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="a9712-129">Debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="a9712-129">Remote debugging</span></span>

<span data-ttu-id="a9712-130">Zdalne debugowanie pomocy technicznej będzie dostępna wkrótce w Visual Studio kodu C/C++ rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a9712-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="a9712-131">W jednocześnie można używać GDB za pośrednictwem Ulubione terminalu SSH:</span><span class="sxs-lookup"><span data-stu-id="a9712-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="a9712-132">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a9712-132">Azure-CLI issues</span></span>
<span data-ttu-id="a9712-133">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a9712-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="a9712-134">Wyszukaj rozwiązanie w hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="a9712-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="a9712-135">Spróbuj tooupgrade interfejsu wiersza polecenia Azure toolatest wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="a9712-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="a9712-136">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9712-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="a9712-137">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="a9712-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="a9712-138">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.</span><span class="sxs-lookup"><span data-stu-id="a9712-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="a9712-139">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="a9712-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="a9712-140">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="a9712-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="a9712-141">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="a9712-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="a9712-142">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="a9712-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="a9712-143">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="a9712-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="a9712-144">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="a9712-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="a9712-145">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="a9712-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="a9712-146">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="a9712-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="a9712-147">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="a9712-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="a9712-148">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="a9712-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="a9712-149">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="a9712-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="a9712-150">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a9712-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="a9712-151">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="a9712-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="a9712-152">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="a9712-152">Device Explorer</span></span>
<span data-ttu-id="a9712-153">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a9712-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="a9712-154">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="a9712-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="a9712-155">*Zarządzanie tożsamościami urządzenia* tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a9712-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="a9712-156">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a9712-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="a9712-157">*Wyślij chmury do urządzenia* , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a9712-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="a9712-158">Konfigurowanie sieci `IoT hub connection string` w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="a9712-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="a9712-159">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="a9712-159">IoT hub Explorer</span></span>
<span data-ttu-id="a9712-160">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów.</span><span class="sxs-lookup"><span data-stu-id="a9712-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="a9712-161">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a9712-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="a9712-162">tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="a9712-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="a9712-163">Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:</span><span class="sxs-lookup"><span data-stu-id="a9712-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="a9712-164">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a9712-164">Azure portal</span></span>
<span data-ttu-id="a9712-165">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a9712-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="a9712-166">Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9712-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="a9712-167">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="a9712-167">Azure storage issues</span></span>
<span data-ttu-id="a9712-168">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="a9712-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a9712-169">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="a9712-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="a9712-170">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9712-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
