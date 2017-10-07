---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 2: narzędzi platformy Azure (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="29365-104">Pobierz narzędzia Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="29365-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29365-105">System Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="29365-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="29365-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="29365-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="29365-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="29365-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="29365-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="29365-108">What you will do</span></span>
<span data-ttu-id="29365-109">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="29365-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="29365-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="29365-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="29365-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="29365-111">What you will learn</span></span>
<span data-ttu-id="29365-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="29365-112">In this article, you will learn:</span></span>
* <span data-ttu-id="29365-113">Jak tooinstall hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="29365-114">Jak tooadd podgrupę IoT hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="29365-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="29365-115">What you need</span></span>
* <span data-ttu-id="29365-116">Ubuntu komputera z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="29365-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="29365-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-117">An active Azure subscription.</span></span> <span data-ttu-id="29365-118">Jeśli nie masz konta, możesz utworzyć [bezpłatnego konta wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="29365-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="29365-119">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="29365-119">Install hello Azure CLI</span></span>
<span data-ttu-id="29365-120">Hello interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure, umożliwiając toowork bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="29365-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="29365-121">tooinstall hello najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="29365-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="29365-122">Uruchom następujące polecenia w oknie terminalu hello.</span><span class="sxs-lookup"><span data-stu-id="29365-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="29365-123">Może upłynąć hello tooinstall pięć minut wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="29365-124">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29365-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="29365-125">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="29365-125">You should see hello following output if hello installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="29365-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="29365-127">Summary</span></span>
<span data-ttu-id="29365-128">Po zainstalowaniu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="29365-129">Następnym zadaniem jest toocreate Centrum Azure IoT i urządzeniami przy użyciu tożsamości hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29365-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29365-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29365-130">Next steps</span></span>
[<span data-ttu-id="29365-131">Utworzenie Centrum IoT i zarejestruj malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="29365-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

