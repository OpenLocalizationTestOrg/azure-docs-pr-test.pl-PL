---
title: "Connect Intel Edison (C) tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Edison w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji w systemie windows, instalowanie node js systemu windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64d8684ffcb858845de02276a11cf2b2e5c701a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="52a72-104">Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="52a72-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="52a72-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="52a72-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="52a72-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="52a72-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="52a72-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="52a72-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="52a72-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="52a72-108">What you will do</span></span>
<span data-ttu-id="52a72-109">Pobierz narzędzia deweloperskie hello i oprogramowania hello hello pierwszy przykładowej aplikacji Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="52a72-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="52a72-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="52a72-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="52a72-111">Mimo że hello język logiki główny hello programowania C, narzędzia Node.js są używane w toobuild — lekcje hello i wdrażania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="52a72-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="52a72-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="52a72-112">What you will learn</span></span>
<span data-ttu-id="52a72-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="52a72-113">In this article, you will learn:</span></span>

* <span data-ttu-id="52a72-114">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="52a72-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="52a72-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="52a72-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="52a72-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="52a72-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="52a72-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="52a72-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="52a72-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="52a72-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="52a72-119">Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="52a72-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="52a72-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="52a72-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="52a72-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="52a72-121">What you need</span></span>

<span data-ttu-id="52a72-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="52a72-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="52a72-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="52a72-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="52a72-124">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="52a72-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="52a72-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="52a72-125">Install Git and Node.js</span></span>

<span data-ttu-id="52a72-126">Kliknij łącza hello poniżej toodownload i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="52a72-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="52a72-127">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="52a72-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="52a72-128">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="52a72-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="52a72-129">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="52a72-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="52a72-130">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooEdison.</span><span class="sxs-lookup"><span data-stu-id="52a72-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="52a72-131">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="52a72-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="52a72-132">Zainstaluj `gulp` , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="52a72-132">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="52a72-133">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="52a72-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="52a72-134">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52a72-134">Install Visual Studio Code</span></span>

<span data-ttu-id="52a72-135">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="52a72-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="52a72-136">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="52a72-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="52a72-137">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="52a72-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="52a72-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="52a72-138">Summary</span></span>

<span data-ttu-id="52a72-139">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="52a72-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="52a72-140">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Edison.</span><span class="sxs-lookup"><span data-stu-id="52a72-140">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52a72-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52a72-141">Next steps</span></span>

<span data-ttu-id="52a72-142">[Tworzenie i wdrażanie aplikacji migania hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="52a72-142">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
