---
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj usługę git w systemie windows, system gulp uruchomienia, zainstalowania systemu operacyjnego windows node js, instalowania npm w systemie windows, zainstaluj python w systemie windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="413cc-104">Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="413cc-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="413cc-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="413cc-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="413cc-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="413cc-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="413cc-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="413cc-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="413cc-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="413cc-108">What you will do</span></span>
<span data-ttu-id="413cc-109">Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji malina Pi 3 i narzędzia deweloperskie hello.</span><span class="sxs-lookup"><span data-stu-id="413cc-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="413cc-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="413cc-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="413cc-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="413cc-111">What you will learn</span></span>
<span data-ttu-id="413cc-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="413cc-112">In this article, you will learn:</span></span>

* <span data-ttu-id="413cc-113">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="413cc-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="413cc-114">[Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="413cc-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="413cc-115">Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.</span><span class="sxs-lookup"><span data-stu-id="413cc-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="413cc-116">[Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="413cc-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="413cc-117">Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="413cc-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="413cc-118">Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="413cc-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="413cc-119">[NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="413cc-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="413cc-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="413cc-120">What you need</span></span>
<span data-ttu-id="413cc-121">toocomplete tej operacji, należy:</span><span class="sxs-lookup"><span data-stu-id="413cc-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="413cc-122">Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="413cc-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="413cc-123">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="413cc-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="413cc-124">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="413cc-124">Install Git and Node.js</span></span>
<span data-ttu-id="413cc-125">Kliknij następujące łącza toodownload hello i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="413cc-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="413cc-126">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="413cc-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="413cc-127">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="413cc-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="413cc-128">Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="413cc-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="413cc-129">Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="413cc-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="413cc-130">Możesz również użyć hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="413cc-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="413cc-131">Uruchom wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="413cc-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="413cc-132">Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="413cc-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="413cc-133">Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="413cc-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="413cc-134">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="413cc-134">Install Visual Studio Code</span></span>
<span data-ttu-id="413cc-135">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="413cc-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="413cc-136">Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="413cc-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="413cc-137">Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="413cc-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="413cc-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="413cc-138">Summary</span></span>
<span data-ttu-id="413cc-139">Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="413cc-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="413cc-140">następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="413cc-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="413cc-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="413cc-141">Next steps</span></span>
[<span data-ttu-id="413cc-142">Tworzenie i wdrażanie hello migania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="413cc-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

