---
title: "Połącz Arduino tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Adafruit piór M0 sieci Wi-Fi w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji w systemie windows, instalowanie node js systemu windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="74537-104">Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="74537-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="74537-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="74537-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="74537-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="74537-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="74537-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="74537-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="74537-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="74537-108">What you will do</span></span>

<span data-ttu-id="74537-109">Pobierz oprogramowanie hello hello pierwszy Przykładowa aplikacja dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="74537-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="74537-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="74537-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="74537-111">Mimo że hello język logiki główny hello programowania Arduino, narzędzia Node.js są używane w toobuild — lekcje hello i wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74537-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="74537-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="74537-112">What you will learn</span></span>
<span data-ttu-id="74537-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="74537-113">In this article, you will learn:</span></span>

* <span data-ttu-id="74537-114">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="74537-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="74537-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="74537-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="74537-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="74537-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="74537-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="74537-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="74537-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="74537-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="74537-119">Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="74537-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="74537-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="74537-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="74537-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="74537-121">What you need</span></span>

<span data-ttu-id="74537-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="74537-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="74537-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="74537-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="74537-124">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="74537-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="74537-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="74537-125">Install Git and Node.js</span></span>

<span data-ttu-id="74537-126">Kliknij łącza hello poniżej toodownload i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="74537-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="74537-127">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="74537-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="74537-128">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="74537-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="74537-129">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="74537-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="74537-130">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooyour Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="74537-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="74537-131">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="74537-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="74537-132">Zainstaluj `gulp`, `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="74537-132">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="74537-133">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="74537-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="74537-134">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74537-134">Install Visual Studio Code</span></span>

<span data-ttu-id="74537-135">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="74537-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="74537-136">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="74537-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="74537-137">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="74537-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="74537-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="74537-138">Summary</span></span>

<span data-ttu-id="74537-139">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="74537-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="74537-140">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="74537-140">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74537-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74537-141">Next steps</span></span>

<span data-ttu-id="74537-142">[Tworzenie i wdrażanie hello migania przykładowej aplikacji][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="74537-142">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md