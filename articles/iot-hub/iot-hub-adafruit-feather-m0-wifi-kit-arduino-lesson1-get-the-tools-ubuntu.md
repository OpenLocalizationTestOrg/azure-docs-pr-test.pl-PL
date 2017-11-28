---
title: "Połącz Arduino tooAzure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji sieci Wi-Fi Adafruit piór M0 na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowania, git instalacji na ubuntu, ubuntu js węzła instalacji"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 586f89025d2fa11a31cb782e3789d306ade018a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="a7d70-104">Pobierz narzędzia hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="a7d70-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="a7d70-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="a7d70-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a7d70-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a7d70-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a7d70-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a7d70-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a7d70-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="a7d70-108">What you will do</span></span>

<span data-ttu-id="a7d70-109">Pobierz oprogramowanie hello hello pierwszy Przykładowa aplikacja dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="a7d70-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="a7d70-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a7d70-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="a7d70-111">Mimo że hello język logiki główny hello programowania Arduino, narzędzia Node.js są używane w toobuild — lekcje hello i wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7d70-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7d70-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="a7d70-112">What you will learn</span></span>
<span data-ttu-id="a7d70-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="a7d70-113">In this article, you will learn:</span></span>

* <span data-ttu-id="a7d70-114">Jak tooinstall Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="a7d70-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="a7d70-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="a7d70-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a7d70-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="a7d70-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a7d70-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="a7d70-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a7d70-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="a7d70-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a7d70-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a7d70-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a7d70-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a7d70-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7d70-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="a7d70-121">What you need</span></span>
<span data-ttu-id="a7d70-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="a7d70-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="a7d70-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="a7d70-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a7d70-124">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a7d70-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="a7d70-125">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="a7d70-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="a7d70-126">Skrót klawiaturowy używany hello `Ctrl + Alt + T` tooopen hello terminalu i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7d70-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a7d70-127">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="a7d70-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="a7d70-128">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooyour Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="a7d70-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="a7d70-129">Zainstaluj `gulp`, `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="a7d70-129">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="a7d70-130">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu Zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="a7d70-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a7d70-131">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7d70-131">Install Visual Studio Code</span></span>
<span data-ttu-id="a7d70-132">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a7d70-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="a7d70-133">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="a7d70-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a7d70-134">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="a7d70-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a7d70-135">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a7d70-135">Summary</span></span>
<span data-ttu-id="a7d70-136">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="a7d70-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a7d70-137">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="a7d70-137">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7d70-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7d70-138">Next steps</span></span>
<span data-ttu-id="a7d70-139">[Tworzenie i wdrażanie hello migania przykładowej aplikacji][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="a7d70-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md