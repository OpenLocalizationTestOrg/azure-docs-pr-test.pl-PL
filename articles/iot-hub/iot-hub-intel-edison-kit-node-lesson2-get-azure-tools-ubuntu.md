---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 2: narzędzi platformy Azure (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca2996b779a4d3cde833c5f2824d19ec46241bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="565f9-104">Pobierz narzędzia Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="565f9-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="565f9-105">[System Windows 7 lub nowszy][windows]</span><span class="sxs-lookup"><span data-stu-id="565f9-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="565f9-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="565f9-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="565f9-107">[System macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="565f9-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="565f9-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="565f9-108">What you will do</span></span>
<span data-ttu-id="565f9-109">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="565f9-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="565f9-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="565f9-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="565f9-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="565f9-111">What you will learn</span></span>
<span data-ttu-id="565f9-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="565f9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="565f9-113">Jak tooinstall hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="565f9-114">Jak tooadd podgrupę IoT hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="565f9-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="565f9-115">What you need</span></span>
* <span data-ttu-id="565f9-116">Ubuntu komputera z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="565f9-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="565f9-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-117">An active Azure subscription.</span></span> <span data-ttu-id="565f9-118">Jeśli nie masz konta, możesz utworzyć [bezpłatnego konta wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="565f9-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="565f9-119">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="565f9-119">Install hello Azure CLI</span></span>
<span data-ttu-id="565f9-120">Hello interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure, umożliwiając toowork bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="565f9-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="565f9-121">tooinstall hello najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="565f9-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="565f9-122">Uruchom następujące polecenia w oknie terminalu hello.</span><span class="sxs-lookup"><span data-stu-id="565f9-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="565f9-123">Może upłynąć hello tooinstall pięć minut wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="565f9-124">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="565f9-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="565f9-125">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="565f9-125">You should see hello following output if hello installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="565f9-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="565f9-127">Summary</span></span>
<span data-ttu-id="565f9-128">Po zainstalowaniu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="565f9-129">Następnym zadaniem jest toocreate Centrum Azure IoT i urządzeniami przy użyciu tożsamości hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="565f9-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="565f9-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="565f9-130">Next steps</span></span>
<span data-ttu-id="565f9-131">[Utworzenie Centrum IoT i zarejestruj Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="565f9-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
