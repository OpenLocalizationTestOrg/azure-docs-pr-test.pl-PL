---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na Ubuntu hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi."
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
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="17ac2-104">Pobierz narzędzia hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="17ac2-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17ac2-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="17ac2-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="17ac2-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="17ac2-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="17ac2-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="17ac2-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="17ac2-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="17ac2-108">What you will do</span></span>
<span data-ttu-id="17ac2-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji sieci malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="17ac2-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="17ac2-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="17ac2-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17ac2-111">Mimo że hello język logiki główny hello programowania C, narzędzia Node.js są używane w hello — lekcje toodiscover urządzeń i tworzenia i wdrażania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="17ac2-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="17ac2-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="17ac2-112">What you will learn</span></span>
<span data-ttu-id="17ac2-113">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="17ac2-113">In this article, you will learn:</span></span>

* <span data-ttu-id="17ac2-114">Jak tooinstall Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="17ac2-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="17ac2-115">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="17ac2-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="17ac2-116">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="17ac2-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="17ac2-117">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="17ac2-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="17ac2-118">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="17ac2-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="17ac2-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="17ac2-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="17ac2-120">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="17ac2-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="17ac2-121">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="17ac2-121">What you need</span></span>
<span data-ttu-id="17ac2-122">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="17ac2-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="17ac2-123">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="17ac2-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="17ac2-124">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="17ac2-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="17ac2-125">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="17ac2-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="17ac2-126">Skrót klawiaturowy używany hello `Ctrl + Alt + T` tooopen hello terminalu i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="17ac2-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="17ac2-127">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="17ac2-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="17ac2-128">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="17ac2-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="17ac2-129">Użyj hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="17ac2-129">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="17ac2-130">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="17ac2-130">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="17ac2-131">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="17ac2-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="17ac2-132">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17ac2-132">Install Visual Studio Code</span></span>
<span data-ttu-id="17ac2-133">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="17ac2-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="17ac2-134">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="17ac2-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="17ac2-135">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="17ac2-135">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="17ac2-136">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="17ac2-136">Summary</span></span>
<span data-ttu-id="17ac2-137">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="17ac2-137">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="17ac2-138">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="17ac2-138">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ac2-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17ac2-139">Next steps</span></span>
[<span data-ttu-id="17ac2-140">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="17ac2-140">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

