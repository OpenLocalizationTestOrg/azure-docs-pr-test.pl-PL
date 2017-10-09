---
title: "aaaCI/CD z aparatem usługi kontenera Azure i tryb Swarm | Dokumentacja firmy Microsoft"
description: "Aparat usługi kontenera Azure za pomocą toodeliver stale aplikacji .NET Core wielu kontenera Docker Swarm tryb rejestru kontenera Azure i Visual Studio Team Services"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, kontenerów, Micro-services, Swarm, Azure, programu Visual Studio Team usług, metodyki DevOps, aparat ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="22aa4-104">Pełna CI/CD toodeploy potoku aplikacji usługi kontenera w usłudze kontenera platformy Azure z aparatem ACS i Docker Swarm trybie przy użyciu programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="22aa4-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="22aa4-105">*Ten artykuł jest oparty na [CI pełnej/CD potoku toodeploy aplikacji usługi kontenera w usłudze kontenera platformy Azure przy użyciu rozwiązania Docker Swarm przy użyciu programu Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) dokumentacji*</span><span class="sxs-lookup"><span data-stu-id="22aa4-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="22aa4-106">Dzisiaj jeden z hello największych wyzwań po opracowywanie nowoczesnych aplikacji w chmurze hello jest możliwe toodeliver te aplikacje stale.</span><span class="sxs-lookup"><span data-stu-id="22aa4-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="22aa4-107">W tym artykule dowiesz się, jak tooimplement pełnej ciągłej integracji i wdrażania (CI/CD) potoku, przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="22aa4-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="22aa4-108">Aparat usługi kontenera platformy Azure z Docker Swarm trybem</span><span class="sxs-lookup"><span data-stu-id="22aa4-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="22aa4-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="22aa4-109">Azure Container Registry</span></span>
* <span data-ttu-id="22aa4-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="22aa4-110">Visual Studio Team Services</span></span>

<span data-ttu-id="22aa4-111">Ten artykuł jest oparty na prostej aplikacji, dostępnych na [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), rozwinięte z platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="22aa4-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="22aa4-112">Aplikacja Hello składa się z czterech różnych usług: trzy sieci web, interfejsów API i frontonu sieci web co:</span><span class="sxs-lookup"><span data-stu-id="22aa4-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="22aa4-114">cel Hello jest toodeliver tej aplikacji stale w klastrze Docker Swarm tryb, za pomocą programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="22aa4-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="22aa4-115">następujące Hello rysunek szczegóły tego potoku ciągłego dostarczania:</span><span class="sxs-lookup"><span data-stu-id="22aa4-115">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="22aa4-117">Poniżej przedstawiono krótki opis kroków hello:</span><span class="sxs-lookup"><span data-stu-id="22aa4-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="22aa4-118">Zmiany kodu są repozytorium kodu źródłowego zatwierdzone toohello (tutaj GitHub)</span><span class="sxs-lookup"><span data-stu-id="22aa4-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="22aa4-119">GitHub uaktywnia kompilację w Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="22aa4-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="22aa4-120">Visual Studio Team Services pobiera najnowsza wersja źródła hello hello i tworzy wszystkie obrazy hello tworzące aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="22aa4-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="22aa4-121">Visual Studio Team Services wypchnięcia każdego obrazu tooa Docker rejestru utworzone za pomocą usługi Azure kontenera rejestru hello</span><span class="sxs-lookup"><span data-stu-id="22aa4-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="22aa4-122">Visual Studio Team Services wyzwala nową wersją</span><span class="sxs-lookup"><span data-stu-id="22aa4-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="22aa4-123">Niektóre polecenia przy użyciu protokołu SSH w węźle głównym klastra usługi kontenera platformy Azure hello uruchamia Hello zlecenia</span><span class="sxs-lookup"><span data-stu-id="22aa4-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="22aa4-124">Tryb docker Swarm w klastrze hello ściąga hello najnowszej wersji hello obrazów</span><span class="sxs-lookup"><span data-stu-id="22aa4-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="22aa4-125">nową wersję aplikacji hello Hello jest wdrażane za pomocą Docker stosu</span><span class="sxs-lookup"><span data-stu-id="22aa4-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="22aa4-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22aa4-126">Prerequisites</span></span>

<span data-ttu-id="22aa4-127">Przed rozpoczęciem tego samouczka potrzebne hello toocomplete następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="22aa4-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="22aa4-128">Tworzenie klastra trybu Swarm usługi kontenera platformy Azure z aparatem ACS</span><span class="sxs-lookup"><span data-stu-id="22aa4-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="22aa4-129">Połącz z klastrem Swarm hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22aa4-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="22aa4-130">Tworzenie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22aa4-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="22aa4-131">Utworzony projekt konta i zespołu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="22aa4-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="22aa4-132">Rozwidlania tooyour repozytorium GitHub hello konto GitHub</span><span class="sxs-lookup"><span data-stu-id="22aa4-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="22aa4-133">Witaj orchestrator Docker Swarm usługi kontenera platformy Azure używa starszej wersji autonomicznej Swarm.</span><span class="sxs-lookup"><span data-stu-id="22aa4-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="22aa4-134">Obecnie zintegrowane hello [tryb Swarm](https://docs.docker.com/engine/swarm/) (w Docker 1.12 lub nowszej) nie jest obsługiwane orchestrator w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="22aa4-135">Z tego powodu używamy [aparat ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), przyczyniły się społeczności [szablon szybkiego startu](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), lub rozwiązania Docker w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="22aa4-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="22aa4-136">Krok 1: Skonfiguruj konto usługi Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="22aa4-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="22aa4-137">W tej sekcji należy skonfigurować konto w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="22aa4-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="22aa4-138">tooconfigure VSTS usługi punktów końcowych, projektu Visual Studio Team Services, kliknij przycisk hello **ustawienia** ikonę w hello narzędzi i wybierz **usług**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Punkt końcowy usługi otwarte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="22aa4-140">Połącz konto usługi Visual Studio Team Services i platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22aa4-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="22aa4-141">Skonfiguruj połączenie między projektu programu VSTS i konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="22aa4-142">Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **usługi Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="22aa4-143">tooauthorize toowork programu VSTS z Twoim kontem platformy Azure, wybierz użytkownika **subskrypcji** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services — autoryzować Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="22aa4-145">Połączenie usługi Visual Studio Team Services i GitHub</span><span class="sxs-lookup"><span data-stu-id="22aa4-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="22aa4-146">Skonfiguruj połączenie między projektu programu VSTS oraz konto GitHub.</span><span class="sxs-lookup"><span data-stu-id="22aa4-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="22aa4-147">Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="22aa4-148">Kliknij tooauthorize toowork programu VSTS z Twoim kontem usługi GitHub **autoryzacji** i wykonaj procedurę hello w otwartym oknie hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services — autoryzować GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="22aa4-150">Łączenie programu VSTS tooyour klastra usługi kontenera Azure</span><span class="sxs-lookup"><span data-stu-id="22aa4-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="22aa4-151">kroki ostatniego Hello przed przejściem do potoku CI/CD hello są tooconfigure połączeń zewnętrznych tooyour Docker Swarm klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="22aa4-152">Klaster Docker Swarm hello Dodawanie punktu końcowego typu **SSH**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="22aa4-153">Następnie wprowadź informacje o połączeniu SSH hello klastra Swarm (węzeł główny).</span><span class="sxs-lookup"><span data-stu-id="22aa4-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="22aa4-155">Cała konfiguracja hello odbywa się teraz.</span><span class="sxs-lookup"><span data-stu-id="22aa4-155">All hello configuration is done now.</span></span> <span data-ttu-id="22aa4-156">W następnych krokach hello możesz utworzyć hello CI/CD potok, który tworzy i wdraża klaster Docker Swarm toohello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="22aa4-157">Krok 2: Tworzenie definicji kompilacji hello</span><span class="sxs-lookup"><span data-stu-id="22aa4-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="22aa4-158">W tym kroku skonfigurować definicję kompilacji projektu programu VSTS i zdefiniuj hello przepływu pracy kompilacji dla obrazów kontenera</span><span class="sxs-lookup"><span data-stu-id="22aa4-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="22aa4-159">Definicja początkowej instalacji</span><span class="sxs-lookup"><span data-stu-id="22aa4-159">Initial definition setup</span></span>

1. <span data-ttu-id="22aa4-160">tooyour projektu Visual Studio Team Services i kliknij przycisk Połącz toocreate definicję kompilacji **kompilacji i wydania**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="22aa4-161">W hello **definicje kompilacji** kliknij **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services — nowej definicji kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="22aa4-163">Wybierz hello **pusta procesu**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-163">Select hello **Empty process**.</span></span>

    ![Definicja kompilacji programu Visual Studio Team Services — nowy pusty](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="22aa4-165">Następnie kliknij przycisk hello **zmienne** karcie i Utwórz dwa nowe zmienne: **RegistryURL** i **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="22aa4-166">Wklej hello wartości rejestru i DNS agentów klastra.</span><span class="sxs-lookup"><span data-stu-id="22aa4-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — Konfiguracja zmienne kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="22aa4-168">Na powitania **definicji kompilacji** strony, otwórz hello **wyzwalaczy** i skonfiguruj hello kompilacji toouse ciągłej integracji z rozwidlenia hello hello MyShop projektu, który został utworzony w hello wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="22aa4-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="22aa4-169">Następnie wybierz opcję **partii zmian**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="22aa4-170">Upewnij się, że wybrano *docker linux* jako hello **gałęzi specyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="22aa4-172">Na koniec kliknij hello **opcje** i skonfiguruj hello domyślnej agenta kolejki zbyt**Podgląd Linux hostowanych**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services — konfiguracja agenta hosta](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="22aa4-174">Zdefiniuj hello przepływu pracy kompilacji</span><span class="sxs-lookup"><span data-stu-id="22aa4-174">Define hello build workflow</span></span>
<span data-ttu-id="22aa4-175">Następne kroki Hello zdefiniuj hello przepływu pracy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="22aa4-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="22aa4-176">Najpierw należy tooconfigure hello źródła hello kodu.</span><span class="sxs-lookup"><span data-stu-id="22aa4-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="22aa4-177">toodo go, wybierz opcję **GitHub** i **repozytorium** i **gałęzi** (docker linux).</span><span class="sxs-lookup"><span data-stu-id="22aa4-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Konfigurowanie programu Visual Studio Team Services — kodu źródłowego](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="22aa4-179">Istnieje pięć toobuild obrazów kontener dla hello *MyShop* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22aa4-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="22aa4-180">Obraz jest utworzony przy użyciu powitalne plik Dockerfile znajdujących się w folderach projektu hello:</span><span class="sxs-lookup"><span data-stu-id="22aa4-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="22aa4-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="22aa4-181">ProductsApi</span></span>
* <span data-ttu-id="22aa4-182">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="22aa4-182">Proxy</span></span>
* <span data-ttu-id="22aa4-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="22aa4-183">RatingsApi</span></span>
* <span data-ttu-id="22aa4-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="22aa4-184">RecommandationsApi</span></span>
* <span data-ttu-id="22aa4-185">Sklepu</span><span class="sxs-lookup"><span data-stu-id="22aa4-185">ShopFront</span></span>

<span data-ttu-id="22aa4-186">Należy dwa kroki Docker dla każdego obrazu, jeden obraz powitania toobuild i jeden obraz powitania toopush hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="22aa4-187">tooadd etapem hello przepływu pracy kompilacji, kliknij przycisk **+ Dodaj krok kompilacji** i wybierz **Docker**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services — dodać kroki procesu kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="22aa4-189">Dla każdego obrazu, należy skonfigurować jeden krok, który używa hello `docker build` polecenia.</span><span class="sxs-lookup"><span data-stu-id="22aa4-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services — Docker kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="22aa4-191">Na powitania utworzyć operację, wybierz rejestru kontenera platformy Azure, hello **kompilacji obrazu** akcji i hello plik Dockerfile, który definiuje każdego obrazu.</span><span class="sxs-lookup"><span data-stu-id="22aa4-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="22aa4-192">Zestaw hello **katalog roboczy** jako katalog główny plik Dockerfile hello, zdefiniuj hello **nazwa obrazu**i wybierz **zawierają najnowsze tagu**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="22aa4-193">Nazwa obrazu Hello ma toobe w następującym formacie: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="22aa4-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="22aa4-194">Zastąp **[nazwa]** o nazwie obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="22aa4-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="22aa4-195">Dla każdego obrazu, skonfiguruj drugi krok, który używa hello `docker push` polecenia.</span><span class="sxs-lookup"><span data-stu-id="22aa4-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services — Docker Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="22aa4-197">Dla operacji wypychania hello, wybierz rejestru kontenera platformy Azure, hello **Push obrazu** akcji, wprowadź hello **nazwa obrazu** wbudowane w poprzednim kroku hello i wybierz **zawierają najnowsze Tag** .</span><span class="sxs-lookup"><span data-stu-id="22aa4-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="22aa4-198">Po skonfigurowaniu hello kompilacji i push kroki dla każdego z pięciu obrazów hello, Dodaj trzy kroki więcej w hello kompilacji przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="22aa4-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services — Dodaj zadania wiersza polecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="22aa4-200">Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *RegistryURL* wystąpienie w plik docker-compose.yml hello hello RegistryURL zmienną.</span><span class="sxs-lookup"><span data-stu-id="22aa4-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services — plik Redaguj aktualizacji z adresem URL rejestru](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="22aa4-202">Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *AgentURL* wystąpienie w plik docker-compose.yml hello hello AgentURL zmienną.</span><span class="sxs-lookup"><span data-stu-id="22aa4-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="22aa4-203">Zadanie porzuca hello aktualizowana tworzenia pliku jako artefaktów kompilacji dzięki mogą być używane w hello wersji.</span><span class="sxs-lookup"><span data-stu-id="22aa4-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="22aa4-204">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="22aa4-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services — Opublikuj artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Usługi Visual Studio Team - publikowania tworzenia pliku](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="22aa4-207">Kliknij przycisk **Zapisz & kolejka** tootest definicję kompilacji.</span><span class="sxs-lookup"><span data-stu-id="22aa4-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services — zapisywanie i kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services — nowej kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="22aa4-210">Jeśli hello **kompilacji** jest poprawna, masz toosee ten ekran:</span><span class="sxs-lookup"><span data-stu-id="22aa4-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services — kompilacja powiodła się](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="22aa4-212">Krok 3: Tworzenie definicji wersji hello</span><span class="sxs-lookup"><span data-stu-id="22aa4-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="22aa4-213">Visual Studio Team Services służy za[zarządzania wersjami w środowiskach](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="22aa4-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="22aa4-214">Można włączyć się, że aplikacja jest wdrożony na Twoje różnych środowiskach (np. dev, test produkcji wstępnej i produkcji) w sposób toomake ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="22aa4-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="22aa4-215">Można utworzyć środowisko, które reprezentuje klastra tryb Azure kontenera usługi Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="22aa4-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services — tooACS zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="22aa4-217">Początkowa wersja Instalatora</span><span class="sxs-lookup"><span data-stu-id="22aa4-217">Initial release setup</span></span>

1. <span data-ttu-id="22aa4-218">toocreate definicji wersji, kliknij przycisk **wersje** > **+ zlecenia**</span><span class="sxs-lookup"><span data-stu-id="22aa4-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="22aa4-219">tooconfigure hello artefaktu źródłowego, kliknij przycisk **artefakty** > **połączenia źródła artefaktu**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="22aa4-220">W tym miejscu łącze nowej wersji definicji toohello kompilacji zdefiniowanego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="22aa4-221">Po wykonaniu tej plik docker-compose.yml hello jest dostępna w procesie zlecenia hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - wersja artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="22aa4-223">wyzwalacz wersji hello tooconfigure, kliknij przycisk **wyzwalaczy** i wybierz **ciągłe wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="22aa4-224">Zestaw wyzwalacza hello na powitania tego samego źródła artefaktu.</span><span class="sxs-lookup"><span data-stu-id="22aa4-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="22aa4-225">To ustawienie zapewnia, że rozpoczyna się nowej wersji, gdy hello kompilacja zostaje ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="22aa4-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services — wyzwalaczy zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="22aa4-227">zmienne wersji hello tooconfigure, kliknij przycisk **zmienne** i wybierz **+ zmiennej** toocreate trzy nowe zmienne z użyciem informacji hello rejestru hello: **docker.username**, **docker.password**, i **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="22aa4-228">Wklej hello wartości rejestru i DNS agentów klastra.</span><span class="sxs-lookup"><span data-stu-id="22aa4-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="22aa4-230">Jak pokazano na poprzednich ekranie powitania, kliknij przycisk hello **blokady** checkbox w docker.password.</span><span class="sxs-lookup"><span data-stu-id="22aa4-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="22aa4-231">To ustawienie jest ważne toorestrict hello hasła.</span><span class="sxs-lookup"><span data-stu-id="22aa4-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="22aa4-232">Zdefiniuj hello wersji w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="22aa4-232">Define hello release workflow</span></span>

<span data-ttu-id="22aa4-233">przepływ pracy wersji Hello składa się z dwóch zadań, które można dodać.</span><span class="sxs-lookup"><span data-stu-id="22aa4-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="22aa4-234">Konfigurowanie zadań toosecurely kopiowania hello utworzenie pliku tooa *wdrażania* folderu na powitania Docker Swarm węzła głównego, przy użyciu połączenia SSH hello został wcześniej skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="22aa4-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="22aa4-235">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="22aa4-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="22aa4-236">Folder źródłowy:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="22aa4-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - wersja punkt połączenia usługi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="22aa4-238">Skonfiguruj drugi tooexecute zadań toorun polecenia bash `docker` i `docker stack deploy` poleceń na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="22aa4-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="22aa4-239">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="22aa4-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services — Bash zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="22aa4-241">polecenie Hello wykonane na wzorcu hello używa hello interfejsu wiersza polecenia Docker i hello toodo rozwiązania Docker Compose CLI hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="22aa4-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="22aa4-242">Zaloguj się w rejestrze kontenera platformy Azure toohello (używa trzech zmiennych kompilacji, które są zdefiniowane w hello **zmienne** kartę)</span><span class="sxs-lookup"><span data-stu-id="22aa4-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="22aa4-243">Zdefiniuj hello **DOCKER_HOST** toowork zmiennej z punktu końcowego Swarm hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="22aa4-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="22aa4-244">Przejdź toohello *wdrażanie* folderu, który został utworzony przez hello poprzedzających zadanie kopiowania bezpiecznego i który zawiera plik docker-compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="22aa4-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="22aa4-245">Wykonanie `docker stack deploy` poleceń ściągnięcia nowych obrazów hello i utworzyć hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="22aa4-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="22aa4-246">Jak pokazano na poprzednich ekranie powitania, pozostaw hello **zakończyć się niepowodzeniem ze strumienia STDERR** niezaznaczone pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="22aa4-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="22aa4-247">To ustawienie pozwala nam procesu publikacji hello toocomplete powodu zbyt`docker-compose` wyświetla komunikaty diagnostyczne, takie jak kontenery są zatrzymywanie lub usuwany na powitania błędów w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="22aa4-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="22aa4-248">Po zaznaczeniu pola wyboru hello Visual Studio Team Services raporty błędów, które wystąpiły podczas wersji hello, nawet jeśli wszystko przebiegnie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="22aa4-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="22aa4-249">Zapisz ten nowej definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="22aa4-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="22aa4-250">Krok 4: Testowanie hello CI/CD potoku</span><span class="sxs-lookup"><span data-stu-id="22aa4-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="22aa4-251">Teraz, po zakończeniu konfiguracji hello, jest czas tootest nowy potok CI/CD.</span><span class="sxs-lookup"><span data-stu-id="22aa4-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="22aa4-252">Hello Najprostszym sposobem tootest jest tooupdate hello źródła kodu i zatwierdzania hello zmienia się w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="22aa4-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="22aa4-253">Kilka sekund po wypchnąć kod hello, zobaczysz nowej kompilacji uruchomionych w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="22aa4-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="22aa4-254">Po pomyślnym ukończeniu nowej wersji wyzwoleniu i wdrożyć hello nowej wersji aplikacji hello na powitania klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22aa4-255">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22aa4-255">Next steps</span></span>

* <span data-ttu-id="22aa4-256">Aby uzyskać więcej informacji na temat CI/CD z Visual Studio Team Services, zobacz hello [kompilacji programu VSTS omówienie](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="22aa4-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="22aa4-257">Aby uzyskać więcej informacji na temat aparatu ACS, zobacz hello [repozytorium GitHub aparat ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="22aa4-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="22aa4-258">Aby uzyskać więcej informacji o trybie Docker Swarm, zobacz hello [Docker Swarm Omówienie trybu](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="22aa4-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
