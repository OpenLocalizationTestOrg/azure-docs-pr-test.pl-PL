---
title: "aaaCI/CD z usługą kontenera Azure i Swarm | Dokumentacja firmy Microsoft"
description: "Użyj usługi kontenera platformy Azure z toodeliver stale aplikacji .NET Core wielu kontenera Docker Swarm, rejestru kontenera Azure i Visual Studio Team Services"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Swarm, Azure, programu Visual Studio Team Services, opracowywania oprogramowania"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="a465a-104">Pełna CI/CD toodeploy potoku aplikacji usługi kontenera w usłudze kontenera platformy Azure przy użyciu rozwiązania Docker Swarm przy użyciu programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a465a-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="a465a-105">Jeden z hello największych wyzwań po opracowywanie nowoczesnych aplikacji w chmurze hello jest możliwe toodeliver te aplikacje stale.</span><span class="sxs-lookup"><span data-stu-id="a465a-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="a465a-106">W tym artykule Dowiedz się, jak zbudować tooimplement pełnej ciągłej integracji i wdrażania (CI/CD) potoku Docker Swarm, rejestru kontenera Azure i Visual Studio Team Services za pomocą usługi kontenera platformy Azure i zarządzania zleceniami.</span><span class="sxs-lookup"><span data-stu-id="a465a-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="a465a-107">Ten artykuł jest oparty na prostej aplikacji, dostępnych na [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), rozwinięte z platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a465a-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="a465a-108">Aplikacja Hello składa się z czterech różnych usług: trzy sieci web, interfejsów API i frontonu sieci web co:</span><span class="sxs-lookup"><span data-stu-id="a465a-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="a465a-110">cel Hello jest toodeliver tej aplikacji stale w klastrze Docker Swarm, za pomocą programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a465a-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="a465a-111">następujące Hello rysunek szczegóły tego potoku ciągłego dostarczania:</span><span class="sxs-lookup"><span data-stu-id="a465a-111">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="a465a-113">Poniżej przedstawiono krótki opis kroków hello:</span><span class="sxs-lookup"><span data-stu-id="a465a-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="a465a-114">Zmiany kodu są repozytorium kodu źródłowego zatwierdzone toohello (tutaj GitHub)</span><span class="sxs-lookup"><span data-stu-id="a465a-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="a465a-115">GitHub uaktywnia kompilację w Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a465a-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="a465a-116">Visual Studio Team Services pobiera najnowsza wersja źródła hello hello i tworzy wszystkie obrazy hello tworzące aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a465a-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="a465a-117">Visual Studio Team Services wypchnięcia każdego obrazu tooa Docker rejestru utworzone za pomocą usługi Azure kontenera rejestru hello</span><span class="sxs-lookup"><span data-stu-id="a465a-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="a465a-118">Visual Studio Team Services wyzwala nową wersją</span><span class="sxs-lookup"><span data-stu-id="a465a-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="a465a-119">Niektóre polecenia przy użyciu protokołu SSH w węźle głównym klastra usługi kontenera platformy Azure hello uruchamia Hello zlecenia</span><span class="sxs-lookup"><span data-stu-id="a465a-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="a465a-120">Rozwiązanie docker Swarm hello klastra ściąga hello najnowszą wersją hello obrazów</span><span class="sxs-lookup"><span data-stu-id="a465a-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="a465a-121">nową wersję aplikacji hello Hello wdrażania przy użyciu rozwiązania Docker Compose</span><span class="sxs-lookup"><span data-stu-id="a465a-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a465a-122">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a465a-122">Prerequisites</span></span>

<span data-ttu-id="a465a-123">Przed rozpoczęciem tego samouczka potrzebne hello toocomplete następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a465a-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="a465a-124">Utworzenie klastra Swarm usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a465a-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="a465a-125">Połącz z klastrem Swarm hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a465a-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="a465a-126">Tworzenie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a465a-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="a465a-127">Utworzony projekt konta i zespołu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a465a-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="a465a-128">Rozwidlania tooyour repozytorium GitHub hello konto GitHub</span><span class="sxs-lookup"><span data-stu-id="a465a-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="a465a-129">Należy również maszyny Ubuntu (14.04 i 16.04) z Docker zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="a465a-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="a465a-130">Ten komputer jest używany przez Visual Studio Team Services podczas hello kompilacji i wydania procesów.</span><span class="sxs-lookup"><span data-stu-id="a465a-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="a465a-131">Jednym ze sposobów toocreate ten komputer jest dostępna w hello obraz powitania toouse [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="a465a-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="a465a-132">Krok 1: Skonfiguruj konto usługi Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a465a-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="a465a-133">W tej sekcji należy skonfigurować konto w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a465a-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="a465a-134">Konfigurowanie agenta kompilacji programu Visual Studio Team Services Linux</span><span class="sxs-lookup"><span data-stu-id="a465a-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="a465a-135">obrazy usługi Docker toocreate i wypychania tworzenia tych obrazów w rejestrze kontenera platformy Azure z Visual Studio Team Services, należy tooregister agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a465a-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="a465a-136">Masz następujące opcje instalacji:</span><span class="sxs-lookup"><span data-stu-id="a465a-136">You have these installation options:</span></span>

* [<span data-ttu-id="a465a-137">Wdrażanie agenta w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="a465a-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="a465a-138">Użyj agenta programu VSTS hello toorun Docker</span><span class="sxs-lookup"><span data-stu-id="a465a-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="a465a-139">Zainstaluj rozszerzenie VSTS integracji Docker hello</span><span class="sxs-lookup"><span data-stu-id="a465a-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="a465a-140">Firma Microsoft udostępnia usługi VSTS rozszerzenia toowork z rozwiązaniem Docker z kompilacji i wydania procesów.</span><span class="sxs-lookup"><span data-stu-id="a465a-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="a465a-141">To rozszerzenie jest dostępna w hello [Marketplace programu VSTS](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="a465a-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="a465a-142">Kliknij przycisk **zainstalować** tooadd tego konta usługi VSTS tooyour rozszerzenia:</span><span class="sxs-lookup"><span data-stu-id="a465a-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Zainstaluj hello Integracja z rozwiązaniem Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="a465a-144">Zostanie wyświetlona prośba konta usługi VSTS tooyour tooconnect przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a465a-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="a465a-145">Połączenie usługi Visual Studio Team Services i GitHub</span><span class="sxs-lookup"><span data-stu-id="a465a-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="a465a-146">Skonfiguruj połączenie między projektu programu VSTS oraz konto GitHub.</span><span class="sxs-lookup"><span data-stu-id="a465a-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="a465a-147">W projekcie programu Visual Studio Team Services, kliknij przycisk hello **ustawienia** ikonę w hello narzędzi i wybierz **usług**.</span><span class="sxs-lookup"><span data-stu-id="a465a-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services — połączenie zewnętrzne](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="a465a-149">Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="a465a-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services — usługi GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="a465a-151">Kliknij tooauthorize toowork programu VSTS z Twoim kontem usługi GitHub **autoryzacji** i wykonaj procedurę hello w otwartym oknie hello.</span><span class="sxs-lookup"><span data-stu-id="a465a-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services — autoryzować GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="a465a-153">Połącz rejestru programu VSTS tooyour kontenera platformy Azure i klastrem usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a465a-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="a465a-154">ostatnie etapy Hello przed przejściem do potoku CI/CD hello są tooconfigure połączeń zewnętrznych tooyour kontenera rejestru i klastrem Docker Swarm w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="a465a-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="a465a-155">W hello **usług** ustawień projektu Visual Studio Team Services, Dodaj punkt końcowy usługi typu **Docker rejestru**.</span><span class="sxs-lookup"><span data-stu-id="a465a-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="a465a-156">W menu podręcznym hello, który zostanie otwarty wprowadź adres URL hello i poświadczenia hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a465a-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services — Docker rejestru](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="a465a-158">Klaster Docker Swarm hello Dodawanie punktu końcowego typu **SSH**.</span><span class="sxs-lookup"><span data-stu-id="a465a-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="a465a-159">Następnie wprowadź informacje o połączeniu SSH hello klastra Swarm.</span><span class="sxs-lookup"><span data-stu-id="a465a-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="a465a-161">Cała konfiguracja hello odbywa się teraz.</span><span class="sxs-lookup"><span data-stu-id="a465a-161">All hello configuration is done now.</span></span> <span data-ttu-id="a465a-162">W następnych krokach hello możesz utworzyć hello CI/CD potok, który tworzy i wdraża klaster Docker Swarm toohello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a465a-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="a465a-163">Krok 2: Tworzenie definicji kompilacji hello</span><span class="sxs-lookup"><span data-stu-id="a465a-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="a465a-164">W tym kroku konfiguracji definitionfor kompilacji projektu programu VSTS i zdefiniuj hello przepływu pracy kompilacji dla obrazów kontenera</span><span class="sxs-lookup"><span data-stu-id="a465a-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="a465a-165">Definicja początkowej instalacji</span><span class="sxs-lookup"><span data-stu-id="a465a-165">Initial definition setup</span></span>

1. <span data-ttu-id="a465a-166">tooyour projektu Visual Studio Team Services i kliknij przycisk Połącz toocreate definicję kompilacji **kompilacji i wydania**.</span><span class="sxs-lookup"><span data-stu-id="a465a-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="a465a-167">W hello **definicje kompilacji** kliknij **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="a465a-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="a465a-168">Wybierz hello **pusty** szablonu.</span><span class="sxs-lookup"><span data-stu-id="a465a-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services — nowej definicji kompilacji](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="a465a-170">Skonfiguruj nową kompilację hello ze źródłem repozytorium GitHub wyboru **ciągłej integracji**i wybierz hello kolejki agenta rejestracji agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a465a-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="a465a-171">Kliknij przycisk **Utwórz** toocreate hello definicji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a465a-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services — Tworzenie definicji kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="a465a-173">Na powitania **definicji kompilacji** strony, należy najpierw otworzyć hello **repozytorium** i skonfiguruj hello kompilacji toouse hello rozwidlenia hello MyShop projektu, który został utworzony w hello wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="a465a-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="a465a-174">Upewnij się, że wybrano *acs docs* jako hello **gałąź domyślną**.</span><span class="sxs-lookup"><span data-stu-id="a465a-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="a465a-176">Na powitania **wyzwalaczy** skonfiguruj toobe kompilacji hello wyzwalane po każdym zatwierdzeniu.</span><span class="sxs-lookup"><span data-stu-id="a465a-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="a465a-177">Wybierz **ciągłej integracji** i **partii zmian**.</span><span class="sxs-lookup"><span data-stu-id="a465a-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services — Konfiguracja wyzwalacza kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="a465a-179">Zdefiniuj hello przepływu pracy kompilacji</span><span class="sxs-lookup"><span data-stu-id="a465a-179">Define hello build workflow</span></span>
<span data-ttu-id="a465a-180">Następne kroki Hello zdefiniuj hello przepływu pracy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a465a-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="a465a-181">Istnieje pięć toobuild obrazów kontener dla hello *MyShop* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a465a-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="a465a-182">Obraz jest utworzony przy użyciu powitalne plik Dockerfile znajdujących się w folderach projektu hello:</span><span class="sxs-lookup"><span data-stu-id="a465a-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="a465a-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="a465a-183">ProductsApi</span></span>
* <span data-ttu-id="a465a-184">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="a465a-184">Proxy</span></span>
* <span data-ttu-id="a465a-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="a465a-185">RatingsApi</span></span>
* <span data-ttu-id="a465a-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="a465a-186">RecommandationsApi</span></span>
* <span data-ttu-id="a465a-187">Sklepu</span><span class="sxs-lookup"><span data-stu-id="a465a-187">ShopFront</span></span>

<span data-ttu-id="a465a-188">Należy tooadd dwa kroki Docker dla każdego obrazu, jeden obraz powitania toobuild i jeden obraz powitania toopush hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a465a-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="a465a-189">tooadd etapem hello przepływu pracy kompilacji, kliknij przycisk **+ Dodaj krok kompilacji** i wybierz **Docker**.</span><span class="sxs-lookup"><span data-stu-id="a465a-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services — dodać kroki procesu kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="a465a-191">Dla każdego obrazu, należy skonfigurować jeden krok, który używa hello `docker build` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a465a-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services — Docker kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="a465a-193">Na powitania utworzyć operację, wybierz rejestru kontenera platformy Azure, hello **kompilacji obrazu** akcji i hello plik Dockerfile, który definiuje każdego obrazu.</span><span class="sxs-lookup"><span data-stu-id="a465a-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="a465a-194">Zestaw hello **kontekst kompilacji** hello plik Dockerfile katalogu głównego, a także definiują hello **nazwa obrazu**.</span><span class="sxs-lookup"><span data-stu-id="a465a-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="a465a-195">Jak pokazano na powitania ekranu poprzedzającym, zaczynać się nazwa obrazu hello hello URI rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a465a-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="a465a-196">(Możesz również użyć kompilacji zmiennej tooparameterize hello tag obrazu hello, takich jak identyfikator kompilacji hello w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="a465a-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="a465a-197">Dla każdego obrazu, skonfiguruj drugi krok, który używa hello `docker push` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a465a-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services — Docker Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="a465a-199">Dla operacji wypychania hello, wybierz rejestru kontenera platformy Azure, hello **Push obrazu** akcji, a następnie wprowadź hello **nazwa obrazu** wbudowane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="a465a-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="a465a-200">Po skonfigurowaniu hello kompilacji i push kroki dla każdego z pięciu obrazów hello, dodaj dwa kroki więcej w hello kompilacji przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="a465a-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="a465a-201">a.</span><span class="sxs-lookup"><span data-stu-id="a465a-201">a.</span></span> <span data-ttu-id="a465a-202">Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *BuildNumber* wystąpienie w pliku docker-compose.yml hello hello bieżącej kompilacji identyfikatora. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a465a-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services — plik Redaguj aktualizacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="a465a-204">b.</span><span class="sxs-lookup"><span data-stu-id="a465a-204">b.</span></span> <span data-ttu-id="a465a-205">Zadanie porzuca hello aktualizowana tworzenia pliku jako artefaktów kompilacji dzięki mogą być używane w hello wersji.</span><span class="sxs-lookup"><span data-stu-id="a465a-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="a465a-206">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a465a-206">See hello following screen for details.</span></span>

    ![Usługi Visual Studio Team - publikowania tworzenia pliku](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="a465a-208">Kliknij przycisk **zapisać** i nazwij definicję kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a465a-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="a465a-209">Krok 3: Tworzenie definicji wersji hello</span><span class="sxs-lookup"><span data-stu-id="a465a-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="a465a-210">Visual Studio Team Services służy za[zarządzania wersjami w środowiskach](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="a465a-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="a465a-211">Można włączyć się, że aplikacja jest wdrożony na Twoje różnych środowiskach (np. dev, test produkcji wstępnej i produkcji) w sposób toomake ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a465a-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="a465a-212">Można utworzyć nowego środowiska reprezentujący klastra Azure kontenera usługi Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a465a-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services — tooACS zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="a465a-214">Początkowa wersja Instalatora</span><span class="sxs-lookup"><span data-stu-id="a465a-214">Initial release setup</span></span>

1. <span data-ttu-id="a465a-215">toocreate definicji wersji, kliknij przycisk **wersje** > **+ zlecenia**</span><span class="sxs-lookup"><span data-stu-id="a465a-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="a465a-216">tooconfigure hello artefaktu źródłowego, kliknij przycisk **artefakty** > **połączenia źródła artefaktu**.</span><span class="sxs-lookup"><span data-stu-id="a465a-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="a465a-217">W tym miejscu łącze nowej wersji definicji toohello kompilacji zdefiniowanego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="a465a-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="a465a-218">Dzięki temu plik docker-compose.yml hello jest dostępna w hello procesu publikacji.</span><span class="sxs-lookup"><span data-stu-id="a465a-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - wersja artefaktów](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="a465a-220">wyzwalacz wersji hello tooconfigure, kliknij przycisk **wyzwalaczy** i wybierz **ciągłe wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="a465a-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="a465a-221">Zestaw wyzwalacza hello na powitania tego samego źródła artefaktu.</span><span class="sxs-lookup"><span data-stu-id="a465a-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="a465a-222">To ustawienie zapewni, jak hello kompilacja zostaje ukończona pomyślnie rozpoczyna się nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="a465a-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services — wyzwalaczy zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="a465a-224">Zdefiniuj hello wersji w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="a465a-224">Define hello release workflow</span></span>

<span data-ttu-id="a465a-225">przepływ pracy wersji Hello składa się z dwóch zadań, które można dodać.</span><span class="sxs-lookup"><span data-stu-id="a465a-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="a465a-226">Konfigurowanie zadań toosecurely kopiowania hello utworzenie pliku tooa *wdrażania* folderu na powitania Docker Swarm węzła głównego, przy użyciu połączenia SSH hello został wcześniej skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="a465a-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="a465a-227">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a465a-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - wersja punkt połączenia usługi](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="a465a-229">Skonfiguruj drugi tooexecute zadań toorun polecenia bash `docker` i `docker-compose` poleceń na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="a465a-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="a465a-230">Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a465a-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services — Bash zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="a465a-232">polecenie Hello wykonane na powitania hello wzorca użycia interfejsu wiersza polecenia Docker i hello toodo rozwiązania Docker Compose CLI hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a465a-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="a465a-233">Logowania toohello kontenera platformy Azure rejestru (używa trzech variab'les kompilacji, które są zdefiniowane w hello **zmienne** kartę)</span><span class="sxs-lookup"><span data-stu-id="a465a-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="a465a-234">Zdefiniuj hello **DOCKER_HOST** toowork zmiennej z punktu końcowego Swarm hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="a465a-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="a465a-235">Przejdź toohello *wdrażanie* folderu, który został utworzony przez hello poprzedzających zadanie kopiowania bezpiecznego i który zawiera plik docker-compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="a465a-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="a465a-236">Wykonanie `docker-compose` poleceń ściągnięcia nowych obrazów hello, Zatrzymaj usługi hello, Usuń usługi hello i utworzyć hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="a465a-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="a465a-237">Jak pokazano na powitania ekranu poprzedzającym, pozostaw hello **zakończyć się niepowodzeniem ze strumienia STDERR** niezaznaczone pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="a465a-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="a465a-238">To ustawienie ważne, ponieważ `docker-compose` wyświetla komunikaty diagnostyczne, takie jak kontenery są zatrzymywanie lub usuwany na powitania błędów w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a465a-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="a465a-239">Po zaznaczeniu pola wyboru hello Visual Studio Team Services raporty błędów, które wystąpiły podczas wersji hello, nawet jeśli wszystko przebiegnie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="a465a-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="a465a-240">Zapisz ten nowej definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="a465a-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="a465a-241">Tego wdrożenia zawiera pewien Przestój, ponieważ jesteśmy zatrzymywanie usług starego hello i systemem hello nową.</span><span class="sxs-lookup"><span data-stu-id="a465a-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="a465a-242">Jego jest to możliwe tooavoid wykonując wdrożenie zielony niebieski.</span><span class="sxs-lookup"><span data-stu-id="a465a-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="a465a-243">Krok 4.</span><span class="sxs-lookup"><span data-stu-id="a465a-243">Step 4.</span></span> <span data-ttu-id="a465a-244">Test hello CI/CD potoku</span><span class="sxs-lookup"><span data-stu-id="a465a-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="a465a-245">Teraz, po zakończeniu konfiguracji hello, jest czas tootest nowy potok CI/CD.</span><span class="sxs-lookup"><span data-stu-id="a465a-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="a465a-246">Hello Najprostszym sposobem tootest jest tooupdate hello źródła kodu i zatwierdzania hello zmienia się w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a465a-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="a465a-247">Kilka sekund po wypchnąć kod hello, zobaczysz nowej kompilacji uruchomionych w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a465a-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="a465a-248">Po pomyślnym ukończeniu nowej wersji zostanie wywołane i wdroży hello nowej wersji aplikacji hello na powitania klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a465a-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a465a-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a465a-249">Next Steps</span></span>

* <span data-ttu-id="a465a-250">Aby uzyskać więcej informacji na temat CI/CD z Visual Studio Team Services, zobacz hello [kompilacji programu VSTS omówienie](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="a465a-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
