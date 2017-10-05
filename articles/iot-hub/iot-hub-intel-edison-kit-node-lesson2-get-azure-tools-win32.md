---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — Lekcja 2: narzędzi platformy Azure (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7257fe98fa1075456de620ca46b4e10c34e06574
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="60d7e-104">Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="60d7e-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="60d7e-105">[System Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="60d7e-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="60d7e-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="60d7e-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="60d7e-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="60d7e-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="60d7e-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="60d7e-108">What you will do</span></span>
<span data-ttu-id="60d7e-109">Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="60d7e-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="60d7e-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="60d7e-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="60d7e-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="60d7e-111">What you will learn</span></span>
<span data-ttu-id="60d7e-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="60d7e-112">In this article, you will learn:</span></span>
* <span data-ttu-id="60d7e-113">Jak zainstalować Python.</span><span class="sxs-lookup"><span data-stu-id="60d7e-113">How to install Python.</span></span>
* <span data-ttu-id="60d7e-114">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="60d7e-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="60d7e-115">What you need</span></span>
* <span data-ttu-id="60d7e-116">Komputer z systemem Windows z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="60d7e-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="60d7e-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-117">An active Azure subscription.</span></span> <span data-ttu-id="60d7e-118">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="60d7e-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="60d7e-119">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="60d7e-119">Install Python</span></span>
<span data-ttu-id="60d7e-120">[Instalowanie języka Python](https://www.python.org/downloads/) na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="60d7e-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="60d7e-121">Można zainstalować środowisko Python 2.7 3.4 lub 3.5.</span><span class="sxs-lookup"><span data-stu-id="60d7e-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="60d7e-122">W tym samouczku jest oparty na języku Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="60d7e-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="60d7e-123">Jeśli po zainstalowaniu języka Python, przejdź do następnej sekcji i zainstaluj interfejs wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="60d7e-124">Należy również dodać ścieżkę do folderów, w którym python.exe i pip.exe są zainstalowane w systemie `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="60d7e-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="60d7e-125">Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="60d7e-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="60d7e-126">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="60d7e-126">Install the Azure CLI</span></span>
<span data-ttu-id="60d7e-127">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="60d7e-128">Praca bezpośrednio w wierszu polecenia do udostępniania i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="60d7e-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="60d7e-129">Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="60d7e-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="60d7e-130">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="60d7e-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="60d7e-131">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="60d7e-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="60d7e-132">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="60d7e-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="60d7e-133">Następujące dane wyjściowe zostanie wyświetlony, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="60d7e-133">You see the following output if the installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="60d7e-135">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="60d7e-135">Summary</span></span>
<span data-ttu-id="60d7e-136">Po zainstalowaniu interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="60d7e-137">Następnym zadaniem do tworzenia tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60d7e-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60d7e-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60d7e-138">Next steps</span></span>
<span data-ttu-id="60d7e-139">[Utworzenie Centrum IoT i zarejestruj Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="60d7e-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
