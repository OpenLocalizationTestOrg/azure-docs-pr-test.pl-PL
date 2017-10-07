---
title: "TooAzure Connect Intel Edison (C) IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony środowisko Intel Edison C"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Rozwiązywanie problemów z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="89767-104">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="89767-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="89767-105">Problemy ze sprzętem</span><span class="sxs-lookup"><span data-stu-id="89767-105">Hardware issues</span></span>
<span data-ttu-id="89767-106">Aby uzyskać informacje o rozwiązywaniu typowych problemów na Intel Edison, zobacz hello [oficjalnego stronę rozwiązywania problemów](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="89767-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="89767-107">Problemy z pakietu node.js</span><span class="sxs-lookup"><span data-stu-id="89767-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="89767-108">Brak odpowiedzi podczas gulp zadań</span><span class="sxs-lookup"><span data-stu-id="89767-108">No response during gulp tasks</span></span>
<span data-ttu-id="89767-109">Jeśli wystąpią problemy z działaniem gulp zadania, można dodać hello `--verbose` opcji do debugowania.</span><span class="sxs-lookup"><span data-stu-id="89767-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="89767-110">Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="89767-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="89767-111">Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="89767-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="89767-112">Problemy z NPM</span><span class="sxs-lookup"><span data-stu-id="89767-112">NPM issues</span></span>
<span data-ttu-id="89767-113">Spróbuj tooupdate pakietu NPM z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="89767-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="89767-114">Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="89767-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="89767-115">Problemy z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89767-115">Azure-CLI issues</span></span>
<span data-ttu-id="89767-116">Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="89767-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="89767-117">Wyszukaj rozwiązanie w hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="89767-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="89767-118">Spróbuj tooupgrade interfejsu wiersza polecenia Azure toolatest wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="89767-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="89767-119">Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="89767-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="89767-120">Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="89767-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="89767-121">Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.</span><span class="sxs-lookup"><span data-stu-id="89767-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="89767-122">Problemy z instalacją Python</span><span class="sxs-lookup"><span data-stu-id="89767-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="89767-123">Problemy z instalacją starszej wersji (system macOS)</span><span class="sxs-lookup"><span data-stu-id="89767-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="89767-124">Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="89767-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="89767-125">Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="89767-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="89767-126">Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="89767-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="89767-127">Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="89767-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="89767-128">To zadanie służy powitania po toocomplete kroki:</span><span class="sxs-lookup"><span data-stu-id="89767-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="89767-129">Przejdź do: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="89767-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="89767-130">Utwórz listę pakietów przez główny:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="89767-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="89767-131">Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="89767-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="89767-132">Zainstaluj ponownie Python.</span><span class="sxs-lookup"><span data-stu-id="89767-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="89767-133">Problemy z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="89767-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="89767-134">Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="89767-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="89767-135">Eksplorator urządzenia</span><span class="sxs-lookup"><span data-stu-id="89767-135">Device Explorer</span></span>
<span data-ttu-id="89767-136">[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89767-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="89767-137">Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="89767-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="89767-138">_Zarządzanie tożsamościami urządzenia_ tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="89767-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="89767-139">_Odbieranie urządzenia do chmury_ , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="89767-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="89767-140">_Wyślij chmury do urządzenia_ , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="89767-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="89767-141">Konfigurowanie sieci `IoT hub connection string` w ramach tego narzędzia toouse jego możliwości.</span><span class="sxs-lookup"><span data-stu-id="89767-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="89767-142">Centrum IoT Explorer</span><span class="sxs-lookup"><span data-stu-id="89767-142">IoT hub Explorer</span></span>
<span data-ttu-id="89767-143">[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów.</span><span class="sxs-lookup"><span data-stu-id="89767-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="89767-144">Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="89767-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="89767-145">tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="89767-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="89767-146">Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:</span><span class="sxs-lookup"><span data-stu-id="89767-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="89767-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="89767-147">Azure portal</span></span>
<span data-ttu-id="89767-148">Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89767-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="89767-149">Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89767-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="89767-150">Problemy z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="89767-150">Azure storage issues</span></span>
<span data-ttu-id="89767-151">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, które umożliwiają toowork z [usługi Azure Storage](https://azure.microsoft.com/en-us/services/storage/) dane dotyczące systemu Windows, system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="89767-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="89767-152">Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim.</span><span class="sxs-lookup"><span data-stu-id="89767-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="89767-153">Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="89767-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89767-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89767-154">Next steps</span></span>
<span data-ttu-id="89767-155">Ta strona zawiera tylko hello najbardziej typowe problemy z zestawu Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="89767-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="89767-156">Można także pozostawić komentarze dolnej tooreport problemów dotyczących rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="89767-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="89767-157">Wróć za[wprowadzenie Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="89767-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started