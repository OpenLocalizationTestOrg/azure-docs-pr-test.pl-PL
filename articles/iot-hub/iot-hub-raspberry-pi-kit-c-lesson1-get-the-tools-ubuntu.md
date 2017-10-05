---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej pi na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj system git, ubuntu, system gulp Uruchom, zainstaluj node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="757ea-104">Pobierz narzędzia (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="757ea-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="757ea-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="757ea-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="757ea-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="757ea-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="757ea-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="757ea-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="757ea-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="757ea-108">What you will do</span></span>
<span data-ttu-id="757ea-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla programu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="757ea-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="757ea-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="757ea-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="757ea-111">Mimo że logiki główny język programowania C, narzędzia Node.js są używane w wnioski do odnajdywania urządzeń i tworzenia i wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="757ea-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="757ea-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="757ea-112">What you will learn</span></span>
<span data-ttu-id="757ea-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="757ea-113">In this article, you will learn:</span></span>

* <span data-ttu-id="757ea-114">Jak zainstalować usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="757ea-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="757ea-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="757ea-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="757ea-116">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="757ea-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="757ea-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="757ea-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="757ea-118">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="757ea-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="757ea-119">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="757ea-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="757ea-120">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="757ea-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="757ea-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="757ea-121">What you need</span></span>
<span data-ttu-id="757ea-122">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="757ea-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="757ea-123">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="757ea-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="757ea-124">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="757ea-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="757ea-125">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="757ea-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="757ea-126">Użyj skrótu klawiaturowego `Ctrl + Alt + T` Otwórz terminal i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="757ea-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="757ea-127">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="757ea-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="757ea-128">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Pi.</span><span class="sxs-lookup"><span data-stu-id="757ea-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="757ea-129">Użyj [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) można pobrać informacji o sieci o urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="757ea-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="757ea-130">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="757ea-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="757ea-131">Jeśli występują problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu, zobacz [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="757ea-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="757ea-132">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="757ea-132">Install Visual Studio Code</span></span>
<span data-ttu-id="757ea-133">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="757ea-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="757ea-134">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="757ea-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="757ea-135">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="757ea-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="757ea-136">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="757ea-136">Summary</span></span>
<span data-ttu-id="757ea-137">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="757ea-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="757ea-138">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="757ea-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="757ea-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="757ea-139">Next steps</span></span>
[<span data-ttu-id="757ea-140">Tworzenie i wdrażanie aplikacji blink</span><span class="sxs-lookup"><span data-stu-id="757ea-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

