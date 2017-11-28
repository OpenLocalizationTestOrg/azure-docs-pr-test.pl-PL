---
title: "CI/CD z aparatem usługi kontenera platformy Azure i tryb Swarm | Dokumentacja firmy Microsoft"
description: "Użyć aparat usługi kontenera platformy Azure z Docker Swarm tryb rejestru kontenera Azure i Visual Studio Team Services w celu dostarczenia stale aplikacji .NET Core wielu kontenera"
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
ms.openlocfilehash: 2c0e5fe4f60738fcc1aa67a78674e6f3c62e5628
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="67b5c-104">Pełny potok CI/CD do wdrażania aplikacji usługi kontenera w usłudze kontenera platformy Azure z aparatem ACS i Docker Swarm trybie przy użyciu programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="67b5c-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="67b5c-105">*Ten artykuł jest oparty na [CI pełnej/CD potoku do wdrażania aplikacji usługi kontenera w usłudze kontenera platformy Azure przy użyciu rozwiązania Docker Swarm przy użyciu programu Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) dokumentacji*</span><span class="sxs-lookup"><span data-stu-id="67b5c-105">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="67b5c-106">Dzisiaj jedną z największych wyzwań podczas tworzenia nowoczesnych aplikacji w chmurze jest możliwość ciągłego dostarczania tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-106">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="67b5c-107">W tym artykule dowiesz się implementowania pełnej ciągłej integracji i wdrażania (CI/CD) potoku przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="67b5c-107">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="67b5c-108">Aparat usługi kontenera platformy Azure z Docker Swarm trybem</span><span class="sxs-lookup"><span data-stu-id="67b5c-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="67b5c-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="67b5c-109">Azure Container Registry</span></span>
* <span data-ttu-id="67b5c-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="67b5c-110">Visual Studio Team Services</span></span>

<span data-ttu-id="67b5c-111">Ten artykuł jest oparty na prostej aplikacji, dostępnych na [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), rozwinięte z platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="67b5c-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="67b5c-112">Aplikacja składa się z czterech różnych usług: trzy sieci web, interfejsów API i frontonu sieci web co:</span><span class="sxs-lookup"><span data-stu-id="67b5c-112">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="67b5c-114">Celem jest stale świadczenia tej aplikacji w klastrze Docker Swarm tryb, za pomocą programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="67b5c-114">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="67b5c-115">Poniższa ilustracja szczegóły tego potoku ciągłego dostarczania:</span><span class="sxs-lookup"><span data-stu-id="67b5c-115">The following figure details this continuous delivery pipeline:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="67b5c-117">Poniżej przedstawiono krótki opis kroków:</span><span class="sxs-lookup"><span data-stu-id="67b5c-117">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="67b5c-118">Zmiany kodu zostały zastosowane w repozytorium kodu źródłowego (tutaj GitHub)</span><span class="sxs-lookup"><span data-stu-id="67b5c-118">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="67b5c-119">GitHub uaktywnia kompilację w Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="67b5c-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="67b5c-120">Visual Studio Team Services pobiera najnowsza wersja źródła i tworzy wszystkie obrazy, które tworzą aplikacji</span><span class="sxs-lookup"><span data-stu-id="67b5c-120">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="67b5c-121">Visual Studio Team Services wypychanie każdego obrazu do rejestru Docker utworzone za pomocą usługi Azure kontenera rejestru</span><span class="sxs-lookup"><span data-stu-id="67b5c-121">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="67b5c-122">Visual Studio Team Services wyzwala nową wersją</span><span class="sxs-lookup"><span data-stu-id="67b5c-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="67b5c-123">Wersja uruchamia niektóre polecenia przy użyciu protokołu SSH w węźle głównym klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67b5c-123">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="67b5c-124">Tryb docker Swarm w klastrze pobiera najnowsza wersja obrazów</span><span class="sxs-lookup"><span data-stu-id="67b5c-124">Docker Swarm Mode on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="67b5c-125">Wdrożenie nowej wersji aplikacji za pomocą Docker stosu</span><span class="sxs-lookup"><span data-stu-id="67b5c-125">The new version of the application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="67b5c-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="67b5c-126">Prerequisites</span></span>

<span data-ttu-id="67b5c-127">Przed rozpoczęciem tego samouczka, należy wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="67b5c-127">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="67b5c-128">Tworzenie klastra trybu Swarm usługi kontenera platformy Azure z aparatem ACS</span><span class="sxs-lookup"><span data-stu-id="67b5c-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="67b5c-129">Połączenie z klastrem Swarm w usłudze Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="67b5c-129">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="67b5c-130">Tworzenie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67b5c-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="67b5c-131">Utworzony projekt konta i zespołu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="67b5c-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="67b5c-132">Rozwidlenia repozytorium GitHub z kontem usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="67b5c-132">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="67b5c-133">Koordynator rozwiązania Docker Swarm w usłudze Azure Container Service korzysta ze starszego autonomicznego rozwiązania Swarm.</span><span class="sxs-lookup"><span data-stu-id="67b5c-133">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="67b5c-134">Obecnie zintegrowany [tryb Swarm](https://docs.docker.com/engine/swarm/) (na platformie Docker 1.12 lub nowszej) nie jest obsługiwanym koordynatorem w usłudze Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="67b5c-134">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="67b5c-135">Z tego powodu używamy [aparat ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), przyczyniły się społeczności [szablon szybkiego startu](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), lub rozwiązania Docker w [portalu Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="67b5c-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="67b5c-136">Krok 1: Skonfiguruj konto usługi Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="67b5c-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="67b5c-137">W tej sekcji należy skonfigurować konto w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="67b5c-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="67b5c-138">Kliknij, aby skonfigurować punkty końcowe usługi VSTS, projektu Visual Studio Team Services **ustawienia** ikonę na pasku narzędzi, a następnie wybierz **usług**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-138">To configure VSTS Services Endpoints, in your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

![Punkt końcowy usługi otwarte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="67b5c-140">Połącz konto usługi Visual Studio Team Services i platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67b5c-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="67b5c-141">Skonfiguruj połączenie między projektu programu VSTS i konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b5c-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="67b5c-142">Po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **usługi Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-142">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="67b5c-143">Aby autoryzować VSTS do pracy z konta platformy Azure, wybierz użytkownika **subskrypcji** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-143">To authorize VSTS to work with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services — autoryzować Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="67b5c-145">Połączenie usługi Visual Studio Team Services i GitHub</span><span class="sxs-lookup"><span data-stu-id="67b5c-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="67b5c-146">Skonfiguruj połączenie między projektu programu VSTS oraz konto GitHub.</span><span class="sxs-lookup"><span data-stu-id="67b5c-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="67b5c-147">Po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-147">On the left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="67b5c-148">Aby autoryzować VSTS do pracy z Twoim kontem usługi GitHub, kliknij przycisk **autoryzacji** i postępuj zgodnie z procedurą w otwartym oknie.</span><span class="sxs-lookup"><span data-stu-id="67b5c-148">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services — autoryzować GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-to-your-azure-container-service-cluster"></a><span data-ttu-id="67b5c-150">VSTS nawiązać połączenia z klastrem usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67b5c-150">Connect VSTS to your Azure Container Service cluster</span></span>

<span data-ttu-id="67b5c-151">Ostatni kroki przed pobraniem z potokiem CI/CD są do konfigurowania połączeń zewnętrznych z klastrem Docker Swarm w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="67b5c-151">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="67b5c-152">Aby klaster Docker Swarm Dodawanie punktu końcowego typu **SSH**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-152">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="67b5c-153">Następnie wprowadź informacje o połączeniu SSH klastra Swarm (węzeł główny).</span><span class="sxs-lookup"><span data-stu-id="67b5c-153">Then enter the SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="67b5c-155">Całą konfigurację odbywa się teraz.</span><span class="sxs-lookup"><span data-stu-id="67b5c-155">All the configuration is done now.</span></span> <span data-ttu-id="67b5c-156">W następnych krokach utworzysz potok CI/CD, który tworzy i wdraża aplikację w klastrze Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="67b5c-156">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="67b5c-157">Krok 2: Tworzenie definicji kompilacji</span><span class="sxs-lookup"><span data-stu-id="67b5c-157">Step 2: Create the build definition</span></span>

<span data-ttu-id="67b5c-158">W tym kroku skonfigurować definicję kompilacji projektu programu VSTS i zdefiniuj przepływu pracy kompilacji dla obrazów kontenera</span><span class="sxs-lookup"><span data-stu-id="67b5c-158">In this step, you set up a build definition for your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="67b5c-159">Definicja początkowej instalacji</span><span class="sxs-lookup"><span data-stu-id="67b5c-159">Initial definition setup</span></span>

1. <span data-ttu-id="67b5c-160">Aby utworzyć definicję kompilacji, nawiązać połączenia z projektu programu Visual Studio Team Services, a następnie kliknij przycisk **kompilacji i wydania**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-160">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="67b5c-161">W **definicje kompilacji** kliknij **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-161">In the **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services — nowej definicji kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="67b5c-163">Wybierz **pusta procesu**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-163">Select the **Empty process**.</span></span>

    ![Definicja kompilacji programu Visual Studio Team Services — nowy pusty](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="67b5c-165">Następnie kliknij przycisk **zmienne** karcie i Utwórz dwa nowe zmienne: **RegistryURL** i **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-165">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="67b5c-166">Wklej wartości rejestru i DNS agentów klastra.</span><span class="sxs-lookup"><span data-stu-id="67b5c-166">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — Konfiguracja zmienne kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="67b5c-168">Na **definicji kompilacji** Otwórz **wyzwalaczy** i skonfiguruj kompilację do korzystania z rozwidlenie projektu MyShop utworzonego w wymaganiach wstępnych ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-168">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="67b5c-169">Następnie wybierz opcję **partii zmian**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="67b5c-170">Upewnij się, że wybrano *docker linux* jako **gałęzi specyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-170">Make sure that you select *docker-linux* as the **Branch specification**.</span></span>

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="67b5c-172">Na koniec kliknij **opcje** i skonfiguruj domyślną agenta w kolejce **Podgląd Linux hostowanych**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-172">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services — konfiguracja agenta hosta](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="67b5c-174">Zdefiniuj przepływu pracy kompilacji</span><span class="sxs-lookup"><span data-stu-id="67b5c-174">Define the build workflow</span></span>
<span data-ttu-id="67b5c-175">Następne kroki zdefiniuj przepływu pracy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-175">The next steps define the build workflow.</span></span> <span data-ttu-id="67b5c-176">Najpierw należy skonfigurować źródła kodu.</span><span class="sxs-lookup"><span data-stu-id="67b5c-176">First, you need to configure the source of the code.</span></span> <span data-ttu-id="67b5c-177">Aby wykonać to zadanie, zaznacz **GitHub** i **repozytorium** i **gałęzi** (docker linux).</span><span class="sxs-lookup"><span data-stu-id="67b5c-177">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Konfigurowanie programu Visual Studio Team Services — kodu źródłowego](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="67b5c-179">Istnieje pięć obrazów kontenera do kompilacji dla *MyShop* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-179">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="67b5c-180">Obraz jest utworzony przy użyciu plik Dockerfile znajdujący się w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="67b5c-180">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="67b5c-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="67b5c-181">ProductsApi</span></span>
* <span data-ttu-id="67b5c-182">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="67b5c-182">Proxy</span></span>
* <span data-ttu-id="67b5c-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="67b5c-183">RatingsApi</span></span>
* <span data-ttu-id="67b5c-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="67b5c-184">RecommandationsApi</span></span>
* <span data-ttu-id="67b5c-185">Sklepu</span><span class="sxs-lookup"><span data-stu-id="67b5c-185">ShopFront</span></span>

<span data-ttu-id="67b5c-186">Należy dwa kroki Docker dla każdego obrazu: jeden do tworzenia obrazu i jeden do dystrybuowania obrazu w rejestrze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b5c-186">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="67b5c-187">Aby dodać krok w przepływie pracy kompilacji, kliknij przycisk **+ Dodaj krok kompilacji** i wybierz **Docker**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-187">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services — dodać kroki procesu kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="67b5c-189">Dla każdego obrazu, należy skonfigurować jeden krok, który używa `docker build` polecenia.</span><span class="sxs-lookup"><span data-stu-id="67b5c-189">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services — Docker kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="67b5c-191">Dla operacji kompilacji, wybierz rejestru kontenera platformy Azure, **kompilacji obrazu** akcji, a plik Dockerfile, który definiuje każdego obrazu.</span><span class="sxs-lookup"><span data-stu-id="67b5c-191">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="67b5c-192">Ustaw **katalog roboczy** jako katalog główny plik Dockerfile, zdefiniuj **nazwa obrazu**i wybierz **zawierają najnowsze tagu**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-192">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="67b5c-193">Nazwa obrazu musi być w następującym formacie: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="67b5c-193">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="67b5c-194">Zastąp **[nazwa]** o nazwie obrazu:</span><span class="sxs-lookup"><span data-stu-id="67b5c-194">Replace **[NAME]** with the image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="67b5c-195">Dla każdego obrazu, skonfiguruj drugi krok, który używa `docker push` polecenia.</span><span class="sxs-lookup"><span data-stu-id="67b5c-195">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services — Docker Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="67b5c-197">Dla operacji wypychania, wybierz rejestru kontenera platformy Azure, **Push obrazu** akcji, wprowadź **nazwa obrazu** wbudowane w poprzednim kroku, a następnie wybierz **zawierają najnowsze Tag**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-197">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="67b5c-198">Po skonfigurowaniu kroków kompilacji i wypychania dla każdego z pięciu obrazów, należy dodać trzy kolejne kroki w przepływie pracy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-198">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span></span>

   ![Visual Studio Team Services — Dodaj zadania wiersza polecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="67b5c-200">Zadania wiersza polecenia, który używa skryptów bash w celu zastąpienia *RegistryURL* wystąpienie w plik docker-compose.yml ze zmienną RegistryURL.</span><span class="sxs-lookup"><span data-stu-id="67b5c-200">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services — plik Redaguj aktualizacji z adresem URL rejestru](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="67b5c-202">Zadania wiersza polecenia, który używa skryptów bash w celu zastąpienia *AgentURL* wystąpienie w plik docker-compose.yml ze zmienną AgentURL.</span><span class="sxs-lookup"><span data-stu-id="67b5c-202">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="67b5c-203">Zadanie porzuca zaktualizowany plik Redaguj jako artefaktów kompilacji dzięki mogą być używane w wersji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-203">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="67b5c-204">Zobacz następujący ekran, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="67b5c-204">See the following screen for details.</span></span>

         ![Visual Studio Team Services — Opublikuj artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Usługi Visual Studio Team - publikowania tworzenia pliku](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="67b5c-207">Kliknij przycisk **Zapisz & kolejka** do testowania definicję kompilacji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-207">Click **Save & queue** to test your build definition.</span></span>

   ![Visual Studio Team Services — zapisywanie i kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services — nowej kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="67b5c-210">Jeśli **kompilacji** jest poprawna, masz wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="67b5c-210">If the **Build** is correct, you have to see this screen:</span></span>

  ![Visual Studio Team Services — kompilacja powiodła się](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="67b5c-212">Krok 3: Tworzenie definicji wersji</span><span class="sxs-lookup"><span data-stu-id="67b5c-212">Step 3: Create the release definition</span></span>

<span data-ttu-id="67b5c-213">Visual Studio Team Services umożliwia [zarządzania wersjami w środowiskach](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="67b5c-213">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="67b5c-214">Można włączyć ciągłego wdrażania upewnić się, że aplikacja jest wdrożony na Twoje różnych środowiskach (np. dev, test produkcji wstępnej i produkcji) w sposób.</span><span class="sxs-lookup"><span data-stu-id="67b5c-214">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="67b5c-215">Można utworzyć środowisko, które reprezentuje klastra tryb Azure kontenera usługi Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="67b5c-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services — w wersji usług ACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="67b5c-217">Początkowa wersja Instalatora</span><span class="sxs-lookup"><span data-stu-id="67b5c-217">Initial release setup</span></span>

1. <span data-ttu-id="67b5c-218">Do tworzenia definicji wersji, kliknij przycisk **wersje** > **+ zlecenia**</span><span class="sxs-lookup"><span data-stu-id="67b5c-218">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="67b5c-219">Kliknij, aby skonfigurować źródła artefaktu **artefakty** > **połączenia źródła artefaktu**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-219">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="67b5c-220">W tym miejscu połączyć tej nowej wersji definicji kompilacji, który został zdefiniowany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="67b5c-220">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="67b5c-221">Po wykonaniu tej plik docker-compose.yml jest dostępna w procesie wersji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-221">After that, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - wersja artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="67b5c-223">Kliknij, aby skonfigurować wyzwalacz wersji **wyzwalaczy** i wybierz **ciągłe wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-223">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="67b5c-224">W tym samym źródle artefaktu, należy ustawić wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="67b5c-224">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="67b5c-225">To ustawienie zapewnia, że rozpoczyna się nowej wersji, gdy kompilacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="67b5c-225">This setting ensures that a new release starts when the build completes successfully.</span></span>

    ![Visual Studio Team Services — wyzwalaczy zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="67b5c-227">Kliknij, aby skonfigurować zmienne wersji **zmienne** i wybierz **+ zmiennej** utworzyć trzy nowe zmienne z użyciem informacji rejestru: **docker.username**, **docker.password**, i **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="67b5c-227">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="67b5c-228">Wklej wartości rejestru i DNS agentów klastra.</span><span class="sxs-lookup"><span data-stu-id="67b5c-228">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="67b5c-230">Jak pokazano na poprzednich ekranu, kliknij przycisk **blokady** checkbox w docker.password.</span><span class="sxs-lookup"><span data-stu-id="67b5c-230">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="67b5c-231">To ustawienie jest ważne ograniczyć hasło.</span><span class="sxs-lookup"><span data-stu-id="67b5c-231">This setting is important to restrict the password.</span></span>
    >

### <a name="define-the-release-workflow"></a><span data-ttu-id="67b5c-232">Definiowanie wersji przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="67b5c-232">Define the release workflow</span></span>

<span data-ttu-id="67b5c-233">Wersja przepływ pracy składa się z dwóch zadań, które można dodać.</span><span class="sxs-lookup"><span data-stu-id="67b5c-233">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="67b5c-234">Skonfigurować zadania bezpiecznie skopiować plik Redaguj *wdrażanie* folder w rozwiązaniu Docker Swarm węzła głównego, przy użyciu połączenia SSH został wcześniej skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="67b5c-234">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="67b5c-235">Zobacz następujący ekran, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="67b5c-235">See the following screen for details.</span></span>
    
    <span data-ttu-id="67b5c-236">Folder źródłowy:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="67b5c-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - wersja punkt połączenia usługi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="67b5c-238">Skonfiguruj drugi zadań do wykonania polecenia bash, aby uruchomić `docker` i `docker stack deploy` poleceń w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="67b5c-238">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span></span> <span data-ttu-id="67b5c-239">Zobacz następujący ekran, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="67b5c-239">See the following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services — Bash zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="67b5c-241">Polecenie wykonane na wzorcu używa interfejsu wiersza polecenia Docker i interfejsu wiersza polecenia rozwiązania Docker Compose do wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="67b5c-241">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="67b5c-242">Zaloguj się do rejestru kontenera platformy Azure (używa trzech zmiennych kompilacji, które są zdefiniowane w **zmienne** kartę)</span><span class="sxs-lookup"><span data-stu-id="67b5c-242">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="67b5c-243">Zdefiniuj **DOCKER_HOST** zmienną do pracy z punktu końcowego Swarm (: 2375)</span><span class="sxs-lookup"><span data-stu-id="67b5c-243">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="67b5c-244">Przejdź do *wdrażanie* folderu, który został utworzony przez poprzednie zadanie kopiowania bezpiecznego i który zawiera plik docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="67b5c-244">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="67b5c-245">Wykonanie `docker stack deploy` poleceń ściągnięcia nowych obrazów i utworzyć kontenerów.</span><span class="sxs-lookup"><span data-stu-id="67b5c-245">Execute `docker stack deploy` commands that pull the new images and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="67b5c-246">Jak pokazano na poprzednich ekranu, pozostaw **zakończyć się niepowodzeniem ze strumienia STDERR** niezaznaczone pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="67b5c-246">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="67b5c-247">To ustawienie umożliwia firmie Microsoft w celu ukończenia procesu wersji ze względu na `docker-compose` wyświetla komunikaty diagnostyczne, takie jak kontenery są zatrzymywanie lub usuwane, dane wyjściowe błędów.</span><span class="sxs-lookup"><span data-stu-id="67b5c-247">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="67b5c-248">Jeśli pole wyboru Visual Studio Team Services raporty błędów, które wystąpiły podczas wersji, nawet jeśli wszystko przebiegnie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="67b5c-248">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="67b5c-249">Zapisz ten nowej definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="67b5c-249">Save this new release definition.</span></span>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="67b5c-250">Krok 4: Testowanie potoku CI/CD</span><span class="sxs-lookup"><span data-stu-id="67b5c-250">Step 4: Test the CI/CD pipeline</span></span>

<span data-ttu-id="67b5c-251">Teraz, po zakończeniu konfiguracji, nadszedł czas na test ten nowy potok CI/CD.</span><span class="sxs-lookup"><span data-stu-id="67b5c-251">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="67b5c-252">Najprostszym sposobem, aby ją przetestować jest zaktualizuj kod źródłowy i zatwierdzić zmiany do repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="67b5c-252">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="67b5c-253">Kilka sekund po naciśnięciu kodu, zobaczysz nowej kompilacji uruchomionych w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="67b5c-253">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="67b5c-254">Po pomyślnym ukończeniu nowej wersji wyzwoleniu i wdrożeniu nowej wersji aplikacji w klastrze usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67b5c-254">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b5c-255">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67b5c-255">Next steps</span></span>

* <span data-ttu-id="67b5c-256">Aby uzyskać więcej informacji na temat CI/CD z Visual Studio Team Services, zobacz [kompilacji programu VSTS omówienie](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="67b5c-256">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="67b5c-257">Aby uzyskać więcej informacji na temat aparatu ACS, zobacz [repozytorium GitHub aparat ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="67b5c-257">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="67b5c-258">Aby uzyskać więcej informacji o trybie Docker Swarm, zobacz [Docker Swarm Omówienie trybu](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="67b5c-258">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
