---
title: "TooAzure Connect Arduino (C) IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="44bd7-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="44bd7-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="44bd7-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="44bd7-105">Hardware issues</span></span>
<span data-ttu-id="44bd7-106">Aby uzyskać informacje o rozwiązywaniu typowych problemów na tablicy Adafruit piór M0 sieci Wi-Fi Arduino, zobacz hello [oficjalnego stronę rozwiązywania problemów](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="44bd7-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="44bd7-107">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="44bd7-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="44bd7-108">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="44bd7-108">No response during gulp tasks</span></span>
<span data-ttu-id="44bd7-109">Jeśli wystąpią problemy z działaniem gulp zadania, można dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="44bd7-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="44bd7-110">Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="44bd7-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="44bd7-111">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="44bd7-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="44bd7-112">Lub możesz dodać `--listen` informacje dziennika tooopen portu szeregowego toooutput urządzenia.</span><span class="sxs-lookup"><span data-stu-id="44bd7-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="44bd7-113">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="44bd7-113">NPM issues</span></span>
<span data-ttu-id="44bd7-114">Spróbuj tooupdate pakietu NPM z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44bd7-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="44bd7-115">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="44bd7-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="44bd7-116">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="44bd7-116">Azure-CLI issues</span></span>
<span data-ttu-id="44bd7-117">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="44bd7-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="44bd7-118">Wyszukaj rozwiązanie w hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="44bd7-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="44bd7-119">Spróbuj tooupgrade interfejsu wiersza polecenia Azure toolatest wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="44bd7-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="44bd7-120">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="44bd7-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="44bd7-121">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="44bd7-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="44bd7-122">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.</span><span class="sxs-lookup"><span data-stu-id="44bd7-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="44bd7-123">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="44bd7-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="44bd7-124">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="44bd7-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="44bd7-125">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="44bd7-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="44bd7-126">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="44bd7-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="44bd7-127">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="44bd7-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="44bd7-128">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="44bd7-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="44bd7-129">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="44bd7-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="44bd7-130">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="44bd7-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="44bd7-131">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="44bd7-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="44bd7-132">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="44bd7-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="44bd7-133">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="44bd7-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="44bd7-134">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="44bd7-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="44bd7-135">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="44bd7-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="44bd7-136">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="44bd7-136">Device Explorer</span></span>
<span data-ttu-id="44bd7-137">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="44bd7-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="44bd7-138">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="44bd7-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="44bd7-139">*Zarządzanie tożsamościami urządzenia* tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44bd7-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="44bd7-140">*Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="44bd7-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="44bd7-141">*Wyślij chmury do urządzenia* , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44bd7-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="44bd7-142">Konfigurowanie sieci `IoT hub connection string` w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="44bd7-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="44bd7-143">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="44bd7-143">IoT hub Explorer</span></span>
<span data-ttu-id="44bd7-144">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów.</span><span class="sxs-lookup"><span data-stu-id="44bd7-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="44bd7-145">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="44bd7-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="44bd7-146">tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="44bd7-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="44bd7-147">Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:</span><span class="sxs-lookup"><span data-stu-id="44bd7-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="44bd7-148">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="44bd7-148">Azure portal</span></span>
<span data-ttu-id="44bd7-149">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="44bd7-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="44bd7-150">Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="44bd7-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="44bd7-151">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="44bd7-151">Azure storage issues</span></span>
<span data-ttu-id="44bd7-152">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="44bd7-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="44bd7-153">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="44bd7-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="44bd7-154">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="44bd7-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md