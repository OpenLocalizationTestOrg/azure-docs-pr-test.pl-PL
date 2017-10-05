---
title: "Wdrażanie kontenera platformy ASP.NET Core Linux Docker z hostem zdalnym Docker | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użyć programu Visual Studio Tools for Docker do wdrażania aplikacji sieci web platformy ASP.NET Core w kontenerze Docker działającym na maszynie Wirtualnej platformy Azure Docker hosta systemu Linux"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="a917e-103">Wdrażanie kontenera ASP.NET z hostem zdalnym Docker</span><span class="sxs-lookup"><span data-stu-id="a917e-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="a917e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a917e-104">Overview</span></span>
<span data-ttu-id="a917e-105">Docker jest aparatem lekkie kontenera, podobne w pewnym sensie do maszyny wirtualnej, która służy do obsługi aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="a917e-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="a917e-106">Ten samouczek przedstawia przy użyciu [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) rozszerzenia do wdrażania aplikacji platformy ASP.NET Core z hostem platformy Docker na platformie Azure przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a917e-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a917e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a917e-107">Prerequisites</span></span>
<span data-ttu-id="a917e-108">Do ukończenia tego samouczka niezbędne jest, następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a917e-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="a917e-109">Tworzenie maszyny Wirtualnej platformy Azure Docker hosta, zgodnie z opisem w [sposób używania maszyny docker z platformy Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a917e-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="a917e-110">Zainstaluj najnowszą wersję pakietu [programu Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="a917e-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="a917e-111">Pobierz [zestawu SDK programu Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="a917e-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="a917e-112">Zainstaluj [Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="a917e-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="a917e-113">1. Tworzenie aplikacji sieci web platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a917e-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="a917e-114">Poniższe kroki pomocne przy tworzeniu Podstawowa aplikacja platformy ASP.NET Core, który będzie używany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="a917e-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="a917e-115">2. Dodawanie obsługi Docker</span><span class="sxs-lookup"><span data-stu-id="a917e-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="a917e-116">3. Użyj skryptu programu PowerShell DockerTask.ps1</span><span class="sxs-lookup"><span data-stu-id="a917e-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="a917e-117">Otwórz wiersz programu PowerShell do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="a917e-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="a917e-118">Sprawdź poprawność zdalnego hosta jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="a917e-118">Validate the remote host is running.</span></span> <span data-ttu-id="a917e-119">Powinien zostać wyświetlony stan = uruchomiona</span><span class="sxs-lookup"><span data-stu-id="a917e-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="a917e-120">Tworzenie aplikacji w programie parametru - kompilacji</span><span class="sxs-lookup"><span data-stu-id="a917e-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="a917e-121">Uruchamianie aplikacji, za pomocą parametru - uruchomienia</span><span class="sxs-lookup"><span data-stu-id="a917e-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="a917e-122">Po zakończeniu docker powinny być widoczne wyniki podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a917e-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![Wyświetlanie aplikacji][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
