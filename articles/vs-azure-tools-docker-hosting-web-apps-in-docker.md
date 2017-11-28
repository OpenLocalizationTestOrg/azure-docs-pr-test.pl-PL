---
title: aaaDeploy platformy ASP.NET Core Linux Docker kontenera tooa Docker hosta zdalnego | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Visual Studio Tools for Docker toodeploy platformy ASP.NET Core sieci web kontenera Docker tooa aplikacji uruchomionych na maszynie Wirtualnej platformy Azure Docker hosta systemu Linux"
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
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="5a197-103">Wdrażanie programu ASP.NET kontenera tooa Docker hosta zdalnego</span><span class="sxs-lookup"><span data-stu-id="5a197-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="5a197-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5a197-104">Overview</span></span>
<span data-ttu-id="5a197-105">Docker jest aparatem lekkie kontenera, podobne niektóre sposoby tooa maszyny wirtualnej, które można użyć toohost aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="5a197-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="5a197-106">Ten samouczek przedstawia przy użyciu hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy rozszerzenia hosta platformy ASP.NET Core aplikacji tooa Docker na platformie Azure przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a197-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a197-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5a197-107">Prerequisites</span></span>
<span data-ttu-id="5a197-108">następujące Hello jest wymagana toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="5a197-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="5a197-109">Tworzenie maszyny Wirtualnej platformy Azure Docker hosta, zgodnie z opisem w [jak toouse docker maszyny z platformy Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5a197-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="5a197-110">Zainstaluj najnowszą wersję hello z [programu Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5a197-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="5a197-111">Pobierz hello [zestawu SDK programu Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="5a197-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="5a197-112">Zainstaluj [Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="5a197-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="5a197-113">1. Tworzenie aplikacji sieci web platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5a197-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="5a197-114">Hello następujące kroki pomocne przy tworzeniu Podstawowa aplikacja platformy ASP.NET Core, który będzie używany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5a197-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="5a197-115">2. Dodawanie obsługi Docker</span><span class="sxs-lookup"><span data-stu-id="5a197-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="5a197-116">3. Użyj hello DockerTask.ps1 skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a197-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="5a197-117">Otwórz katalog główny toohello monitu środowiska PowerShell projektu.</span><span class="sxs-lookup"><span data-stu-id="5a197-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="5a197-118">Sprawdź poprawność hello zdalnym hoście jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="5a197-118">Validate hello remote host is running.</span></span> <span data-ttu-id="5a197-119">Powinien zostać wyświetlony stan = uruchomiona</span><span class="sxs-lookup"><span data-stu-id="5a197-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="5a197-120">Przy użyciu aplikacji hello kompilacji hello - parametru kompilacji</span><span class="sxs-lookup"><span data-stu-id="5a197-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="5a197-121">Uruchamianie aplikacji hello przy użyciu hello — Uruchom parametr</span><span class="sxs-lookup"><span data-stu-id="5a197-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="5a197-122">Po zakończeniu docker powinny być widoczne wyniki podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="5a197-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Wyświetlanie aplikacji][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
