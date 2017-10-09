---
title: Host Docker z VirtualBox aaaConfigure | Dokumentacja firmy Microsoft
description: "Wystąpienie domyślne Docker przy użyciu rozwiązania Docker maszyny i VirtualBox tooconfigure instrukcje krok po kroku"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="52162-103">Konfigurowanie hosta Docker z VirtualBox</span><span class="sxs-lookup"><span data-stu-id="52162-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="52162-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="52162-104">Overview</span></span>
<span data-ttu-id="52162-105">W tym artykule przedstawiono Konfigurowanie domyślnego wystąpienia Docker przy użyciu rozwiązania Docker maszyny i VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="52162-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="52162-106">Jeśli używasz hello [Docker dla systemu Windows w wersji beta](http://beta.docker.com/), ta konfiguracja nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="52162-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52162-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52162-107">Prerequisites</span></span>
<span data-ttu-id="52162-108">Witaj następujących narzędzi muszą toobe zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52162-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="52162-109">Przybornik docker</span><span class="sxs-lookup"><span data-stu-id="52162-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="52162-110">Konfigurowanie klienta platformy Docker hello przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="52162-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="52162-111">po prostu tooconfigure Docker klienta, Otwórz program Windows PowerShell i wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="52162-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="52162-112">Utwórz wystąpienie domyślne hostów docker.</span><span class="sxs-lookup"><span data-stu-id="52162-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="52162-113">Sprawdź, czy wystąpienie domyślne hello jest skonfigurowana i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="52162-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="52162-114">(Powinna zostać wyświetlona wystąpienia o nazwie "default" systemem.</span><span class="sxs-lookup"><span data-stu-id="52162-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![dane wyjściowe ls maszyny docker][0]
3. <span data-ttu-id="52162-116">Domyślne jako hello bieżącego hosta i konfigurowanie powłoki.</span><span class="sxs-lookup"><span data-stu-id="52162-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="52162-117">Wyświetlanie hello kontenery usługi active Docker.</span><span class="sxs-lookup"><span data-stu-id="52162-117">Display hello active Docker containers.</span></span> <span data-ttu-id="52162-118">Lista Hello powinna być pusta.</span><span class="sxs-lookup"><span data-stu-id="52162-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![dane wyjściowe ps docker][1]

> [!NOTE]
> <span data-ttu-id="52162-120">Każdym uruchomieniu komputerze deweloperskim, należy toorestart hosta lokalnego docker.</span><span class="sxs-lookup"><span data-stu-id="52162-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="52162-121">toodo hello tego problemu, następujące polecenie w wierszu polecenia: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="52162-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
