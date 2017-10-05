---
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 2: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="5ba6a-104">Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="5ba6a-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ba6a-105">System Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="5ba6a-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="5ba6a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="5ba6a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="5ba6a-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="5ba6a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="5ba6a-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5ba6a-108">What you will do</span></span>
<span data-ttu-id="5ba6a-109">Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="5ba6a-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5ba6a-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5ba6a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5ba6a-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5ba6a-111">What you will learn</span></span>
<span data-ttu-id="5ba6a-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5ba6a-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5ba6a-113">Jak zainstalować Python.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-113">How to install Python.</span></span>
* <span data-ttu-id="5ba6a-114">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5ba6a-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5ba6a-115">What you need</span></span>
* <span data-ttu-id="5ba6a-116">Komputer z systemem Windows z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="5ba6a-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-117">An active Azure subscription.</span></span> <span data-ttu-id="5ba6a-118">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="5ba6a-119">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="5ba6a-119">Install Python</span></span>
<span data-ttu-id="5ba6a-120">[Instalowanie języka Python](https://www.python.org/downloads/) na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="5ba6a-121">Można zainstalować środowisko Python 2.7 3.4 lub 3.5.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="5ba6a-122">W tym samouczku jest oparty na języku Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="5ba6a-123">Jeśli po zainstalowaniu języka Python, przejdź do następnej sekcji i zainstaluj interfejs wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="5ba6a-124">Należy również dodać ścieżkę do folderów, w którym python.exe i pip.exe są zainstalowane w systemie `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="5ba6a-125">Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="5ba6a-126">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5ba6a-126">Install the Azure CLI</span></span>
<span data-ttu-id="5ba6a-127">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5ba6a-128">Możesz pracować bezpośrednio z z wiersza polecenia do obsługi administracyjnej zasobów i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-128">You work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="5ba6a-129">Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ba6a-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5ba6a-130">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5ba6a-131">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba6a-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="5ba6a-132">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5ba6a-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5ba6a-133">Następujące dane wyjściowe zostanie wyświetlony, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-133">You see the following output if the installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="5ba6a-135">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5ba6a-135">Summary</span></span>
<span data-ttu-id="5ba6a-136">Po zainstalowaniu interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="5ba6a-137">Następnym zadaniem do tworzenia tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba6a-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ba6a-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ba6a-138">Next steps</span></span>
[<span data-ttu-id="5ba6a-139">Utworzenie Centrum IoT i zarejestruj malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="5ba6a-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

