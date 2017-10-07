---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia na komputerze Mac, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
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
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="43305-104">Pobierz narzędzia hello (macOS)</span><span class="sxs-lookup"><span data-stu-id="43305-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43305-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="43305-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="43305-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="43305-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="43305-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="43305-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="43305-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="43305-108">What you will do</span></span>

- <span data-ttu-id="43305-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="43305-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="43305-110">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="43305-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="43305-111">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="43305-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="43305-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="43305-112">What you will learn</span></span>

<span data-ttu-id="43305-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="43305-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="43305-114">Jak tooinstall [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="43305-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="43305-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="43305-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="43305-116">Witaj Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="43305-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="43305-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="43305-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="43305-118">Jak toouse [NPM](https://www.npmjs.com/) tooinstall narzędzi do tworzenia środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="43305-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="43305-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="43305-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="43305-120">NPM jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="43305-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="43305-121">Jak tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="43305-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="43305-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="43305-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="43305-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="43305-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="43305-124">Jak tooinstall języka Python.</span><span class="sxs-lookup"><span data-stu-id="43305-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="43305-125">Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="43305-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="43305-126">Jak tooinstall hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43305-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="43305-127">Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43305-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="43305-128">Praca bezpośrednio z tooprovision wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="43305-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="43305-129">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="43305-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="43305-130">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="43305-130">What you need</span></span>

- <span data-ttu-id="43305-131">Toodownload połączenia internetowego hello i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="43305-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="43305-132">Komputer Mac z systemem OS X Yosemite (10.10) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="43305-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="43305-133">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="43305-133">Install Git and Node.js</span></span>

<span data-ttu-id="43305-134">tooinstall Git i Node.js, należy użyć narzędzia zarządzania pakietów oprogramowania Homebrew hello, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="43305-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="43305-135">[Pobierz](http://brew.sh/) i zainstalowania oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="43305-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="43305-136">Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź toostep 2.</span><span class="sxs-lookup"><span data-stu-id="43305-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="43305-137">Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` tooopen terminalu.</span><span class="sxs-lookup"><span data-stu-id="43305-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="43305-138">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="43305-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="43305-139">Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="43305-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="43305-140">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="43305-140">Install Node.js development tools</span></span>

<span data-ttu-id="43305-141">Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="43305-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="43305-142">gulp tooinstall, uruchom następujące polecenie w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="43305-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="43305-143">Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="43305-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="43305-144">Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="43305-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="43305-145">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="43305-145">Install Python</span></span>

<span data-ttu-id="43305-146">Mimo że systemu Mac OS X jest dostarczany z Python 2.7, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="43305-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="43305-147">Zobacz [instalacji języka Python w systemie Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="43305-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="43305-148">Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="43305-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="43305-149">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43305-149">Install hello Azure CLI</span></span>

<span data-ttu-id="43305-150">Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="43305-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="43305-151">Uruchom następujące polecenia w terminalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="43305-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="43305-152">Witaj, instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="43305-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="43305-153">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="43305-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="43305-154">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="43305-154">You should see hello following output if hello installation is successful.</span></span>

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="43305-156">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43305-156">Install Visual Studio Code</span></span>

<span data-ttu-id="43305-157">W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.</span><span class="sxs-lookup"><span data-stu-id="43305-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="43305-158">[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="43305-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="43305-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="43305-159">Summary</span></span>

<span data-ttu-id="43305-160">Na komputerze Mac, że zainstalowano wszystkie wymagane hello i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="43305-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="43305-161">Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="43305-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43305-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43305-162">Next steps</span></span>
[<span data-ttu-id="43305-163">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="43305-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
