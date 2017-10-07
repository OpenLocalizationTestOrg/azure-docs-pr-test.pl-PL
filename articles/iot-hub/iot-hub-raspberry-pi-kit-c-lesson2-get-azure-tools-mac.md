---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 2: narzędzi platformy Azure (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="0b24a-104">Pobierz narzędzia Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="0b24a-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b24a-105">System Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="0b24a-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="0b24a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="0b24a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="0b24a-107">System macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="0b24a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="0b24a-108">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="0b24a-108">What you will do</span></span>
<span data-ttu-id="0b24a-109">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="0b24a-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="0b24a-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0b24a-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0b24a-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="0b24a-111">What you will learn</span></span>
<span data-ttu-id="0b24a-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="0b24a-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0b24a-113">Jak tooinstall wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="0b24a-114">Jak tooadd podgrupę IoT hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0b24a-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="0b24a-115">What you need</span></span>
* <span data-ttu-id="0b24a-116">Mac z połączeniem internetowym.</span><span class="sxs-lookup"><span data-stu-id="0b24a-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="0b24a-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-117">An active Azure subscription.</span></span> <span data-ttu-id="0b24a-118">Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0b24a-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="0b24a-119">Instalowanie języka Python</span><span class="sxs-lookup"><span data-stu-id="0b24a-119">Install Python</span></span>
<span data-ttu-id="0b24a-120">Mimo że macOS zawiera Python 2.7 fabrycznej hello, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew.</span><span class="sxs-lookup"><span data-stu-id="0b24a-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="0b24a-121">Zobacz [instalowanie Python na macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="0b24a-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="0b24a-122">Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0b24a-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="0b24a-123">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0b24a-123">Install hello Azure CLI</span></span>
<span data-ttu-id="0b24a-124">Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0b24a-125">Praca bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="0b24a-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="0b24a-126">tooinstall hello najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0b24a-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0b24a-127">Uruchom następujące polecenia w oknie terminalu hello.</span><span class="sxs-lookup"><span data-stu-id="0b24a-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="0b24a-128">Może upłynąć hello tooinstall pięć minut wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="0b24a-129">Sprawdź hello instalacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0b24a-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="0b24a-130">Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="0b24a-130">You should see hello following output if hello installation is successful.</span></span>

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="0b24a-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0b24a-132">Summary</span></span>
<span data-ttu-id="0b24a-133">Po zainstalowaniu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="0b24a-134">Następnym zadaniem jest toocreate tożsamości Azure IoT hub i urządzeń za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b24a-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b24a-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b24a-135">Next steps</span></span>
[<span data-ttu-id="0b24a-136">Utworzenie Centrum IoT i zarejestruj malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="0b24a-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

