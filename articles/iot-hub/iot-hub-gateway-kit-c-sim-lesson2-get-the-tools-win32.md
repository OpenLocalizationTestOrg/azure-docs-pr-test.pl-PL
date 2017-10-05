---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia i oprogramowania na komputerze hosta z systemem Windows, Utwórz Centrum IoT i zarejestrować urządzenie w Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj oprogramowanie git w systemie windows, system gulp Uruchom, zainstalowania systemu operacyjnego windows node js, instalowania npm w systemie windows, zainstaluj python w systemie windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="d0e93-104">Pobierz narzędzia (z systemem Windows 7 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="d0e93-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0e93-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="d0e93-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="d0e93-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d0e93-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="d0e93-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="d0e93-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="d0e93-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="d0e93-108">What you will do</span></span>

- <span data-ttu-id="d0e93-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="d0e93-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="d0e93-110">Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d0e93-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="d0e93-111">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d0e93-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d0e93-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d0e93-112">What you will learn</span></span>

<span data-ttu-id="d0e93-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="d0e93-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="d0e93-114">Jak zainstalować [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="d0e93-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="d0e93-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="d0e93-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="d0e93-116">Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="d0e93-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="d0e93-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0e93-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="d0e93-118">Jak używać [NPM](https://www.npmjs.com/) do instalowania narzędzi do tworzenia środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="d0e93-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="d0e93-119">Minimalna wymagana wersja programu Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="d0e93-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="d0e93-120">NPM jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="d0e93-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="d0e93-121">Jak zainstalować program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d0e93-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="d0e93-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="d0e93-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="d0e93-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="d0e93-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="d0e93-124">Jak zainstalować Python.</span><span class="sxs-lookup"><span data-stu-id="d0e93-124">How to install Python.</span></span>
  - <span data-ttu-id="d0e93-125">Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="d0e93-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="d0e93-126">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e93-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="d0e93-127">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e93-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="d0e93-128">Praca bezpośrednio z poziomu wiersza polecenia do udostępniania i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="d0e93-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="d0e93-129">Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d0e93-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d0e93-130">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="d0e93-130">What you need</span></span>

- <span data-ttu-id="d0e93-131">Połączenia internetowego do pobierania narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="d0e93-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="d0e93-132">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="d0e93-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="d0e93-133">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="d0e93-133">Install Git and Node.js</span></span>

<span data-ttu-id="d0e93-134">Kliknij poniższe łącza, aby pobrać i zainstalować usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d0e93-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="d0e93-135">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d0e93-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="d0e93-136">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d0e93-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="d0e93-137">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="d0e93-137">Install Node.js development tools</span></span>

<span data-ttu-id="d0e93-138">Możesz użyć [gulp.js](http://gulpjs.com/) do automatyzowania wdrażania i uruchamiania skryptów.</span><span class="sxs-lookup"><span data-stu-id="d0e93-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="d0e93-139">Naciśnij klawisz `Windows + R`, typ `cmd` i naciśnij klawisz `Enter` aby otworzyć okno wiersza polecenia, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d0e93-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="d0e93-140">Jeśli występują problemy z instalacją, zobacz [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="d0e93-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="d0e93-141">Węzeł, NPM i Gulp są wymagane do uruchamiania skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="d0e93-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="d0e93-142">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="d0e93-142">Install Python</span></span>

<span data-ttu-id="d0e93-143">Można wybrać z Python 2.7 3.4 lub 3.5.</span><span class="sxs-lookup"><span data-stu-id="d0e93-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="d0e93-144">W tym samouczku używamy Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="d0e93-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="d0e93-145">Jeśli po zainstalowaniu języka python, przejdź do następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d0e93-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="d0e93-146">Pobierz języka Python dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d0e93-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="d0e93-147">Należy również dodać ścieżkę do folderów, w którym Python.exe i pip.exe są zainstalowane w systemie `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="d0e93-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="d0e93-148">Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="d0e93-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="d0e93-149">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d0e93-149">Install the Azure CLI</span></span>

<span data-ttu-id="d0e93-150">Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0e93-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="d0e93-151">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="d0e93-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="d0e93-152">Instalowanie interfejsu wiersza polecenia Azure, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d0e93-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="d0e93-153">Instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="d0e93-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="d0e93-154">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d0e93-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="d0e93-155">Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d0e93-155">You should see the following output if the installation is successful.</span></span>

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="d0e93-157">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0e93-157">Install Visual Studio Code</span></span>

<span data-ttu-id="d0e93-158">Używasz programu Visual Studio Code później w samouczku do edycji plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d0e93-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="d0e93-159">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d0e93-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="d0e93-160">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d0e93-160">Summary</span></span>

<span data-ttu-id="d0e93-161">Po zainstalowaniu wszystkich wymaganych narzędzi i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="d0e93-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="d0e93-162">Następnym zadaniem jest korzystanie z wiersza polecenia platformy Azure w celu tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d0e93-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e93-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0e93-163">Next steps</span></span>
<span data-ttu-id="d0e93-164">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="d0e93-164">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>
