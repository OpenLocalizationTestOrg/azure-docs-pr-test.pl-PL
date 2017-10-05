---
title: "Connect Intel Edison (C) do Azure IoT — Lekcja 2: narzędzi platformy Azure (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 897ab63af85a1f830ed49084ce7c3e74c84a4cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="67b18-104">Pobierz narzędzia Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="67b18-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="67b18-105">[System Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="67b18-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="67b18-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="67b18-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="67b18-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="67b18-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="67b18-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="67b18-108">What you will do</span></span>
<span data-ttu-id="67b18-109">Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="67b18-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="67b18-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="67b18-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="67b18-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="67b18-111">What you will learn</span></span>
<span data-ttu-id="67b18-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="67b18-112">In this article, you will learn:</span></span>
* <span data-ttu-id="67b18-113">Jak zainstalować wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="67b18-114">Jak dodać podgrupę IoT wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="67b18-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="67b18-115">What you need</span></span>
* <span data-ttu-id="67b18-116">Ubuntu komputera z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="67b18-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="67b18-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-117">An active Azure subscription.</span></span> <span data-ttu-id="67b18-118">Jeśli nie masz konta, możesz utworzyć [bezpłatnego konta wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="67b18-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="67b18-119">Zainstaluj interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67b18-119">Install the Azure CLI</span></span>
<span data-ttu-id="67b18-120">Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure, dzięki któremu można pracować bezpośrednio w wierszu polecenia do udostępniania zasobów i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="67b18-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="67b18-121">Aby zainstalować najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="67b18-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="67b18-122">Uruchom następujące polecenia w oknie terminalu.</span><span class="sxs-lookup"><span data-stu-id="67b18-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="67b18-123">Może upłynąć pięć minut na zainstalowanie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="67b18-124">Instalację można zweryfikować, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="67b18-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="67b18-125">Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="67b18-125">You should see the following output if the installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="67b18-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="67b18-127">Summary</span></span>
<span data-ttu-id="67b18-128">Po zainstalowaniu interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="67b18-129">Następnym zadaniem będzie można utworzyć tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b18-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67b18-130">Next steps</span></span>
<span data-ttu-id="67b18-131">[Utworzenie Centrum IoT i zarejestruj Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="67b18-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
