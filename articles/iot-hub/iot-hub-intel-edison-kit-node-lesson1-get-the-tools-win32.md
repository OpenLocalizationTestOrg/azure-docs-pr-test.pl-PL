---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Edison w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji w systemie windows, instalowanie node js systemu windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="c646a-104">Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="c646a-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c646a-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="c646a-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="c646a-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="c646a-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="c646a-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="c646a-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c646a-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="c646a-108">What you will do</span></span>
<span data-ttu-id="c646a-109">Pobierz narzędzia deweloperskie hello i oprogramowania hello hello pierwszy przykładowej aplikacji Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="c646a-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="c646a-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c646a-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c646a-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="c646a-111">What you will learn</span></span>
<span data-ttu-id="c646a-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="c646a-112">In this article, you will learn:</span></span>

* <span data-ttu-id="c646a-113">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="c646a-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="c646a-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="c646a-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="c646a-115">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="c646a-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="c646a-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="c646a-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="c646a-117">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="c646a-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="c646a-118">Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c646a-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="c646a-119">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="c646a-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c646a-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="c646a-120">What you need</span></span>

<span data-ttu-id="c646a-121">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="c646a-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="c646a-122">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="c646a-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="c646a-123">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c646a-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c646a-124">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="c646a-124">Install Git and Node.js</span></span>

<span data-ttu-id="c646a-125">Kliknij łącza hello poniżej toodownload i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c646a-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="c646a-126">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c646a-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="c646a-127">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c646a-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="c646a-128">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="c646a-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="c646a-129">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooEdison.</span><span class="sxs-lookup"><span data-stu-id="c646a-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="c646a-130">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c646a-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="c646a-131">Zainstaluj `gulp` , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c646a-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="c646a-132">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="c646a-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="c646a-133">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c646a-133">Install Visual Studio Code</span></span>

<span data-ttu-id="c646a-134">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c646a-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="c646a-135">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="c646a-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c646a-136">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="c646a-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="c646a-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c646a-137">Summary</span></span>

<span data-ttu-id="c646a-138">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="c646a-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="c646a-139">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Edison.</span><span class="sxs-lookup"><span data-stu-id="c646a-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c646a-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c646a-140">Next steps</span></span>

<span data-ttu-id="c646a-141">[Tworzenie i wdrażanie aplikacji migania hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="c646a-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
