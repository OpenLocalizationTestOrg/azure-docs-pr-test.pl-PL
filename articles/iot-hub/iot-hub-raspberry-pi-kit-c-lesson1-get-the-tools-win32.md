---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj system git w systemie windows, zainstalowania systemu operacyjnego windows node js, zainstaluj npm w systemie windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="e4a7a-104">Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="e4a7a-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4a7a-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="e4a7a-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="e4a7a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e4a7a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e4a7a-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e4a7a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="e4a7a-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e4a7a-108">What you will do</span></span>
<span data-ttu-id="e4a7a-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="e4a7a-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e4a7a-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e4a7a-111">Mimo że hello język logiki główny hello programowania C, narzędzia Node.js są używane w hello — lekcje toodiscover urządzeń i tworzenia i wdrażania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e4a7a-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e4a7a-112">What you will learn</span></span>
<span data-ttu-id="e4a7a-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e4a7a-113">In this article, you will learn:</span></span>

* <span data-ttu-id="e4a7a-114">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="e4a7a-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e4a7a-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e4a7a-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e4a7a-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="e4a7a-119">Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e4a7a-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e4a7a-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e4a7a-121">What you need</span></span>

<span data-ttu-id="e4a7a-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="e4a7a-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="e4a7a-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="e4a7a-124">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e4a7a-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="e4a7a-125">Install Git and Node.js</span></span>

<span data-ttu-id="e4a7a-126">Kliknij łącza hello poniżej toodownload i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="e4a7a-127">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e4a7a-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="e4a7a-128">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e4a7a-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e4a7a-129">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="e4a7a-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="e4a7a-130">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="e4a7a-131">Użyj hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="e4a7a-132">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="e4a7a-133">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e4a7a-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="e4a7a-134">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e4a7a-135">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4a7a-135">Install Visual Studio Code</span></span>

<span data-ttu-id="e4a7a-136">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="e4a7a-137">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e4a7a-138">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e4a7a-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e4a7a-139">Summary</span></span>

<span data-ttu-id="e4a7a-140">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="e4a7a-141">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="e4a7a-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4a7a-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4a7a-142">Next steps</span></span>

[<span data-ttu-id="e4a7a-143">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="e4a7a-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
