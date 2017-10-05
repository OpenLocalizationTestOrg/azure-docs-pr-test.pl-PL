---
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej pi na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, instalowanie python mac, zainstaluj usługę git dla komputerów mac, system gulp Uruchom i zainstalować node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="581e7-104">Pobierz narzędzia (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="581e7-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="581e7-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="581e7-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="581e7-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="581e7-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="581e7-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="581e7-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="581e7-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="581e7-108">What you will do</span></span>
<span data-ttu-id="581e7-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla programu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="581e7-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="581e7-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="581e7-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="581e7-111">What you will learn</span></span>
<span data-ttu-id="581e7-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="581e7-112">In this article, you will learn:</span></span>

* <span data-ttu-id="581e7-113">Jak zainstalować usługi Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="581e7-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="581e7-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="581e7-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="581e7-115">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="581e7-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="581e7-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="581e7-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="581e7-117">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="581e7-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="581e7-118">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="581e7-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="581e7-119">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="581e7-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="581e7-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="581e7-120">What you need</span></span>
<span data-ttu-id="581e7-121">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="581e7-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="581e7-122">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="581e7-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="581e7-123">Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="581e7-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="581e7-124">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="581e7-124">Install Git and Node.js</span></span>
<span data-ttu-id="581e7-125">Aby zainstalować usługi Git i Node.js, użyj [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="581e7-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="581e7-126">Instalowanie oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="581e7-126">Install Homebrew.</span></span> <span data-ttu-id="581e7-127">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="581e7-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="581e7-128">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` otworzyć terminal.</span><span class="sxs-lookup"><span data-stu-id="581e7-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="581e7-129">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="581e7-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="581e7-130">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="581e7-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="581e7-131">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="581e7-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="581e7-132">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Pi.</span><span class="sxs-lookup"><span data-stu-id="581e7-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="581e7-133">Użyj [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) można pobrać informacji o sieci o urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="581e7-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="581e7-134">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="581e7-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="581e7-135">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS zobacz [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="581e7-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="581e7-136">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="581e7-136">Install Visual Studio Code</span></span>
<span data-ttu-id="581e7-137">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="581e7-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="581e7-138">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="581e7-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="581e7-139">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="581e7-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="581e7-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="581e7-140">Summary</span></span>
<span data-ttu-id="581e7-141">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="581e7-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="581e7-142">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="581e7-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="581e7-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="581e7-143">Next steps</span></span>
[<span data-ttu-id="581e7-144">Tworzenie i wdrażanie migania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="581e7-144">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

