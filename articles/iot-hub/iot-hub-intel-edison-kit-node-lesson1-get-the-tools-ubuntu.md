---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszego Przykładowa aplikacja dla Edison na Ubuntu."
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
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="99501-104">Pobierz narzędzia (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="99501-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="99501-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="99501-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="99501-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="99501-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="99501-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="99501-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="99501-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="99501-108">What you will do</span></span>
<span data-ttu-id="99501-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla programu Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="99501-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="99501-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="99501-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="99501-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="99501-111">What you will learn</span></span>
<span data-ttu-id="99501-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="99501-112">In this article, you will learn:</span></span>

* <span data-ttu-id="99501-113">Jak zainstalować usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="99501-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="99501-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="99501-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="99501-115">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="99501-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="99501-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="99501-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="99501-117">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="99501-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="99501-118">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="99501-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="99501-119">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="99501-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="99501-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="99501-120">What you need</span></span>
<span data-ttu-id="99501-121">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="99501-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="99501-122">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="99501-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="99501-123">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="99501-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="99501-124">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="99501-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="99501-125">Użyj skrótu klawiaturowego `Ctrl + Alt + T` Otwórz terminal i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="99501-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="99501-126">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="99501-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="99501-127">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Edison.</span><span class="sxs-lookup"><span data-stu-id="99501-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="99501-128">Zainstaluj `gulp` , uruchamiając następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="99501-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="99501-129">Jeśli występują problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="99501-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="99501-130">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99501-130">Install Visual Studio Code</span></span>
<span data-ttu-id="99501-131">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="99501-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="99501-132">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="99501-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="99501-133">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="99501-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="99501-134">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="99501-134">Summary</span></span>
<span data-ttu-id="99501-135">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="99501-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="99501-136">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Edison.</span><span class="sxs-lookup"><span data-stu-id="99501-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99501-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99501-137">Next steps</span></span>
<span data-ttu-id="99501-138">[Tworzenie i wdrażanie migania przykładowej aplikacji][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="99501-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
