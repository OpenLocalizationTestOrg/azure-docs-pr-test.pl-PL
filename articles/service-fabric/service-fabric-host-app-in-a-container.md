---
title: "aaaDeploy aplikacji .NET w kontenerze tooAzure sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Przedstawienie sposobu toopackage aplikacji .NET w programie Visual Studio w kontenerze Docker. Ta nowa aplikacja \"kontener\" jest następnie wdrażana tooa klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="6db4a-104">Wdrażanie aplikacji .NET w Windows tooAzure kontenera sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="6db4a-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="6db4a-105">W tym samouczku przedstawiono sposób toodeploy istniejącej aplikacji ASP.NET w kontenerze systemu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="6db4a-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="6db4a-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6db4a-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6db4a-107">Tworzenie projektu platformy Docker w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6db4a-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="6db4a-108">Containerize istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6db4a-108">Containerize an existing application</span></span>
> * <span data-ttu-id="6db4a-109">Instalator ciągłej integracji z programu Visual Studio i VSTS</span><span class="sxs-lookup"><span data-stu-id="6db4a-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6db4a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6db4a-110">Prerequisites</span></span>

1. <span data-ttu-id="6db4a-111">Zainstaluj [CE Docker dla systemu Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) , co umożliwia uruchamianie kontenerów w systemie Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6db4a-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="6db4a-112">Zapoznaj się z hello [Szybki Start systemu Windows 10 kontenery][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="6db4a-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="6db4a-113">Pobierz hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6db4a-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="6db4a-114">Zainstaluj [programu Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="6db4a-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="6db4a-115">Zainstaluj hello [rozszerzenie ciągłego dostarczania narzędzi dla programu Visual Studio 2017 r.][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="6db4a-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="6db4a-116">Utwórz [subskrypcji platformy Azure] [ link-azure-subscription] i [konto usługi Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="6db4a-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="6db4a-117">Tworzenie klastra na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6db4a-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="6db4a-118">Containerize aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6db4a-118">Containerize hello application</span></span>

<span data-ttu-id="6db4a-119">Teraz, gdy masz [klastra sieci szkieletowej usług jest uruchomiona na platformie Azure](service-fabric-tutorial-create-cluster-azure-ps.md) są gotowe toocreate i wdrażania konteneryzowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6db4a-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="6db4a-120">toostart uruchamiania aplikacji w kontenerze, potrzebujemy tooadd **Obsługa Docker** toohello projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6db4a-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="6db4a-121">Po dodaniu **Obsługa Docker** aplikacji toohello dwie czynności stanie.</span><span class="sxs-lookup"><span data-stu-id="6db4a-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="6db4a-122">Najpierw _plik Dockerfile_ dodaniu toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="6db4a-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="6db4a-123">Ten nowy plik opisano hello kontener obrazu toobe skompilowany.</span><span class="sxs-lookup"><span data-stu-id="6db4a-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="6db4a-124">Następnie po drugie, nowy _rozwiązania docker compose_ projekt zostanie dodany toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6db4a-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="6db4a-125">Witaj nowy projekt zawiera kilka rozwiązania docker compose plików.</span><span class="sxs-lookup"><span data-stu-id="6db4a-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="6db4a-126">Rozwiązania docker compose pliki mogą być używane toodescribe sposób uruchamiania hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="6db4a-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="6db4a-127">Więcej informacji na temat pracy z [programu Visual Studio Tools kontenera][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="6db4a-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="6db4a-128">Jeśli jest hello obrazów kontenera systemu Windows są uruchomione na komputerze po raz pierwszy, Docker CE musi rozwiń hello obrazy podstawowe dla kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6db4a-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="6db4a-129">obrazy Hello używane w tym samouczku są 14 GB.</span><span class="sxs-lookup"><span data-stu-id="6db4a-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="6db4a-130">Przejdź dalej i uruchom następujące obrazy podstawowe polecenia terminali toopull hello hello:</span><span class="sxs-lookup"><span data-stu-id="6db4a-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="6db4a-131">Dodawanie obsługi Docker</span><span class="sxs-lookup"><span data-stu-id="6db4a-131">Add Docker support</span></span>

<span data-ttu-id="6db4a-132">Otwórz hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] pliku w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6db4a-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="6db4a-133">Kliknij prawym przyciskiem myszy hello **FabrikamFiber.Web** projektu > **Dodaj** > **Obsługa Docker**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="6db4a-134">Dodawanie obsługi SQL</span><span class="sxs-lookup"><span data-stu-id="6db4a-134">Add support for SQL</span></span>

<span data-ttu-id="6db4a-135">Ta aplikacja używa SQL na powitania dostawcy danych, więc programu SQL server jest wymagane toorun aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6db4a-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="6db4a-136">Odwołuje się obraz kontenera programu SQL Server w naszym pliku docker compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="6db4a-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="6db4a-137">W programie Visual Studio Otwórz **Eksploratora rozwiązań**, Znajdź **rozwiązania docker compose**i otwórz hello pliku **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="6db4a-138">Przejdź toohello `services:` węzła, Dodaj węzeł o nazwie `db:` definiuje hello wpis programu SQL Server dla hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="6db4a-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="6db4a-139">Można użyć dowolnego wolisz dla debugowania lokalnego programu SQL Server, tak długo, jak jest dostępny z hosta.</span><span class="sxs-lookup"><span data-stu-id="6db4a-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="6db4a-140">Jednak **localdb** nie obsługuje `container -> host` komunikacji.</span><span class="sxs-lookup"><span data-stu-id="6db4a-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="6db4a-141">Programem SQL Server w kontenerze nie obsługuje trwałych danych.</span><span class="sxs-lookup"><span data-stu-id="6db4a-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="6db4a-142">Po zatrzymaniu kontenera hello wymazaniu danych.</span><span class="sxs-lookup"><span data-stu-id="6db4a-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="6db4a-143">Nie używaj tej konfiguracji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="6db4a-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="6db4a-144">Przejdź toohello `fabrikamfiber.web:` węzeł i Dodaj węzeł podrzędny o nazwie `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="6db4a-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="6db4a-145">Gwarantuje to, że hello `db` usługi (kontenera hello programu SQL Server), który rozpoczyna się przed naszej aplikacji sieci web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="6db4a-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="6db4a-146">Aktualizacja konfiguracji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="6db4a-146">Update hello web config</span></span>

<span data-ttu-id="6db4a-147">Po powrocie do hello **FabrikamFiber.Web** projektu, ciąg połączenia hello aktualizacji w hello **web.config** pliku toohello toopoint programu SQL Server w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="6db4a-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="6db4a-148">Jeśli toouse inny serwer SQL podczas kompilowania zlecenia tworzenie aplikacji sieci web, należy dodać innego pliku web.release.config tooyour parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="6db4a-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="6db4a-149">Twoje kontener testu</span><span class="sxs-lookup"><span data-stu-id="6db4a-149">Test your container</span></span>

<span data-ttu-id="6db4a-150">Naciśnij klawisz **F5** toorun i debugowania aplikacji hello w kontenerze sieci.</span><span class="sxs-lookup"><span data-stu-id="6db4a-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="6db4a-151">Krawędź otwiera stronę zdefiniowanych uruchamiania aplikacji przy użyciu adresu IP hello kontenera hello na powitania wewnętrzny translatora adresów Sieciowych sieci (zazwyczaj 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="6db4a-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="6db4a-152">Zobacz toolearn więcej informacji o debugowaniu aplikacji w kontenerach przy użyciu programu Visual Studio 2017 r. [w tym artykule][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="6db4a-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![przykład firma fabrikam w kontenerze][image-web-preview]

<span data-ttu-id="6db4a-154">kontener Hello jest teraz gotowy toobe wbudowany i opakowane w aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6db4a-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="6db4a-155">Po utworzeniu obrazu kontenera hello oparty na tym komputerze, możesz wypchnąć go tooany kontenera rejestru i rozwiń tooany toorun hosta.</span><span class="sxs-lookup"><span data-stu-id="6db4a-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="6db4a-156">Przygotowanie aplikacji hello hello chmury</span><span class="sxs-lookup"><span data-stu-id="6db4a-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="6db4a-157">gotowy do uruchomienia w sieci szkieletowej usług na platformie Azure aplikacji hello tooget, potrzebujemy toocomplete należy wykonać dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="6db4a-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="6db4a-158">Udostępnianie portu hello, gdy chcemy tooreach stanie toobe naszej aplikacji sieci web w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="6db4a-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="6db4a-159">Podaj produkcji gotowy bazy danych SQL dla naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6db4a-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="6db4a-160">Udostępnianie portów hello aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6db4a-160">Expose hello port for hello app</span></span>
<span data-ttu-id="6db4a-161">Możemy skonfigurowano klaster sieci szkieletowej usług Hello ma port *80* otwarty domyślnie hello modułu równoważenia obciążenia Azure, która równoważy przychodzącego ruchu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="6db4a-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="6db4a-162">Uwidaczniamy naszych kontenera na tym porcie za pośrednictwem naszego plik docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="6db4a-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="6db4a-163">W programie Visual Studio Otwórz **Eksploratora rozwiązań**, Znajdź **rozwiązania docker compose**i otwórz hello pliku **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="6db4a-164">Modyfikowanie hello `fabrikamfiber.web:` węzła, Dodaj węzeł podrzędny o nazwie `ports:`.</span><span class="sxs-lookup"><span data-stu-id="6db4a-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="6db4a-165">Dodaj wpis ciąg `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="6db4a-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="6db4a-166">Użyj produkcyjną bazę danych SQL</span><span class="sxs-lookup"><span data-stu-id="6db4a-166">Use a production SQL database</span></span>
<span data-ttu-id="6db4a-167">Podczas uruchamiania w środowisku produkcyjnym, potrzebujemy nasze dane utrwalone w naszej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6db4a-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="6db4a-168">Nie ma obecnie żadnych danych trwałych tooguarantee sposób w kontenerze, dlatego nie można zapisać danych produkcyjnych w programie SQL Server w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="6db4a-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="6db4a-169">Zaleca się korzystanie z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6db4a-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="6db4a-170">tooset zapasowej i uruchamiania zarządzanego serwera SQL na platformie Azure, odwiedź hello [Quickstarts bazy danych SQL Azure] [ link-azure-sql] artykułu.</span><span class="sxs-lookup"><span data-stu-id="6db4a-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="6db4a-171">Pamiętaj toochange hello połączenie ciągów toohello programu SQL server w hello **web.release.config** pliku w hello **FabrikamFiber.Web** projektu.</span><span class="sxs-lookup"><span data-stu-id="6db4a-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="6db4a-172">Ta aplikacja powiedzie się, jeśli baza danych SQL jest osiągalny.</span><span class="sxs-lookup"><span data-stu-id="6db4a-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="6db4a-173">Można wybrać toogo wyprzedzeniem i wdrażanie aplikacji hello bez serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="6db4a-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="6db4a-174">Rozmieszczanie za pomocą programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6db4a-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="6db4a-175">tooset wdrożenia przy użyciu programu Visual Studio Team Services, potrzebne tooinstall hello [rozszerzenie ciągłego dostarczania narzędzi dla programu Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="6db4a-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="6db4a-176">To rozszerzenie umożliwia łatwe toodeploy tooAzure przez skonfigurowanie Visual Studio Team Services i korzystaj z klastra usługi sieć szkieletowa tooyour wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6db4a-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="6db4a-177">tooget pracę, kod musi być hostowany w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="6db4a-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="6db4a-178">Witaj pozostałej części tej sekcji założono **git** jest używany.</span><span class="sxs-lookup"><span data-stu-id="6db4a-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="6db4a-179">Konfigurowanie repozytorium VSTS</span><span class="sxs-lookup"><span data-stu-id="6db4a-179">Set up a VSTS repo</span></span>
<span data-ttu-id="6db4a-180">W prawym dolnym rogu hello programu Visual Studio, kliknij **Dodaj formant tooSource** > **Git** (lub użyć jednego z tych opcji).</span><span class="sxs-lookup"><span data-stu-id="6db4a-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Naciśnij przycisk kontroli źródła hello][image-source-control]

<span data-ttu-id="6db4a-182">W hello _Team Explorer_ okienka, naciśnij klawisz **Publikuj repozytorium Git**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="6db4a-183">Wybierz nazwę repozytorium VSTS i naciśnij klawisz **repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-183">Select your VSTS repository name and press **Repository**.</span></span>

![Publikowanie tooVSTS repozytorium][image-publish-repo]

<span data-ttu-id="6db4a-185">Teraz, gdy kod jest zsynchronizowany z repozytorium źródłowe VSTS, można skonfigurować ciągłej integracji i ciągłego dostarczania.</span><span class="sxs-lookup"><span data-stu-id="6db4a-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="6db4a-186">Instalator ciągłego dostarczania</span><span class="sxs-lookup"><span data-stu-id="6db4a-186">Setup continuous delivery</span></span>

<span data-ttu-id="6db4a-187">W _Eksploratora rozwiązań_, kliknij prawym przyciskiem myszy hello **rozwiązania** > **skonfigurować ciągłego dostarczania**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="6db4a-188">Wybierz hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6db4a-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="6db4a-189">Ustaw **typ hosta** za**klastra sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="6db4a-190">Ustaw **hosta docelowego** klastra sieci szkieletowej usług toohello utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="6db4a-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="6db4a-191">Wybierz **rejestru kontenera** toopublish Twojego kontenera do.</span><span class="sxs-lookup"><span data-stu-id="6db4a-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="6db4a-192">Użyj hello **Edytuj** toocreate przycisk rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="6db4a-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="6db4a-193">Naciśnij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6db4a-193">Press **OK**.</span></span>

![Instalator usługi sieci szkieletowej ciągłej integracji][image-setup-ci]
   
   <span data-ttu-id="6db4a-195">Po zakończeniu konfiguracji hello z kontenera jest wdrożony tooService sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="6db4a-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="6db4a-196">Zawsze, gdy wypychanie aktualizacji toohello repozytorium jest wykonywany nowej kompilacji i wydania.</span><span class="sxs-lookup"><span data-stu-id="6db4a-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="6db4a-197">Kompilowanie hello kontener obrazów potrwać około 15 minut.</span><span class="sxs-lookup"><span data-stu-id="6db4a-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="6db4a-198">klaster sieci szkieletowej usług toohello pierwszego wdrożenia Hello powoduje, że hello podstawowej systemu Windows Server Core kontener obrazów toobe pobrane.</span><span class="sxs-lookup"><span data-stu-id="6db4a-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="6db4a-199">Pobieranie Hello przyjmuje toocomplete dodatkowe 5 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="6db4a-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="6db4a-200">Przeglądaj toohello Fabrikam biurem aplikacji przy użyciu adresu url hello klastra: na przykład *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="6db4a-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="6db4a-201">Teraz, gdy masz konteneryzowanych i wdrożyć rozwiązanie firmy Fabrikam biurem hello, możesz otworzyć hello [portalu Azure] [ link-azure-portal] i aplikacja hello w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6db4a-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="6db4a-202">Aplikacja hello tootry, otwórz przeglądarkę sieci web i przejdź toohello adres URL klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="6db4a-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6db4a-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6db4a-203">Next steps</span></span>

<span data-ttu-id="6db4a-204">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6db4a-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6db4a-205">Tworzenie projektu platformy Docker w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6db4a-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="6db4a-206">Containerize istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6db4a-206">Containerize an existing application</span></span>
> * <span data-ttu-id="6db4a-207">Instalator ciągłej integracji z programu Visual Studio i VSTS</span><span class="sxs-lookup"><span data-stu-id="6db4a-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
