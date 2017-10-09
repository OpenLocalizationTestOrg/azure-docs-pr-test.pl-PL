---
title: "aaaCI/CD z Wpięć tooAzure maszyn wirtualnych o Team Services | Dokumentacja firmy Microsoft"
description: "Konfigurowanie ciągłej integracji (CI), jak i ciągłe wdrażanie (CD) aplikacji Node.js przy użyciu maszyn wirtualnych tooAzure Wpięć z zarządzania zleceniami w programie Visual Studio Team Services (VSTS) lub programu Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="d642f-103">Wdrażanie Twojej aplikacji tooLinux maszyn wirtualnych przy użyciu Wpięć i usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="d642f-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="d642f-104">Ciągłej integracji (CI), jak i ciągłe wdrażanie (CD) jest potoku, za pomocą którego można kompilacji, wersji i wdrażanie kodu.</span><span class="sxs-lookup"><span data-stu-id="d642f-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="d642f-105">Usługi Team Services zapewnia pełną, kompletny zestaw narzędzi automatyzacji CI/CD dla tooAzure wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d642f-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="d642f-106">Wpięć to popularnych 3rd firm CI/CD serwerowych narzędzie, które udostępnia również automatyzacji CI/CD.</span><span class="sxs-lookup"><span data-stu-id="d642f-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="d642f-107">Można użyć obu razem toocustomize sposób dostarczania Twojej aplikacji w chmurze lub usługi.</span><span class="sxs-lookup"><span data-stu-id="d642f-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="d642f-108">W tym samouczku, użyj toobuild Wpięć **aplikacji sieci web Node.js**i Visual Studio Team Services toodeploy on tooa [grupę wdrożenia](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) zawierających maszyny wirtualne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="d642f-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="d642f-109">Wykonasz następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d642f-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d642f-110">Tworzenie aplikacji w Wpięć</span><span class="sxs-lookup"><span data-stu-id="d642f-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="d642f-111">Skonfiguruj Wpięć integracji usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="d642f-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="d642f-112">Utwórz grupę wdrożenia dla hello maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d642f-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="d642f-113">Tworzenie definicji wersji, która konfiguruje hello maszyn wirtualnych i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d642f-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d642f-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d642f-114">Before you begin</span></span>

* <span data-ttu-id="d642f-115">Musisz mieć konto Wpięć tooa dostępu.</span><span class="sxs-lookup"><span data-stu-id="d642f-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="d642f-116">Jeśli jeszcze nie utworzono serwera Wpięć, zobacz [dokumentacji Wpięć](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="d642f-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="d642f-117">Zaloguj się tooyour konta usługi Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="d642f-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="d642f-118">Możesz uzyskać [bezpłatnego konta usługi Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="d642f-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="d642f-119">Aby uzyskać więcej informacji, zobacz [połączenia usług tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="d642f-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="d642f-120">Utwórz osobisty token dostępu (PAWEŁ) w ramach konta usługi Team Services, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d642f-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="d642f-121">Wpięć wymaga tego tooaccess informacji konta usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="d642f-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="d642f-122">Odczyt [jak utworzyć osobisty token dostępu dla usługi Team Services i TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn jak toogenerate jeden.</span><span class="sxs-lookup"><span data-stu-id="d642f-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="d642f-123">Pobierz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d642f-123">Get hello sample app</span></span>

<span data-ttu-id="d642f-124">Należy toodeploy aplikacji przechowywanych w repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="d642f-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="d642f-125">W tym samouczku, zalecane jest użycie [tej przykładowej aplikacji dostępne w serwisie GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="d642f-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="d642f-126">Utwórz rozwidlenia tej aplikacji i zanotuj lokalizację hello (URL) do użycia w kolejnych krokach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d642f-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="d642f-127">Wprowadź rozwidlenia hello **publicznego** toosimplify tooGitHub połączyć się później.</span><span class="sxs-lookup"><span data-stu-id="d642f-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="d642f-128">Aby uzyskać więcej informacji, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/) i [ujawnianie prywatnym repozytorium](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="d642f-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="d642f-129">Aplikacja Hello został zbudowany przy użyciu [narzędzia Yeoman](http://yeoman.io/learning/index.html); używa **Express**, **bower**, i **grunt**; i zawiera niektóre **npm**pakietów jako zależności.</span><span class="sxs-lookup"><span data-stu-id="d642f-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="d642f-130">Witaj przykładowej aplikacji zawiera zestaw [szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) , są używane toodynamically utworzyć hello maszyn wirtualnych do wdrożenia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d642f-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="d642f-131">Te szablony są używane przez zadania w hello [Team Services wersji definicji](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="d642f-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="d642f-132">Szablon głównego Hello tworzy sieciową grupę zabezpieczeń, maszyny wirtualnej i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d642f-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="d642f-133">Przypisuje publicznego adresu IP, a otwiera przychodzący port 80.</span><span class="sxs-lookup"><span data-stu-id="d642f-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="d642f-134">Dodaje tag, który jest używany przez wdrożenie hello tooreceive maszyny zbyt wybierz hello hello wdrożenia grupy.</span><span class="sxs-lookup"><span data-stu-id="d642f-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="d642f-135">przykład Witaj zawiera także skrypt, który konfiguruje Nginx i wdraża aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="d642f-136">Wykonaniem na każdym hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d642f-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="d642f-137">W szczególności skryptu hello instaluje węzła, Nginx i PM2; Konfiguruje Nginx i PM2; następnie uruchamia hello węzła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d642f-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="d642f-138">Skonfiguruj Wpięć wtyczek</span><span class="sxs-lookup"><span data-stu-id="d642f-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="d642f-139">Najpierw należy skonfigurować dwa wtyczek Wpięć dla **NodeJS** i **integracji z usługami zespołu**.</span><span class="sxs-lookup"><span data-stu-id="d642f-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="d642f-140">Otwórz konta Wpięć i wybierz polecenie **Zarządzanie Wpięć**.</span><span class="sxs-lookup"><span data-stu-id="d642f-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="d642f-141">W hello **Zarządzanie Wpięć** wybierz pozycję **Zarządzanie wtyczkami**.</span><span class="sxs-lookup"><span data-stu-id="d642f-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="d642f-142">Filtr hello listy toolocate hello **NodeJS** wtyczki i zainstaluj go bez ponownego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="d642f-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Dodawanie hello NodeJS wtyczki tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="d642f-144">Filtr hello listy toofind hello **Team Foundation Server** wtyczki i zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="d642f-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="d642f-145">(Ta wtyczka dotyczy Team Foundation Server i usługi Team Services.) Ponowne uruchamianie Wpięć nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="d642f-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="d642f-146">Konfigurowanie kompilowania Wpięć dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="d642f-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="d642f-147">W Wpięć Utwórz nowy projekt kompilacji i skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d642f-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="d642f-148">W hello **ogólne** wprowadź nazwę dla projektu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d642f-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="d642f-149">W hello **zarządzania kodem źródłowym** wybierz opcję **Git** , a następnie wprowadź szczegóły hello hello repozytorium i gałęzi hello zawierający kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d642f-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Dodaj kompilacji tooyour repozytorium](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="d642f-151">Jeśli repozytorium nie jest publiczny, wybierz **Dodaj** i podaj poświadczenia tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="d642f-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="d642f-152">W hello **kompilacji wyzwalaczy** wybierz opcję **SCM sondowania** , a następnie wprowadź harmonogram hello `H/03 * * * *` repozytorium Git hello toopoll zmiany co trzy minuty.</span><span class="sxs-lookup"><span data-stu-id="d642f-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="d642f-153">W hello **Build Environment** wybierz opcję **Podaj węzła &amp; npm bin / ŚCIEŻKĘ folderu** , a następnie wprowadź `NodeJS` dla hello wartość Node JS instalacji.</span><span class="sxs-lookup"><span data-stu-id="d642f-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="d642f-154">Pozostaw **pliku npmrc** ustawioną wartość "Użyj domyślnej system."</span><span class="sxs-lookup"><span data-stu-id="d642f-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="d642f-155">W hello **kompilacji** wprowadź polecenie hello `npm install` tooensure wszystkie zależności są aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="d642f-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="d642f-156">Skonfiguruj Wpięć integracji usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="d642f-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="d642f-157">W hello **akcje postkompilacyjnego** karcie dla **tooarchive pliki**, wprowadź `**/*` tooinclude wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="d642f-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="d642f-158">Dla **wyzwalanie wydania w TFS/Team Services**, wprowadź pełny adres URL hello konta (takie jak `https://your-account-name.visualstudio.com`), hello nazwę projektu, nazwę definicji wersji hello (utworzone później), i hello poświadczenia tooconnect tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="d642f-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="d642f-159">Należy swoją nazwę użytkownika i hello PAWEŁ utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d642f-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Konfigurowanie Wpięć działania mające miejsce po kompilacji](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="d642f-161">Zapisz hello kompilacji projektu.</span><span class="sxs-lookup"><span data-stu-id="d642f-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="d642f-162">Tworzenie punktu końcowego usługi Wpięć</span><span class="sxs-lookup"><span data-stu-id="d642f-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="d642f-163">Punkt końcowy usługi umożliwia tooJenkins tooconnect Team Services.</span><span class="sxs-lookup"><span data-stu-id="d642f-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="d642f-164">Otwórz hello **usług** strony w Team Services, otwórz hello **nowy punkt końcowy usługi** listy, a następnie wybierz pozycję **Wpięć**.</span><span class="sxs-lookup"><span data-stu-id="d642f-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Dodawanie punktu końcowego Wpięć](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="d642f-166">Wprowadź nazwę użyje toorefer toothis połączenia.</span><span class="sxs-lookup"><span data-stu-id="d642f-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="d642f-167">Wprowadź adres URL powitania serwera Wpięć i znaczników hello **zaakceptować niezaufane certyfikaty protokołu SSL** opcji.</span><span class="sxs-lookup"><span data-stu-id="d642f-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="d642f-168">Wprowadź hello nazwę użytkownika i hasło do konta Wpięć.</span><span class="sxs-lookup"><span data-stu-id="d642f-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="d642f-169">Wybierz **sprawdzić połączenie** toocheck, który hello informacje są poprawne.</span><span class="sxs-lookup"><span data-stu-id="d642f-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="d642f-170">Wybierz **OK** punktu końcowego usługi hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d642f-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="d642f-171">Utwórz grupę wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d642f-171">Create a deployment group</span></span>

<span data-ttu-id="d642f-172">Należy [grupę wdrożenia](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) zbyt zawierają hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d642f-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="d642f-173">Otwórz hello **wersje** kartę hello **kompilacji &amp; wersji** koncentratora, a następnie otwórz hello **grupy wdrożenia** , a następnie wybierz **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="d642f-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="d642f-174">Wprowadź nazwę grupy wdrożenia hello i opcjonalny opis.</span><span class="sxs-lookup"><span data-stu-id="d642f-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="d642f-175">Następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d642f-175">Then choose **Create**.</span></span>

<span data-ttu-id="d642f-176">Zadanie wdrażania grupy zasobów Azure Hello tworzy i rejestruje hello maszyn wirtualnych, gdy jest uruchamiany przy użyciu szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="d642f-177">Nie należy toocreate i samodzielnie zarejestrować hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d642f-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="d642f-178">Utwórz definicję zlecenia</span><span class="sxs-lookup"><span data-stu-id="d642f-178">Create a release definition</span></span>

<span data-ttu-id="d642f-179">Proces hello Team Services będą wykonywane aplikacji hello toodeploy określa definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="d642f-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="d642f-180">toocreate hello wersji definicji w Team Services:</span><span class="sxs-lookup"><span data-stu-id="d642f-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="d642f-181">Otwórz hello **wersje** kartę hello **kompilacji &amp; wersji** koncentratora, otwórz hello  **+**  listy rozwijanej liście hello definicji wersji, a następnie wybierz pozycję Witaj **Tworzenie wersji definicji**.</span><span class="sxs-lookup"><span data-stu-id="d642f-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="d642f-182">Wybierz hello **pusty** szablonu i wybierz polecenie **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d642f-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="d642f-183">W hello **artefakty** kliknij na **Link artefaktu** i wybierz polecenie **Wpięć**.</span><span class="sxs-lookup"><span data-stu-id="d642f-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="d642f-184">Wybierz połączenie Wpięć usługi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d642f-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="d642f-185">Następnie wybierz zadanie źródła Wpięć hello i wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d642f-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="d642f-186">W hello nowych definicji wersji, wybierz polecenie **+ Dodaj zadania** i Dodaj **wdrożenie grupy zasobów Azure** zadań toohello domyślnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="d642f-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="d642f-187">Wybierz hello listy rozwijanej strzałkę dalej toohello **+ Dodaj zadania** Dodaj definicję toohello fazy wdrożenia grupy i łącza.</span><span class="sxs-lookup"><span data-stu-id="d642f-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Dodawanie grupy faza wdrożenia](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="d642f-189">W katalogu zadania hello, otwórz hello **narzędzie** i Dodaj wystąpienia hello **skrypt powłoki** zadań.</span><span class="sxs-lookup"><span data-stu-id="d642f-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="d642f-190">Hello parametrów szablonu używanego w hello wdrożenie grupy zasobów Azure zadań ustawia hello admin hasło używane tooconnect toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d642f-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="d642f-191">Podaj hasło ze zmienną hello **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="d642f-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="d642f-192">Otwórz hello **zmienne** kartę, a w hello **zmienne** sekcji, wprowadź nazwę hello `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="d642f-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="d642f-193">Wprowadź hasło administratora hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="d642f-194">Wybierz hello "kłódki" ikona dalej toohello wartości tekstowe tooprotect hello hasło.</span><span class="sxs-lookup"><span data-stu-id="d642f-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="d642f-195">Zadanie wdrażania grupy zasobów Azure hello konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d642f-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="d642f-196">Witaj **wdrożenie grupy zasobów Azure** zadań jest używane toocreate hello wdrożenia grupy.</span><span class="sxs-lookup"><span data-stu-id="d642f-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="d642f-197">Skonfiguruj w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d642f-197">Configure it as follows:</span></span>

* <span data-ttu-id="d642f-198">**Subskrypcja platformy Azure:** wybierz połączenie z listy hello w obszarze **dostępne połączenia usługi Azure**.</span><span class="sxs-lookup"><span data-stu-id="d642f-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="d642f-199">Jeśli widoczne żadne połączenia, wybierz polecenie **Zarządzaj**, wybierz pozycję **nowy punkt końcowy usługi** następnie **usługi Azure Resource Manager**i postępuj zgodnie z monitami hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="d642f-200">Zwraca tooyour wersji definicji, hello odświeżania **AzureRM subskrypcji** listy i utworzone połączenie select hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="d642f-201">**Grupa zasobów**: Wprowadź nazwę grupy zasobów hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d642f-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="d642f-202">**Lokalizacja**: Wybierz region hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d642f-202">**Location**: Select a region for hello deployment.</span></span>

  ![Utworzenie nowej grupy zasobów](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="d642f-204">**Lokalizacja szablonów**:`URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="d642f-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="d642f-205">**Łącze szablonu**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="d642f-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="d642f-206">**Łącze parametrów szablonu**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="d642f-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="d642f-207">**Zastąp parametry szablonu**: Lista hello zastępowania wartości, na przykład: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="d642f-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="d642f-208">Wstaw wartości określonej dla hello {symbole zastępcze}.</span><span class="sxs-lookup"><span data-stu-id="d642f-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="d642f-209">**Wymagania wstępne włączyć**:`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="d642f-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="d642f-210">**Punkt końcowy TFS/VSTS**: Wybierz **Dodaj** , a następnie w oknie dialogowym "Dodaj nowe połączenie usługi Team Foundation Server/zespołu" hello, zaznacz **Token uwierzytelniania na podstawie**.</span><span class="sxs-lookup"><span data-stu-id="d642f-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="d642f-211">Wprowadź nazwę połączenia hello i adres URL hello projektu zespołowego.</span><span class="sxs-lookup"><span data-stu-id="d642f-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="d642f-212">Następnie generowanie i wprowadź [osobistych dostępu tokenu (PAWEŁ)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) projektu zespołowego tooyour tooauthenticate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="d642f-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Tworzenie osobistego tokenu dostępu](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="d642f-214">**Projekt zespołowy**: Wybierz bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="d642f-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="d642f-215">**Grupa wdrożenia**: Wprowadź hello tej samej nazwy grupy wdrożenia jako używaną na potrzeby hello **grupy zasobów** parametru.</span><span class="sxs-lookup"><span data-stu-id="d642f-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="d642f-216">ustawienia domyślne Hello hello zadania wdrażania grupy zasobów platformy Azure są toocreate lub tak przyrostowo aktualizować zasobu i toodo.</span><span class="sxs-lookup"><span data-stu-id="d642f-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="d642f-217">zadanie Hello tworzy Witaj Witaj maszyn wirtualnych po raz pierwszy uruchamia, a następnie wystarczy zaktualizować je.</span><span class="sxs-lookup"><span data-stu-id="d642f-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="d642f-218">Skonfiguruj zadania skryptu powłoki hello</span><span class="sxs-lookup"><span data-stu-id="d642f-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="d642f-219">Witaj **skrypt powłoki** zadań jest używane tooprovide Konfiguracja hello toorun skryptu, na każdy serwer tooinstall Node.js i rozpocząć hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d642f-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="d642f-220">Skonfiguruj w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d642f-220">Configure it as follows:</span></span>

* <span data-ttu-id="d642f-221">**Ścieżka skryptu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="d642f-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="d642f-222">**Określ pracy katalogu**:`Checked`</span><span class="sxs-lookup"><span data-stu-id="d642f-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="d642f-223">**Katalog roboczy**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="d642f-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="d642f-224">Zmień nazwę i zapisać hello wersji definicji</span><span class="sxs-lookup"><span data-stu-id="d642f-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="d642f-225">Edytuj nazwę hello hello wersji definicji toohello nazwy określone w **działania mające miejsce po kompilacji** kartę hello kompilacji w Wpięć.</span><span class="sxs-lookup"><span data-stu-id="d642f-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="d642f-226">Wpięć wymaga to nazwa toobe stanie tootrigger nową wersję, po zaktualizowaniu hello źródła artefaktów.</span><span class="sxs-lookup"><span data-stu-id="d642f-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="d642f-227">Opcjonalnie można zmienić nazwy hello hello środowiska, klikając nazwę hello.</span><span class="sxs-lookup"><span data-stu-id="d642f-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="d642f-228">Wybierz **zapisać**i wybierz polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="d642f-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="d642f-229">Rozpocznij wdrażanie ręczne</span><span class="sxs-lookup"><span data-stu-id="d642f-229">Start a manual deployment</span></span>

1. <span data-ttu-id="d642f-230">Wybierz **+ wersji** i wybierz **Tworzenie wersji**.</span><span class="sxs-lookup"><span data-stu-id="d642f-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="d642f-231">Zaznacz kompilacji hello ukończono hello wyróżnione listy rozwijanej i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d642f-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="d642f-232">Wybierz łącze wersji hello hello komunikatu podręcznego.</span><span class="sxs-lookup"><span data-stu-id="d642f-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="d642f-233">Na przykład: "wersji **wersji 1** został utworzony."</span><span class="sxs-lookup"><span data-stu-id="d642f-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="d642f-234">Otwórz hello **dzienniki** karcie toowatch hello wersji konsoli w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d642f-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="d642f-235">W przeglądarce otwórz adres URL hello jednego z serwerów hello dodana grupa wdrożenia tooyour.</span><span class="sxs-lookup"><span data-stu-id="d642f-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="d642f-236">Na przykład wprowadź`http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="d642f-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="d642f-237">Rozpocząć wdrażanie elementu konfiguracji/CD</span><span class="sxs-lookup"><span data-stu-id="d642f-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="d642f-238">W hello wersji definicji, usuń zaznaczenie pola wyboru hello **włączone** checkbox w hello **opcje sterowania** części ustawień hello hello zadania wdrażania grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d642f-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="d642f-239">Dla przyszłych wdrożeń toohello istniejącego wdrożenia grupy, nie trzeba toore — wykonanie tego zadania.</span><span class="sxs-lookup"><span data-stu-id="d642f-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="d642f-240">Przejdź do repozytorium Git źródła toohello i modyfikować zawartość hello hello **h1** pozycji w pliku hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="d642f-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="d642f-241">Zatwierdź zmiany.</span><span class="sxs-lookup"><span data-stu-id="d642f-241">Commit your change.</span></span>

1. <span data-ttu-id="d642f-242">Po kilku minutach, pojawi się nowe wydanie utworzone w hello **wersje** strona Team Services lub TFS.</span><span class="sxs-lookup"><span data-stu-id="d642f-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="d642f-243">Otwórz miejsce hello wersji toosee hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d642f-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="d642f-244">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="d642f-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d642f-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d642f-245">Next Steps</span></span>

<span data-ttu-id="d642f-246">Ten samouczek służy do automatycznego wdrożenia hello tooAzure aplikacji przy użyciu Wpięć kompilacji i usługi Team Services w wersji.</span><span class="sxs-lookup"><span data-stu-id="d642f-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="d642f-247">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="d642f-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d642f-248">Tworzenie aplikacji w Wpięć</span><span class="sxs-lookup"><span data-stu-id="d642f-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="d642f-249">Skonfiguruj Wpięć integracji usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="d642f-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="d642f-250">Utwórz grupę wdrożenia dla hello maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d642f-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="d642f-251">Tworzenie definicji wersji, która konfiguruje hello maszyn wirtualnych i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d642f-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="d642f-252">Więcej informacji na temat sposobu stosu toodeploy światło (Linux, Apache MySQL i PHP) poprawić toohello dalej toolearn samouczka.</span><span class="sxs-lookup"><span data-stu-id="d642f-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d642f-253">Wdrażanie stosu LAMP</span><span class="sxs-lookup"><span data-stu-id="d642f-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)