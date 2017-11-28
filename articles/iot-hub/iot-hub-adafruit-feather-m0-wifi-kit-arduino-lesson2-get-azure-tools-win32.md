---
title: "Połącz Arduino tooAzure IoT — Lekcja 2: narzędzi platformy Azure (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i hello interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9b891224ff3974d9ce5382eb983470d5d41bcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="ee04f-104">Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="ee04f-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="ee04f-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="ee04f-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="ee04f-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ee04f-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ee04f-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ee04f-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ee04f-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="ee04f-108">What you will do</span></span>

<span data-ttu-id="ee04f-109">Zainstaluj Python i hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="ee04f-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="ee04f-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="ee04f-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ee04f-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="ee04f-111">What you will learn</span></span>
<span data-ttu-id="ee04f-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="ee04f-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ee04f-113">Jak tooinstall języka Python.</span><span class="sxs-lookup"><span data-stu-id="ee04f-113">How tooinstall Python.</span></span>
* <span data-ttu-id="ee04f-114">Jak tooinstall hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ee04f-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="ee04f-115">What you need</span></span>
* <span data-ttu-id="ee04f-116">Komputer z systemem Windows z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="ee04f-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="ee04f-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-117">An active Azure subscription.</span></span> <span data-ttu-id="ee04f-118">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ee04f-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="ee04f-119">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="ee04f-119">Install Python</span></span>
<span data-ttu-id="ee04f-120">[Instalowanie języka Python](https://www.python.org/downloads/) na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="ee04f-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="ee04f-121">Można zainstalować środowisko Python 2.7 3.4 lub 3.5.</span><span class="sxs-lookup"><span data-stu-id="ee04f-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="ee04f-122">W tym samouczku jest oparty na języku Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="ee04f-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="ee04f-123">Po zainstalowaniu języka Python, przejdź do następnej sekcji toohello i zainstalować hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="ee04f-124">Należy również tooadd hello ścieżki folderów hello skutkującej systemu zainstalowanych toohello python.exe i pip.exe `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="ee04f-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="ee04f-125">Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="ee04f-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="ee04f-126">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ee04f-126">Install hello Azure CLI</span></span>
<span data-ttu-id="ee04f-127">Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="ee04f-128">Praca bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="ee04f-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="ee04f-129">Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ee04f-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ee04f-130">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="ee04f-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="ee04f-131">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ee04f-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="ee04f-132">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ee04f-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="ee04f-133">Zobaczysz, że hello następujących danych wyjściowych, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="ee04f-133">You see hello following output if hello installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie][output]

## <a name="summary"></a><span data-ttu-id="ee04f-135">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ee04f-135">Summary</span></span>
<span data-ttu-id="ee04f-136">Po zainstalowaniu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="ee04f-137">Następnego zadań toocreate tożsamości koncentratora i urządzenia Azure IoT przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04f-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee04f-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee04f-138">Next steps</span></span>
<span data-ttu-id="ee04f-139">[Utworzenie Centrum IoT i zarejestruj tablicy Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="ee04f-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md