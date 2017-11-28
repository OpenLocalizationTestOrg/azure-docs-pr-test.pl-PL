---
title: "Nawiązać Arduino Azure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszego przykładowej aplikacji dla sieci Wi-Fi Adafruit piór M0 na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji dla komputerów mac, zainstaluj node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a6dc2555367e5fe530b3acde1f1f04ac442fb638
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="5ad5c-104">Pobierz narzędzia (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="5ad5c-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5ad5c-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="5ad5c-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="5ad5c-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5ad5c-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5ad5c-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5ad5c-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5ad5c-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5ad5c-108">What you will do</span></span>

<span data-ttu-id="5ad5c-109">Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="5ad5c-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5ad5c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="5ad5c-111">Mimo że język programowania logiki główny Arduino, narzędzia Node.js są używane w wnioski do tworzenia i wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5ad5c-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5ad5c-112">What you will learn</span></span>
<span data-ttu-id="5ad5c-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-113">In this article, you will learn:</span></span>

* <span data-ttu-id="5ad5c-114">Jak zainstalować usługi Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="5ad5c-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="5ad5c-116">Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="5ad5c-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="5ad5c-118">Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="5ad5c-119">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="5ad5c-120">[NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5ad5c-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5ad5c-121">What you need</span></span>
<span data-ttu-id="5ad5c-122">Aby wykonać tę operację, potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="5ad5c-123">Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="5ad5c-124">Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="5ad5c-125">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="5ad5c-125">Install Git and Node.js</span></span>
<span data-ttu-id="5ad5c-126">Aby zainstalować usługi Git i Node.js, użyj [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="5ad5c-127">Instalowanie oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-127">Install Homebrew.</span></span> <span data-ttu-id="5ad5c-128">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-128">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="5ad5c-129">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` otworzyć terminal.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="5ad5c-130">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-130">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="5ad5c-131">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-131">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="5ad5c-132">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="5ad5c-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="5ad5c-133">Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="5ad5c-134">Zainstaluj `gulp`, `device-discovery-cli` , uruchamiając następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="5ad5c-134">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="5ad5c-135">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="5ad5c-136">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ad5c-136">Install Visual Studio Code</span></span>
<span data-ttu-id="5ad5c-137">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="5ad5c-138">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="5ad5c-139">Umożliwia to edytor później w samouczku Edytuj przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="5ad5c-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5ad5c-140">Summary</span></span>
<span data-ttu-id="5ad5c-141">Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="5ad5c-142">Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="5ad5c-142">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ad5c-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ad5c-143">Next steps</span></span>
<span data-ttu-id="5ad5c-144">[Tworzenie i wdrażanie aplikacji migania][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="5ad5c-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md