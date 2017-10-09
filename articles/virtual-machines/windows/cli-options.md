---
title: Witaj aaaUsing wiersza polecenia platformy Azure w systemie Windows | Dokumentacja firmy Microsoft
description: "Przy użyciu interfejsu wiersza polecenia Azure hello w systemie Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="8de65-103">Przy użyciu interfejsu wiersza polecenia Azure hello w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="8de65-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="8de65-104">Hello Azure interfejsu wiersza polecenia (CLI) oferuje wiersza polecenia i skryptów środowiska do tworzenia i zarządzania zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8de65-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="8de65-105">Hello wiersza polecenia platformy Azure jest dostępna dla macOS, Linux i systemów operacyjnych Windows.</span><span class="sxs-lookup"><span data-stu-id="8de65-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="8de65-106">W tych systemach operacyjnych hello polecenia interfejsu wiersza polecenia są identyczne, jednak może się różnić składni skryptów systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="8de65-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="8de65-107">Tej metody hello szczegóły dokumentu hello wiersza polecenia platformy Azure można zainstalować i uruchomić na zagadnienia syntaktycznych systemu Windows i szczegóły dla każdego.</span><span class="sxs-lookup"><span data-stu-id="8de65-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="8de65-108">Aby uzyskać szczegółowe interfejsu wiersza polecenia Azure dokumentacji, zobacz [dokumentacji interfejsu wiersza polecenia Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8de65-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="8de65-109">Podsystem systemu Windows dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="8de65-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="8de65-110">Witaj podsystemu systemu Windows dla systemu Linux (WSL) udostępnia środowisko Ubuntu Linux na system Windows 10 Anniversary i późniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="8de65-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="8de65-111">Po włączeniu WSL zapewnia natywnym środowiskiem Bash, która może służyć do tworzenia i uruchamiania skryptów wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8de65-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="8de65-112">Ponieważ WSL zapewnia natywnym środowiskiem Bash, skryptów wiersza polecenia platformy Azure może być współużytkowana macOS, Linux i Windows bez żadnych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="8de65-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="8de65-113">Witaj toouse wiersza polecenia platformy Azure w WSL, wykonaj następujące czynności hello.</span><span class="sxs-lookup"><span data-stu-id="8de65-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="8de65-114">Zadanie</span><span class="sxs-lookup"><span data-stu-id="8de65-114">Task</span></span> | <span data-ttu-id="8de65-115">Instrukcje</span><span class="sxs-lookup"><span data-stu-id="8de65-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="8de65-116">Włącz WSL</span><span class="sxs-lookup"><span data-stu-id="8de65-116">Enable WSL</span></span> | [<span data-ttu-id="8de65-117">Zainstaluj WSL dokumentacji</span><span class="sxs-lookup"><span data-stu-id="8de65-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="8de65-118">Zainstaluj hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8de65-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="8de65-119">Zainstaluj na WSL/Ubuntu 14.04 hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8de65-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="8de65-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8de65-120">PowerShell</span></span>

<span data-ttu-id="8de65-121">Witaj wiersza polecenia platformy Azure może działać natywnie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="8de65-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="8de65-122">W tej konfiguracji hello Azure CLI pakiet jest zainstalowany w systemie operacyjnym Windows hello, a polecenia można uruchomić z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8de65-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="8de65-123">W tej konfiguracji interfejsu wiersza polecenia Azure poleceń i skryptów może działać w dowolnej obsługiwanej wersji systemu Windows, jednak platforma składni skryptów jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="8de65-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="8de65-124">W związku z tym skrypty nie zawsze mogą współużytkować system macOS, Linux i Windows bez żadnych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="8de65-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="8de65-125">Witaj toouse wiersza polecenia platformy Azure w systemie Windows, zainstaluj pakiet hello za pomocą tych instrukcji [hello instalowanie interfejsu wiersza polecenia w systemie Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="8de65-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="8de65-126">Obraz docker</span><span class="sxs-lookup"><span data-stu-id="8de65-126">Docker Image</span></span>

<span data-ttu-id="8de65-127">Korzystając z Docker dla systemu Windows, obrazu Docker można uruchomić zawierającą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8de65-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="8de65-128">Ten obraz jest oparte na systemie Linux i zawiera natywnym środowiskiem Bash.</span><span class="sxs-lookup"><span data-stu-id="8de65-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="8de65-129">Korzystając z Docker dla systemu Windows i hello Azure CLI obrazu, toobe skrypty współużytkowane przez system macOS, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="8de65-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="8de65-130">toouse hello Azure CLI na Docker dla systemu Windows, upewnij się, że Docker dla systemu Windows działa i uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="8de65-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="8de65-131">Po ukończeniu Bash, czyli rozpoczęcia sesji wstępnie ładowane hello narzędzia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8de65-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8de65-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8de65-132">Next Steps</span></span>

[<span data-ttu-id="8de65-133">Przykładowy interfejs wiersza polecenia dla maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8de65-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="8de65-134">Przykłady interfejsu wiersza polecenia dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="8de65-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="8de65-135">Przykłady interfejsu wiersza polecenia dla bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8de65-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
