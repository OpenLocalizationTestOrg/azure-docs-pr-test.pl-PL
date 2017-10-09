---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia hello i hello oprogramowania na komputerze hosta z systemem Ubuntu, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj system git, ubuntu, system gulp uruchomienia, zainstaluj node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="3f53b-104">Pobierz narzędzia hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="3f53b-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f53b-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="3f53b-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="3f53b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="3f53b-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="3f53b-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="3f53b-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="3f53b-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="3f53b-108">What you will do</span></span>

- <span data-ttu-id="3f53b-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="3f53b-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="3f53b-110">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="3f53b-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="3f53b-111">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3f53b-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="3f53b-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="3f53b-112">What you will learn</span></span>

<span data-ttu-id="3f53b-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="3f53b-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="3f53b-114">Jak tooinstall Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="3f53b-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="3f53b-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="3f53b-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="3f53b-116">Witaj Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="3f53b-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="3f53b-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3f53b-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="3f53b-118">Jak narzędzia deweloperskie toouse NPM tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="3f53b-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="3f53b-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="3f53b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="3f53b-120">NPM jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="3f53b-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="3f53b-121">Jak tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3f53b-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="3f53b-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="3f53b-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3f53b-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="3f53b-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="3f53b-124">Jak tooinstall hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3f53b-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="3f53b-125">Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f53b-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="3f53b-126">Praca bezpośrednio z tooprovision wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="3f53b-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="3f53b-127">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f53b-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3f53b-128">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="3f53b-128">What you need</span></span>

- <span data-ttu-id="3f53b-129">Toodownload połączenia internetowego hello i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3f53b-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="3f53b-130">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3f53b-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="3f53b-131">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="3f53b-131">Install Git and Node.js</span></span>

<span data-ttu-id="3f53b-132">tooinstall Git i Node.js, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3f53b-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="3f53b-133">Naciśnij klawisz `Ctrl + Alt + T` tooopen terminalu.</span><span class="sxs-lookup"><span data-stu-id="3f53b-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="3f53b-134">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3f53b-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="3f53b-135">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="3f53b-135">Install Node.js development tools</span></span>

<span data-ttu-id="3f53b-136">Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="3f53b-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="3f53b-137">gulp tooinstall, uruchom następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="3f53b-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="3f53b-138">Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="3f53b-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="3f53b-139">Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="3f53b-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="3f53b-140">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3f53b-140">Install hello Azure CLI</span></span>

<span data-ttu-id="3f53b-141">Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3f53b-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="3f53b-142">Uruchom następujące polecenia w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="3f53b-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="3f53b-143">Witaj, instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="3f53b-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="3f53b-144">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="3f53b-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="3f53b-145">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="3f53b-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="3f53b-146">![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="3f53b-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="3f53b-147">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f53b-147">Install Visual Studio Code</span></span>

<span data-ttu-id="3f53b-148">W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.</span><span class="sxs-lookup"><span data-stu-id="3f53b-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="3f53b-149">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3f53b-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="3f53b-150">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3f53b-150">Summary</span></span>

<span data-ttu-id="3f53b-151">Po zainstalowaniu wszystkich wymaganych hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="3f53b-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="3f53b-152">Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="3f53b-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f53b-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f53b-153">Next steps</span></span>
<span data-ttu-id="3f53b-154">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="3f53b-154">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>
