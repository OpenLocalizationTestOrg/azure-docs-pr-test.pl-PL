---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia i oprogramowania na komputerze hosta z systemem Ubuntu, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj system git, ubuntu, system gulp uruchomienia, zainstaluj node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="f90b5-104">Pobierz narzędzia (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="f90b5-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f90b5-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f90b5-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="f90b5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f90b5-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f90b5-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f90b5-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f90b5-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="f90b5-108">What you will do</span></span>

- <span data-ttu-id="f90b5-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="f90b5-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="f90b5-110">Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f90b5-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="f90b5-111">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f90b5-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="f90b5-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="f90b5-112">What you will learn</span></span>

<span data-ttu-id="f90b5-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f90b5-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f90b5-114">Jak zainstalować usługi Git i Node.js.</span><span class="sxs-lookup"><span data-stu-id="f90b5-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="f90b5-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="f90b5-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="f90b5-116">Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="f90b5-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="f90b5-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="f90b5-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="f90b5-118">Sposób instalowania narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.</span><span class="sxs-lookup"><span data-stu-id="f90b5-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="f90b5-119">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f90b5-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="f90b5-120">NPM jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="f90b5-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="f90b5-121">Jak zainstalować program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f90b5-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="f90b5-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="f90b5-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f90b5-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="f90b5-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="f90b5-124">Jak zainstalować wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f90b5-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="f90b5-125">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f90b5-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f90b5-126">Praca bezpośrednio z poziomu wiersza polecenia do udostępniania i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="f90b5-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="f90b5-127">Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f90b5-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f90b5-128">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="f90b5-128">What you need</span></span>

- <span data-ttu-id="f90b5-129">Połączenia internetowego do pobierania narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="f90b5-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="f90b5-130">Komputer z systemem Ubuntu 16.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f90b5-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f90b5-131">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="f90b5-131">Install Git and Node.js</span></span>

<span data-ttu-id="f90b5-132">Aby zainstalować usługi Git i Node.js, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f90b5-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="f90b5-133">Naciśnij klawisz `Ctrl + Alt + T` otworzyć terminal.</span><span class="sxs-lookup"><span data-stu-id="f90b5-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="f90b5-134">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="f90b5-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="f90b5-135">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="f90b5-135">Install Node.js development tools</span></span>

<span data-ttu-id="f90b5-136">Możesz użyć [gulp.js](http://gulpjs.com/) do automatyzowania wdrażania i uruchamiania skryptów.</span><span class="sxs-lookup"><span data-stu-id="f90b5-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="f90b5-137">Aby zainstalować gulp, uruchom następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="f90b5-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="f90b5-138">Jeśli występują problemy z instalacją, zobacz [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="f90b5-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="f90b5-139">Węzeł, NPM i Gulp są wymagane do uruchamiania skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="f90b5-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="f90b5-140">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f90b5-140">Install the Azure CLI</span></span>

<span data-ttu-id="f90b5-141">Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f90b5-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f90b5-142">Uruchom następujące polecenia z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="f90b5-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="f90b5-143">Instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="f90b5-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="f90b5-144">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f90b5-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="f90b5-145">Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="f90b5-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="f90b5-146">![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="f90b5-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="f90b5-147">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f90b5-147">Install Visual Studio Code</span></span>

<span data-ttu-id="f90b5-148">Używasz programu Visual Studio Code później w samouczku do edycji plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f90b5-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="f90b5-149">[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f90b5-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="f90b5-150">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f90b5-150">Summary</span></span>

<span data-ttu-id="f90b5-151">Po zainstalowaniu wszystkich wymaganych narzędzi i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="f90b5-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="f90b5-152">Następnym zadaniem jest korzystanie z wiersza polecenia platformy Azure w celu tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f90b5-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f90b5-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f90b5-153">Next steps</span></span>
<span data-ttu-id="f90b5-154">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="f90b5-154">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>
