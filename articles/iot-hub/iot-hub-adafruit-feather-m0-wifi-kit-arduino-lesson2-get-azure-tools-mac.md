---
title: "Nawiązać Arduino Azure IoT — Lekcja 2: narzędzi platformy Azure (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 037f8e3dba542773185fde43a345d5fd487b2d84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="6fec6-104">Pobierz narzędzia Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="6fec6-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="6fec6-105">[Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="6fec6-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="6fec6-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="6fec6-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="6fec6-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="6fec6-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6fec6-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="6fec6-108">What you will do</span></span>

<span data-ttu-id="6fec6-109">Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="6fec6-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="6fec6-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="6fec6-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6fec6-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="6fec6-111">What you will learn</span></span>
<span data-ttu-id="6fec6-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="6fec6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="6fec6-113">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="6fec6-114">Jak dodać podgrupę IoT wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6fec6-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="6fec6-115">What you need</span></span>
* <span data-ttu-id="6fec6-116">Mac z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="6fec6-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="6fec6-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-117">An active Azure subscription.</span></span> <span data-ttu-id="6fec6-118">Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6fec6-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="6fec6-119">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="6fec6-119">Install Python</span></span>
<span data-ttu-id="6fec6-120">Mimo że macOS zawiera Python 2.7 fabrycznej, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="6fec6-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="6fec6-121">Zobacz [instalowanie Python na macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="6fec6-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="6fec6-122">Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6fec6-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="6fec6-123">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6fec6-123">Install the Azure CLI</span></span>
<span data-ttu-id="6fec6-124">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6fec6-125">Praca bezpośrednio w wierszu polecenia do udostępniania i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="6fec6-125">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="6fec6-126">Aby zainstalować najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6fec6-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6fec6-127">Uruchom następujące polecenia w oknie terminalu.</span><span class="sxs-lookup"><span data-stu-id="6fec6-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="6fec6-128">Może upłynąć pięć minut na zainstalowanie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="6fec6-129">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6fec6-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="6fec6-130">Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6fec6-130">You should see the following output if the installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie][output]

## <a name="summary"></a><span data-ttu-id="6fec6-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6fec6-132">Summary</span></span>
<span data-ttu-id="6fec6-133">Po zainstalowaniu interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="6fec6-134">Następnym zadaniem będzie można utworzyć tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fec6-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fec6-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6fec6-135">Next steps</span></span>
<span data-ttu-id="6fec6-136">[Utworzenie Centrum IoT i zarejestruj tablicy Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="6fec6-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md