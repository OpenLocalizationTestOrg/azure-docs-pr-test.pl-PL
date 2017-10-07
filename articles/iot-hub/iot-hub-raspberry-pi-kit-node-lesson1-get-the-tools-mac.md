---
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na macOS hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, instalowanie python mac, zainstaluj usługę git dla komputerów mac, system gulp Uruchom i zainstalować node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="504a8-104">Pobierz narzędzia hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="504a8-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="504a8-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="504a8-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="504a8-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="504a8-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="504a8-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="504a8-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="504a8-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="504a8-108">What you will do</span></span>
<span data-ttu-id="504a8-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji sieci malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="504a8-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="504a8-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="504a8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="504a8-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="504a8-111">What you will learn</span></span>
<span data-ttu-id="504a8-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="504a8-112">In this article, you will learn:</span></span>

* <span data-ttu-id="504a8-113">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="504a8-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="504a8-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="504a8-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="504a8-115">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="504a8-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="504a8-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="504a8-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="504a8-117">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="504a8-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="504a8-118">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="504a8-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="504a8-119">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="504a8-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="504a8-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="504a8-120">What you need</span></span>
<span data-ttu-id="504a8-121">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="504a8-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="504a8-122">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="504a8-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="504a8-123">Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="504a8-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="504a8-124">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="504a8-124">Install Git and Node.js</span></span>
<span data-ttu-id="504a8-125">tooinstall Git i Node.js, użyj hello [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="504a8-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="504a8-126">Instalowanie oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="504a8-126">Install Homebrew.</span></span> <span data-ttu-id="504a8-127">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź toostep 2.</span><span class="sxs-lookup"><span data-stu-id="504a8-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="504a8-128">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` tooopen terminalu.</span><span class="sxs-lookup"><span data-stu-id="504a8-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="504a8-129">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="504a8-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="504a8-130">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="504a8-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="504a8-131">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="504a8-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="504a8-132">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="504a8-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="504a8-133">Użyj hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="504a8-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="504a8-134">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="504a8-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="504a8-135">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="504a8-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="504a8-136">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="504a8-136">Install Visual Studio Code</span></span>
<span data-ttu-id="504a8-137">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="504a8-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="504a8-138">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="504a8-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="504a8-139">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="504a8-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="504a8-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="504a8-140">Summary</span></span>
<span data-ttu-id="504a8-141">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="504a8-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="504a8-142">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="504a8-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="504a8-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="504a8-143">Next steps</span></span>
[<span data-ttu-id="504a8-144">Tworzenie i wdrażanie hello migania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="504a8-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

