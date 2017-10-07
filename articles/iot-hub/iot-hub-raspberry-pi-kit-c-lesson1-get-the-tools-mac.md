---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na macOS hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji dla komputerów mac, gulp, uruchom instalację node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="f02f9-104">Pobierz narzędzia hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="f02f9-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f02f9-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f02f9-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="f02f9-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f02f9-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f02f9-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f02f9-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f02f9-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="f02f9-108">What you will do</span></span>
<span data-ttu-id="f02f9-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji sieci malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="f02f9-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="f02f9-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f02f9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f02f9-111">Mimo że hello język logiki główny hello programowania C, narzędzia Node.js są używane w hello — lekcje toodiscover urządzeń i tworzenia i wdrażania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="f02f9-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f02f9-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="f02f9-112">What you will learn</span></span>
<span data-ttu-id="f02f9-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f02f9-113">In this article, you will learn:</span></span>

* <span data-ttu-id="f02f9-114">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="f02f9-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="f02f9-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="f02f9-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f02f9-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="f02f9-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f02f9-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="f02f9-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f02f9-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="f02f9-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="f02f9-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f02f9-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f02f9-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="f02f9-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f02f9-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="f02f9-121">What you need</span></span>
<span data-ttu-id="f02f9-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="f02f9-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="f02f9-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="f02f9-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="f02f9-124">Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="f02f9-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f02f9-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="f02f9-125">Install Git and Node.js</span></span>
<span data-ttu-id="f02f9-126">tooinstall Git i Node.js, użyj hello [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f02f9-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="f02f9-127">Instalowanie oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="f02f9-127">Install Homebrew.</span></span> <span data-ttu-id="f02f9-128">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź toostep 2.</span><span class="sxs-lookup"><span data-stu-id="f02f9-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="f02f9-129">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` tooopen terminalu.</span><span class="sxs-lookup"><span data-stu-id="f02f9-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="f02f9-130">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f02f9-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="f02f9-131">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f02f9-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f02f9-132">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="f02f9-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="f02f9-133">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="f02f9-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="f02f9-134">Użyj hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="f02f9-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="f02f9-135">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="f02f9-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="f02f9-136">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="f02f9-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f02f9-137">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f02f9-137">Install Visual Studio Code</span></span>
<span data-ttu-id="f02f9-138">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f02f9-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="f02f9-139">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="f02f9-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f02f9-140">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="f02f9-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f02f9-141">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f02f9-141">Summary</span></span>
<span data-ttu-id="f02f9-142">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="f02f9-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="f02f9-143">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="f02f9-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f02f9-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f02f9-144">Next steps</span></span>
[<span data-ttu-id="f02f9-145">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="f02f9-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

