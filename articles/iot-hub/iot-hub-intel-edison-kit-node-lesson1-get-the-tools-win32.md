---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszego Przykładowa aplikacja dla Edison w systemie Windows 7 i nowszych wersjach."
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
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="ffc14-104">Pobierz narzędzia (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="ffc14-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ffc14-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="ffc14-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="ffc14-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ffc14-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ffc14-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ffc14-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ffc14-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="ffc14-108">What you will do</span></span>
<span data-ttu-id="ffc14-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="ffc14-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="ffc14-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ffc14-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ffc14-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="ffc14-111">What you will learn</span></span>
<span data-ttu-id="ffc14-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="ffc14-112">In this article, you will learn:</span></span>

* <span data-ttu-id="ffc14-113">Jak zainstalować usługi Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc14-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="ffc14-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="ffc14-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="ffc14-115">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="ffc14-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="ffc14-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ffc14-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="ffc14-117">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="ffc14-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="ffc14-118">Minimalne wymagania wersji środowiska node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="ffc14-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="ffc14-119">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc14-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ffc14-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="ffc14-120">What you need</span></span>

<span data-ttu-id="ffc14-121">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="ffc14-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="ffc14-122">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="ffc14-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="ffc14-123">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="ffc14-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="ffc14-124">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="ffc14-124">Install Git and Node.js</span></span>

<span data-ttu-id="ffc14-125">Kliknij poniższe łącza, aby pobrać i zainstalować usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ffc14-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="ffc14-126">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ffc14-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="ffc14-127">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ffc14-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="ffc14-128">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="ffc14-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="ffc14-129">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Edison.</span><span class="sxs-lookup"><span data-stu-id="ffc14-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="ffc14-130">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ffc14-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="ffc14-131">Zainstaluj `gulp` , uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ffc14-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="ffc14-132">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="ffc14-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="ffc14-133">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffc14-133">Install Visual Studio Code</span></span>

<span data-ttu-id="ffc14-134">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ffc14-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="ffc14-135">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="ffc14-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="ffc14-136">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="ffc14-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="ffc14-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ffc14-137">Summary</span></span>

<span data-ttu-id="ffc14-138">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="ffc14-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="ffc14-139">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Edison.</span><span class="sxs-lookup"><span data-stu-id="ffc14-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc14-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ffc14-140">Next steps</span></span>

<span data-ttu-id="ffc14-141">[Tworzenie i wdrażanie aplikacji migania][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="ffc14-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
