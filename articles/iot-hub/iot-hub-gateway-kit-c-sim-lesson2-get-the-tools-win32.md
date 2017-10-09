---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia hello i hello oprogramowania na komputerze hosta z systemem Windows, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
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
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="365a5-104">Pobierz narzędzia hello (z systemem Windows 7 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="365a5-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="365a5-105">Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="365a5-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="365a5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="365a5-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="365a5-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="365a5-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="365a5-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="365a5-108">What you will do</span></span>

- <span data-ttu-id="365a5-109">Zainstaluj narzędzia Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="365a5-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="365a5-110">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="365a5-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="365a5-111">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="365a5-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="365a5-112">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="365a5-112">What you will learn</span></span>

<span data-ttu-id="365a5-113">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="365a5-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="365a5-114">Jak tooinstall [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="365a5-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="365a5-115">Git jest typu open source rozproszonego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="365a5-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="365a5-116">Witaj Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.</span><span class="sxs-lookup"><span data-stu-id="365a5-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="365a5-117">Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="365a5-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="365a5-118">Jak toouse [NPM](https://www.npmjs.com/) tooinstall narzędzi do tworzenia środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="365a5-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="365a5-119">Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="365a5-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="365a5-120">NPM jest jednym z hello menedżerów pakietu dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="365a5-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="365a5-121">Jak tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="365a5-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="365a5-122">Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="365a5-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="365a5-123">Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.</span><span class="sxs-lookup"><span data-stu-id="365a5-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="365a5-124">Jak tooinstall języka Python.</span><span class="sxs-lookup"><span data-stu-id="365a5-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="365a5-125">Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="365a5-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="365a5-126">Jak tooinstall hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="365a5-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="365a5-127">Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="365a5-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="365a5-128">Praca bezpośrednio z tooprovision wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="365a5-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="365a5-129">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="365a5-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="365a5-130">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="365a5-130">What you need</span></span>

- <span data-ttu-id="365a5-131">Toodownload połączenia internetowego hello i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="365a5-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="365a5-132">Komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="365a5-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="365a5-133">Zainstaluj usługi Git i Node.js</span><span class="sxs-lookup"><span data-stu-id="365a5-133">Install Git and Node.js</span></span>

<span data-ttu-id="365a5-134">Kliknij następujące łącza toodownload hello i zainstaluj usługi Git i LTS Node.js dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="365a5-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="365a5-135">Pobierz Git dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="365a5-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="365a5-136">Pobierz Node.js LTS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="365a5-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="365a5-137">Instalowania narzędzi do tworzenia środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="365a5-137">Install Node.js development tools</span></span>

<span data-ttu-id="365a5-138">Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="365a5-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="365a5-139">Naciśnij klawisz `Windows + R`, typ `cmd` i naciśnij klawisz `Enter` tooopen okno wiersza polecenia, a następnie hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="365a5-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="365a5-140">Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="365a5-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="365a5-141">Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="365a5-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="365a5-142">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="365a5-142">Install Python</span></span>

<span data-ttu-id="365a5-143">Można wybrać z Python 2.7 3.4 lub 3.5.</span><span class="sxs-lookup"><span data-stu-id="365a5-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="365a5-144">W tym samouczku używamy Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="365a5-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="365a5-145">Jeśli po zainstalowaniu języka python, przejdź toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="365a5-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="365a5-146">Pobierz języka Python dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="365a5-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="365a5-147">Należy również tooadd hello ścieżki folderów hello skutkującej systemu zainstalowanych toohello Python.exe i pip.exe `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="365a5-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="365a5-148">Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="365a5-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="365a5-149">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="365a5-149">Install hello Azure CLI</span></span>

<span data-ttu-id="365a5-150">Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="365a5-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="365a5-151">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="365a5-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="365a5-152">Zainstaluj hello Azure CLI, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="365a5-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="365a5-153">Witaj, instalacja może zająć 5 minut.</span><span class="sxs-lookup"><span data-stu-id="365a5-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="365a5-154">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="365a5-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="365a5-155">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="365a5-155">You should see hello following output if hello installation is successful.</span></span>

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="365a5-157">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="365a5-157">Install Visual Studio Code</span></span>

<span data-ttu-id="365a5-158">W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.</span><span class="sxs-lookup"><span data-stu-id="365a5-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="365a5-159">[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="365a5-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="365a5-160">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="365a5-160">Summary</span></span>

<span data-ttu-id="365a5-161">Po zainstalowaniu wszystkich wymaganych hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="365a5-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="365a5-162">Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="365a5-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="365a5-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="365a5-163">Next steps</span></span>
<span data-ttu-id="365a5-164">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="365a5-164">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>
