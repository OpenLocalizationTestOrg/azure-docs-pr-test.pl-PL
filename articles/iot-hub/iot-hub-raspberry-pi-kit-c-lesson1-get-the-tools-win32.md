---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej pi w systemie Windows 7 i nowszych wersjach."
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
ms.openlocfilehash: 0e58975f4411f97223b2c4374bdd746fe6628c42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="c8dd1-104">Pobierz narzędzia (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="c8dd1-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8dd1-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="c8dd1-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="c8dd1-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c8dd1-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="c8dd1-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="c8dd1-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="c8dd1-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="c8dd1-108">What you will do</span></span>
<span data-ttu-id="c8dd1-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="c8dd1-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c8dd1-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c8dd1-111">Mimo że logiki główny język programowania C, narzędzia Node.js są używane w wnioski do odnajdywania urządzeń i tworzenia i wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c8dd1-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="c8dd1-112">What you will learn</span></span>
<span data-ttu-id="c8dd1-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="c8dd1-113">In this article, you will learn:</span></span>

* <span data-ttu-id="c8dd1-114">Jak zainstalować usługi Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="c8dd1-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="c8dd1-116">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="c8dd1-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="c8dd1-118">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="c8dd1-119">Minimalne wymagania wersji środowiska node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="c8dd1-120">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c8dd1-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="c8dd1-121">What you need</span></span>

<span data-ttu-id="c8dd1-122">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="c8dd1-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="c8dd1-123">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="c8dd1-124">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c8dd1-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="c8dd1-125">Install Git and Node.js</span></span>

<span data-ttu-id="c8dd1-126">Kliknij poniższe łącza, aby pobrać i zainstalować usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="c8dd1-127">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c8dd1-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="c8dd1-128">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c8dd1-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="c8dd1-129">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="c8dd1-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="c8dd1-130">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Pi.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="c8dd1-131">Użyj [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) można pobrać informacji o sieci o urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-131">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="c8dd1-132">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="c8dd1-133">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c8dd1-133">Install `gulp` and `device-discovery-cli` by running the following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="c8dd1-134">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="c8dd1-135">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c8dd1-135">Install Visual Studio Code</span></span>

<span data-ttu-id="c8dd1-136">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="c8dd1-137">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c8dd1-138">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="c8dd1-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c8dd1-139">Summary</span></span>

<span data-ttu-id="c8dd1-140">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="c8dd1-141">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="c8dd1-141">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8dd1-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8dd1-142">Next steps</span></span>

[<span data-ttu-id="c8dd1-143">Tworzenie i wdrażanie aplikacji blink</span><span class="sxs-lookup"><span data-stu-id="c8dd1-143">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
