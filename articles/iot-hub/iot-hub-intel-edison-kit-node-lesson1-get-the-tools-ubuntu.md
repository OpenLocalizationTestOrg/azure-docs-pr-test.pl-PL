---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Edison na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowania, git instalacji na ubuntu, ubuntu js węzła instalacji"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="34b85-104">Pobierz narzędzia hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="34b85-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="34b85-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="34b85-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="34b85-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="34b85-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="34b85-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="34b85-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="34b85-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="34b85-108">What you will do</span></span>
<span data-ttu-id="34b85-109">Pobierz narzędzia deweloperskie hello i oprogramowania hello hello pierwszy przykładowej aplikacji Edison Twojego Intel.</span><span class="sxs-lookup"><span data-stu-id="34b85-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="34b85-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="34b85-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="34b85-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="34b85-111">What you will learn</span></span>
<span data-ttu-id="34b85-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="34b85-112">In this article, you will learn:</span></span>

* <span data-ttu-id="34b85-113">Jak tooinstall Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="34b85-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="34b85-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="34b85-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="34b85-115">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="34b85-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="34b85-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="34b85-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="34b85-117">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="34b85-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="34b85-118">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="34b85-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="34b85-119">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="34b85-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="34b85-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="34b85-120">What you need</span></span>
<span data-ttu-id="34b85-121">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="34b85-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="34b85-122">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="34b85-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="34b85-123">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="34b85-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="34b85-124">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="34b85-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="34b85-125">Skrót klawiaturowy używany hello `Ctrl + Alt + T` tooopen hello terminalu i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="34b85-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="34b85-126">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="34b85-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="34b85-127">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooEdison.</span><span class="sxs-lookup"><span data-stu-id="34b85-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="34b85-128">Zainstaluj `gulp` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="34b85-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="34b85-129">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu Zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="34b85-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="34b85-130">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34b85-130">Install Visual Studio Code</span></span>
<span data-ttu-id="34b85-131">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="34b85-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="34b85-132">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="34b85-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="34b85-133">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="34b85-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="34b85-134">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="34b85-134">Summary</span></span>
<span data-ttu-id="34b85-135">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="34b85-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="34b85-136">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Edison.</span><span class="sxs-lookup"><span data-stu-id="34b85-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34b85-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34b85-137">Next steps</span></span>
<span data-ttu-id="34b85-138">[Tworzenie i wdrażanie hello migania przykładowej aplikacji][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="34b85-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
