---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia na komputerze Mac, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowanie iot, iot usługi w chmurze internet rzeczy oprogramowania, interfejsu wiersza polecenia platformy azure, zainstaluj mac python, zainstaluj usługę git dla komputerów mac, gulp, uruchom instalację node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="bbe7d-104">Pobierz narzędzia (macOS)</span><span class="sxs-lookup"><span data-stu-id="bbe7d-104">Get the tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bbe7d-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="bbe7d-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="bbe7d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bbe7d-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="bbe7d-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="bbe7d-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="bbe7d-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="bbe7d-108">What you will do</span></span>

- <span data-ttu-id="bbe7d-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="bbe7d-110">Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="bbe7d-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="bbe7d-111">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bbe7d-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bbe7d-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="bbe7d-112">What you will learn</span></span>

<span data-ttu-id="bbe7d-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="bbe7d-114">Jak zainstalować [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="bbe7d-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="bbe7d-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="bbe7d-116">Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="bbe7d-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="bbe7d-118">Jak używać [NPM](https://www.npmjs.com/) do instalowania narzędzi do tworzenia środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="bbe7d-119">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="bbe7d-120">NPM jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="bbe7d-121">Jak zainstalować program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="bbe7d-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bbe7d-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="bbe7d-124">Jak zainstalować Python.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-124">How to install Python.</span></span>
  - <span data-ttu-id="bbe7d-125">Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="bbe7d-126">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="bbe7d-127">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="bbe7d-128">Praca bezpośrednio z poziomu wiersza polecenia do udostępniania i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="bbe7d-129">Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bbe7d-130">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="bbe7d-130">What you need</span></span>

- <span data-ttu-id="bbe7d-131">Połączenia internetowego do pobierania narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="bbe7d-132">Komputer Mac z systemem OS X Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bbe7d-133">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="bbe7d-133">Install Git and Node.js</span></span>

<span data-ttu-id="bbe7d-134">Aby zainstalować usługi Git i Node.js, należy użyć narzędzia zarządzania pakietów oprogramowania Homebrew wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="bbe7d-135">[Pobierz](http://brew.sh/) i zainstalowania oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="bbe7d-136">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="bbe7d-137">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` otworzyć terminal.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="bbe7d-138">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="bbe7d-139">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="bbe7d-140">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="bbe7d-140">Install Node.js development tools</span></span>

<span data-ttu-id="bbe7d-141">Możesz użyć [gulp.js](http://gulpjs.com/) do automatyzowania wdrażania i uruchamiania skryptów.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="bbe7d-142">Aby zainstalować gulp, uruchom następujące polecenie z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="bbe7d-143">Jeśli występują problemy z instalacją, zobacz [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="bbe7d-144">Węzeł, NPM i Gulp są wymagane do uruchamiania skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="bbe7d-145">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="bbe7d-145">Install Python</span></span>

<span data-ttu-id="bbe7d-146">Mimo że systemu Mac OS X jest dostarczany z Python 2.7, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="bbe7d-147">Zobacz [instalacji języka Python w systemie Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="bbe7d-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="bbe7d-148">Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="bbe7d-149">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bbe7d-149">Install the Azure CLI</span></span>

<span data-ttu-id="bbe7d-150">Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="bbe7d-151">Uruchom następujące polecenia z poziomu terminala:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="bbe7d-152">Instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="bbe7d-153">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bbe7d-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="bbe7d-154">Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-154">You should see the following output if the installation is successful.</span></span>

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="bbe7d-156">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbe7d-156">Install Visual Studio Code</span></span>

<span data-ttu-id="bbe7d-157">Używasz programu Visual Studio Code później w samouczku do edycji plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="bbe7d-158">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="bbe7d-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="bbe7d-159">Summary</span></span>

<span data-ttu-id="bbe7d-160">Na komputerze Mac, że zainstalowano wszystkie wymagane narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="bbe7d-161">Następnym zadaniem jest korzystanie z wiersza polecenia platformy Azure w celu tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bbe7d-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbe7d-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbe7d-162">Next steps</span></span>
[<span data-ttu-id="bbe7d-163">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="bbe7d-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
