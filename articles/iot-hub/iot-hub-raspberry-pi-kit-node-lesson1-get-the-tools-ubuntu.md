---
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na Ubuntu hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj system git, ubuntu, system gulp Uruchom, zainstaluj node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="3db27-104">Pobierz narzędzia hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="3db27-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3db27-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="3db27-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="3db27-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="3db27-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="3db27-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="3db27-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="3db27-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="3db27-108">What you will do</span></span>
<span data-ttu-id="3db27-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="3db27-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="3db27-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3db27-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3db27-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="3db27-111">What you will learn</span></span>
<span data-ttu-id="3db27-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="3db27-112">In this article, you will learn:</span></span>

* <span data-ttu-id="3db27-113">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="3db27-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="3db27-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="3db27-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="3db27-115">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="3db27-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="3db27-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3db27-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="3db27-117">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="3db27-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="3db27-118">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="3db27-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="3db27-119">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="3db27-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="3db27-120">Czego potrzebujesz</span><span class="sxs-lookup"><span data-stu-id="3db27-120">What do you need</span></span>
<span data-ttu-id="3db27-121">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="3db27-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="3db27-122">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3db27-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="3db27-123">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3db27-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="3db27-124">Zainstaluj narzędzia Git, Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="3db27-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="3db27-125">Skrót klawiaturowy używany hello `Ctrl + Alt + T` tooopen hello terminalu i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="3db27-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="3db27-126">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="3db27-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="3db27-127">Możesz użyć [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="3db27-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="3db27-128">Możesz również użyć hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="3db27-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="3db27-129">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="3db27-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="3db27-130">Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="3db27-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="3db27-131">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3db27-131">Install Visual Studio Code</span></span>
<span data-ttu-id="3db27-132">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3db27-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="3db27-133">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="3db27-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3db27-134">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="3db27-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="3db27-135">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3db27-135">Summary</span></span>
<span data-ttu-id="3db27-136">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="3db27-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="3db27-137">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="3db27-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3db27-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3db27-138">Next steps</span></span>
[<span data-ttu-id="3db27-139">Tworzenie i wdrażanie hello migania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3db27-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

