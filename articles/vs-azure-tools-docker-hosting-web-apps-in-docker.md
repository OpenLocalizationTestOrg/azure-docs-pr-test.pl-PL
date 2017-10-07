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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Wdrażanie programu ASP.NET kontenera tooa Docker hosta zdalnego
## <a name="overview"></a>Omówienie
Docker jest aparatem lekkie kontenera, podobne niektóre sposoby tooa maszyny wirtualnej, które można użyć toohost aplikacji i usług.
Ten samouczek przedstawia przy użyciu hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy rozszerzenia hosta platformy ASP.NET Core aplikacji tooa Docker na platformie Azure przy użyciu programu PowerShell.

## <a name="prerequisites"></a>Wymagania wstępne
następujące Hello jest wymagana toocomplete tego samouczka:

* Tworzenie maszyny Wirtualnej platformy Azure Docker hosta, zgodnie z opisem w [jak toouse docker maszyny z platformy Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zainstaluj najnowszą wersję hello z [programu Visual Studio](https://www.visualstudio.com/downloads/)
* Pobierz hello [zestawu SDK programu Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)
* Zainstaluj [Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Tworzenie aplikacji sieci web platformy ASP.NET Core
Hello następujące kroki pomocne przy tworzeniu Podstawowa aplikacja platformy ASP.NET Core, który będzie używany w tym samouczku.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Dodawanie obsługi Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Użyj hello DockerTask.ps1 skrypt programu PowerShell
1. Otwórz katalog główny toohello monitu środowiska PowerShell projektu. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Sprawdź poprawność hello zdalnym hoście jest uruchomiony. Powinien zostać wyświetlony stan = uruchomiona 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Przy użyciu aplikacji hello kompilacji hello - parametru kompilacji
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Uruchamianie aplikacji hello przy użyciu hello — Uruchom parametr
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Po zakończeniu docker powinny być widoczne wyniki podobne toohello poniżej:
   
   ![Wyświetlanie aplikacji][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
