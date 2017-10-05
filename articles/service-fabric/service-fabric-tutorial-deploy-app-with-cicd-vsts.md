---
title: "Wdróż aplikację Azure Service Fabric przy ciągłej integracji (Team Services) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio Team Services.  Wdrażanie aplikacji do klastra usługi sieć szkieletowa na platformie Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: 631f9794994530092d05a33b06ebf8c07f331649
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-with-cicd-to-a-service-fabric-cluster"></a><span data-ttu-id="0b73b-104">Wdrażanie aplikacji przy użyciu elementu konfiguracji/CD do klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="0b73b-104">Deploy an application with CI/CD to a Service Fabric cluster</span></span>
<span data-ttu-id="0b73b-105">W tym samouczku jest częścią trzy serii i zawiera opis sposobu konfigurowania ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług Azure przy użyciu programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0b73b-105">This tutorial is part three of a series and describes how to set up continuous integration and deployment for an Azure Service Fabric application using Visual Studio Team Services.</span></span>  <span data-ttu-id="0b73b-106">Istniejącej aplikacji usługi sieć szkieletowa jest potrzebna, aplikacji utworzony w [tworzenia aplikacji .NET](service-fabric-tutorial-create-dotnet-app.md) służy jako przykład.</span><span class="sxs-lookup"><span data-stu-id="0b73b-106">An existing Service Fabric application is needed, the application created in [Build a .NET application](service-fabric-tutorial-create-dotnet-app.md) is used as an example.</span></span>

<span data-ttu-id="0b73b-107">W trzech części serii, możesz dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="0b73b-107">In part three of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0b73b-108">Dodaj do kontroli źródła do projektu</span><span class="sxs-lookup"><span data-stu-id="0b73b-108">Add source control to your project</span></span>
> * <span data-ttu-id="0b73b-109">Utwórz definicję kompilacji w Team Services</span><span class="sxs-lookup"><span data-stu-id="0b73b-109">Create a build definition in Team Services</span></span>
> * <span data-ttu-id="0b73b-110">Tworzenie definicji wersji w usłudze Team Services</span><span class="sxs-lookup"><span data-stu-id="0b73b-110">Create a release definition in Team Services</span></span>
> * <span data-ttu-id="0b73b-111">Automatyczne wdrażanie i uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-111">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="0b73b-112">W tym samouczku dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="0b73b-112">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="0b73b-113">Tworzenie aplikacji sieci szkieletowej usług .NET</span><span class="sxs-lookup"><span data-stu-id="0b73b-113">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * [<span data-ttu-id="0b73b-114">Wdrażanie aplikacji do zdalnego klastra</span><span class="sxs-lookup"><span data-stu-id="0b73b-114">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * <span data-ttu-id="0b73b-115">Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="0b73b-115">Configure CI/CD using Visual Studio Team Services</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b73b-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b73b-116">Prerequisites</span></span>
<span data-ttu-id="0b73b-117">Przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="0b73b-117">Before you begin this tutorial:</span></span>
- <span data-ttu-id="0b73b-118">Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="0b73b-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="0b73b-119">[Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) i zainstaluj **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.</span><span class="sxs-lookup"><span data-stu-id="0b73b-119">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="0b73b-120">Zainstaluj zestaw SDK sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="0b73b-120">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)
- <span data-ttu-id="0b73b-121">Tworzenie aplikacji usługi Service Fabric, na przykład przez [tego samouczka](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b73b-121">Create a Service Fabric application, for example by [following this tutorial](service-fabric-tutorial-create-dotnet-app.md).</span></span> 
- <span data-ttu-id="0b73b-122">Tworzenie klastra sieci szkieletowej usług systemu Windows na platformie Azure, na przykład przez [tego samouczka](service-fabric-tutorial-create-cluster-azure-ps.md)</span><span class="sxs-lookup"><span data-stu-id="0b73b-122">Create a Windows Service Fabric cluster on Azure, for example by [following this tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>
- <span data-ttu-id="0b73b-123">Utwórz [konta usługi Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="0b73b-123">Create a [Team Services account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>

## <a name="download-the-voting-sample-application"></a><span data-ttu-id="0b73b-124">Pobierz aplikację przykładową głosowania</span><span class="sxs-lookup"><span data-stu-id="0b73b-124">Download the Voting sample application</span></span>
<span data-ttu-id="0b73b-125">Jeśli nie zbudować głosowania przykładowej aplikacji [część jednego z tego samouczka serii](service-fabric-tutorial-create-dotnet-app.md), można go pobrać.</span><span class="sxs-lookup"><span data-stu-id="0b73b-125">If you did not build the Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="0b73b-126">W oknie poleceń uruchom następujące polecenie sklonować repozytorium przykładowej aplikacji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0b73b-126">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a><span data-ttu-id="0b73b-127">Przygotowanie profilu publikowania</span><span class="sxs-lookup"><span data-stu-id="0b73b-127">Prepare a publish profile</span></span>
<span data-ttu-id="0b73b-128">Znasz [utworzona aplikacja](service-fabric-tutorial-create-dotnet-app.md) i mieć [po wdrożeniu aplikacji na platformie Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md), wszystko jest gotowe do skonfigurowania ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-128">Now that you've [created an application](service-fabric-tutorial-create-dotnet-app.md) and have [deployed the application to Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md), you're ready to set up continuous integration.</span></span>  <span data-ttu-id="0b73b-129">Najpierw przygotować profilu publikowania w aplikacji do użycia przez proces wdrażania, która jest wykonywana w ramach usług Team Services.</span><span class="sxs-lookup"><span data-stu-id="0b73b-129">First, prepare a publish profile within your application for use by the deployment process that executes within Team Services.</span></span>  <span data-ttu-id="0b73b-130">Profil publikowania, należy skonfigurować pod kątem klastra, które wcześniej zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="0b73b-130">The publish profile should be configured to target the cluster that you've previously created.</span></span>  <span data-ttu-id="0b73b-131">Uruchom program Visual Studio i otworzyć istniejący projekt aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="0b73b-131">Start Visual Studio and open an existing Service Fabric application project.</span></span>  <span data-ttu-id="0b73b-132">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy aplikację i wybierz **publikowania...** .</span><span class="sxs-lookup"><span data-stu-id="0b73b-132">In **Solution Explorer**, right-click the application and select **Publish...**.</span></span>

<span data-ttu-id="0b73b-133">Wybierz profil docelowy w ramach projektu aplikacji w celu używania przepływu pracy ciągłej integracji, na przykład w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0b73b-133">Choose a target profile within your application project to use for your continuous integration workflow, for example Cloud.</span></span>  <span data-ttu-id="0b73b-134">Określ punktu końcowego połączenia klastra.</span><span class="sxs-lookup"><span data-stu-id="0b73b-134">Specify the cluster connection endpoint.</span></span>  <span data-ttu-id="0b73b-135">Sprawdź **uaktualnienie aplikacji** pole wyboru, aby aplikacja uaktualnia dla każdego wdrożenia w Team Services.</span><span class="sxs-lookup"><span data-stu-id="0b73b-135">Check the **Upgrade the Application** checkbox so that your application upgrades for each deployment in Team Services.</span></span>  <span data-ttu-id="0b73b-136">Kliknij przycisk **zapisać** hiperłącze, aby zapisać ustawienia w profilu publikowania, a następnie kliknij przycisk **anulować** aby zamknąć okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0b73b-136">Click the **Save** hyperlink to save the settings to the publish profile and then click **Cancel** to close the dialog box.</span></span>  

![Profil wypychania][publish-app-profile]

## <a name="share-your-visual-studio-solution-to-a-new-team-services-git-repo"></a><span data-ttu-id="0b73b-138">Udostępnianie rozwiązania Visual Studio do nowego repozytorium Git programu Team Services</span><span class="sxs-lookup"><span data-stu-id="0b73b-138">Share your Visual Studio solution to a new Team Services Git repo</span></span>
<span data-ttu-id="0b73b-139">Udostępnianie plików źródłowych aplikacji do projektu zespołowego Team Services, można wygenerować kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-139">Share your application source files to a team project in Team Services so you can generate builds.</span></span>  

<span data-ttu-id="0b73b-140">Utwórz nowe lokalne repozytorium Git dla projektu, zaznaczając **Dodaj do kontroli źródła** -> **Git** na pasku stanu w prawym dolnym rogu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b73b-140">Create a new local Git repo for your project by selecting **Add to Source Control** -> **Git** on the status bar in the lower right-hand corner of Visual Studio.</span></span> 

<span data-ttu-id="0b73b-141">W **Push** wyświetlić w **Team Explorer**, wybierz pozycję **Publikuj repozytorium Git** przycisku w obszarze **wypychania do programu Visual Studio Team Services**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-141">In the **Push** view in **Team Explorer**, select the **Publish Git Repo** button under **Push to Visual Studio Team Services**.</span></span>

![Wypychanie repozytorium Git][push-git-repo]

<span data-ttu-id="0b73b-143">Sprawdź pocztę i wybierz konto w **zespołu usług domenowych** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="0b73b-143">Verify your email and select your account in the **Team Services Domain** drop-down.</span></span> <span data-ttu-id="0b73b-144">Wprowadź nazwę repozytorium i wybierz **Publikuj repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-144">Enter your repository name and select **Publish repository**.</span></span>

![Wypychanie repozytorium Git][publish-code]

<span data-ttu-id="0b73b-146">Opublikowanie repozytorium powoduje utworzenie nowego projektu zespołowego na koncie z taką samą nazwę jak lokalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0b73b-146">Publishing the repo creates a new team project in your account with the same name as the local repo.</span></span> <span data-ttu-id="0b73b-147">Aby utworzyć repozytorium w istniejących projektów zespołowych, kliknij przycisk **zaawansowane** obok **repozytorium** nazwę, a następnie wybierz projekt zespołowy.</span><span class="sxs-lookup"><span data-stu-id="0b73b-147">To create the repo in an existing team project, click **Advanced** next to **Repository** name and select a team project.</span></span> <span data-ttu-id="0b73b-148">Kod w sieci web można wyświetlić, wybierając **jest widoczny w sieci web**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-148">You can view your code on the web by selecting **See it on the web**.</span></span>

## <a name="configure-continuous-delivery-with-vsts"></a><span data-ttu-id="0b73b-149">Konfigurowanie ciągłego dostarczania przy użyciu programu VSTS</span><span class="sxs-lookup"><span data-stu-id="0b73b-149">Configure Continuous Delivery with VSTS</span></span>
<span data-ttu-id="0b73b-150">Definicja kompilacji Team Services zawiera opis przepływu pracy, który składa się z zestaw kroków kompilacji, które są wykonywane sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="0b73b-150">A Team Services build definition describes a workflow that is composed of a set of build steps that are executed sequentially.</span></span> <span data-ttu-id="0b73b-151">Utwórz definicję kompilacji, który, który spowoduje utworzenie pakietu aplikacji sieci szkieletowej usług i innych artefakty do wdrożenia klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="0b73b-151">Create a build definition that that produces a Service Fabric application package, and other artifacts, to deploy to a Service Fabric cluster.</span></span> <span data-ttu-id="0b73b-152">Dowiedz się więcej o [definicje kompilacji Team Services](https://www.visualstudio.com/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="0b73b-152">Learn more about [Team Services build definitions](https://www.visualstudio.com/docs/build/define/create).</span></span> 

<span data-ttu-id="0b73b-153">Definicja wersji Team Services opisano przepływ pracy, który wdraża pakiet aplikacji do klastra.</span><span class="sxs-lookup"><span data-stu-id="0b73b-153">A Team Services release definition describes a workflow that deploys an application package to a cluster.</span></span> <span data-ttu-id="0b73b-154">Razem definicję kompilacji i wersji definicji wykonać całego przepływu pracy, zaczynając od plików źródłowych z uruchomioną aplikację w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0b73b-154">When used together, the build definition and release definition execute the entire workflow starting with source files to ending with a running application in your cluster.</span></span> <span data-ttu-id="0b73b-155">Dowiedz się więcej na temat usługi Team Services [wersji definicji](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span><span class="sxs-lookup"><span data-stu-id="0b73b-155">Learn more about Team Services [release definitions](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span></span>

### <a name="create-a-build-definition"></a><span data-ttu-id="0b73b-156">Tworzenie definicji kompilacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-156">Create a build definition</span></span>
<span data-ttu-id="0b73b-157">Otwórz przeglądarkę sieci web i przejdź do nowego projektu zespołowego na: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting.</span><span class="sxs-lookup"><span data-stu-id="0b73b-157">Open a web browser and navigate to your new team project at: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting .</span></span> 

<span data-ttu-id="0b73b-158">Wybierz **kompilacji i wydania** karcie następnie **kompilacje**, następnie **+ nową definicję**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-158">Select the **Build & Release** tab, then **Builds**, then **+ New definition**.</span></span>  <span data-ttu-id="0b73b-159">W **wybierz szablon**, wybierz pozycję **aplikacji sieci szkieletowej usług Azure** szablon i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-159">In **Select a template**, select the **Azure Service Fabric Application** template and click **Apply**.</span></span> 

![Wybierz szablon kompilacji][select-build-template] 

<span data-ttu-id="0b73b-161">Aplikację do głosowania zawiera projekt .NET Core, a więc Dodaj zadanie, które przywraca zależności.</span><span class="sxs-lookup"><span data-stu-id="0b73b-161">The voting application contains a .NET Core project, so add a task that restores the dependencies.</span></span> <span data-ttu-id="0b73b-162">W **zadania** widok, wybierz opcję **+ Dodaj zadanie** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="0b73b-162">In the **Tasks** view, select **+ Add Task** in the bottom left.</span></span> <span data-ttu-id="0b73b-163">Wyszukaj frazę "Wiersza polecenia" Znajdź zadania wiersza polecenia, a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-163">Search on "Command Line" to find the command-line task, then click **Add**.</span></span> 

![Dodaj zadanie][add-task] 

<span data-ttu-id="0b73b-165">W nowych zadań, wprowadź "Uruchom dotnet.exe" w **Nazwa wyświetlana**, "dotnet.exe" w **narzędzie**, a "Przywróć" w **argumenty**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-165">In the new task, enter "Run dotnet.exe" in **Display name**, "dotnet.exe" in **Tool**, and "restore" in **Arguments**.</span></span> 

![Nowe zadanie][new-task] 

<span data-ttu-id="0b73b-167">W **wyzwalaczy** wyświetlić, kliknij przycisk **włączyć tego wyzwalacza** przełącznika w obszarze **ciągłej integracji**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-167">In the **Triggers** view, click the **Enable this trigger** switch under **Continuous Integration**.</span></span> 

<span data-ttu-id="0b73b-168">Wybierz **Zapisz & kolejka** , a następnie wprowadź "VS2017 hostowanej" jako **kolejki agenta**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-168">Select **Save & queue** and enter "Hosted VS2017" as the **Agent queue**.</span></span> <span data-ttu-id="0b73b-169">Wybierz **kolejki** ręcznie uruchomić kompilację.</span><span class="sxs-lookup"><span data-stu-id="0b73b-169">Select **Queue** to manually start a build.</span></span>  <span data-ttu-id="0b73b-170">Opisano również wyzwalacze wypychania lub zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="0b73b-170">Builds also triggers upon push or check-in.</span></span>

<span data-ttu-id="0b73b-171">Aby sprawdzić postęp kompilacji, Przełącz **kompilacje** kartę.  Po upewnieniu się, że Kompilacja została wykonana pomyślnie, należy zdefiniować definicji wersji, która wdraża aplikację do klastra.</span><span class="sxs-lookup"><span data-stu-id="0b73b-171">To check your build progress, switch to the **Builds** tab.  Once you verify that the build executes successfully, define a release definition that deploys your application to a cluster.</span></span> 

### <a name="create-a-release-definition"></a><span data-ttu-id="0b73b-172">Utwórz definicję zlecenia</span><span class="sxs-lookup"><span data-stu-id="0b73b-172">Create a release definition</span></span>  

<span data-ttu-id="0b73b-173">Wybierz **kompilacji i wydania** karcie następnie **wersje**, następnie **+ nową definicję**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-173">Select the **Build & Release** tab, then **Releases**, then **+ New definition**.</span></span>  <span data-ttu-id="0b73b-174">W **Tworzenie wersji definicji**, wybierz pozycję **wdrażania usługi Azure Service Fabric** szablon z listy i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-174">In **Create release definition**, select the **Azure Service Fabric Deployment** template from the list and click **Next**.</span></span>  <span data-ttu-id="0b73b-175">Wybierz **kompilacji** źródła, sprawdź **ciągłe wdrażanie** i kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-175">Select the **Build** source, check the **Continuous deployment** box, and click **Create**.</span></span> 

<span data-ttu-id="0b73b-176">W **środowisk** wyświetlić, kliknij przycisk **Dodaj** z prawej strony **połączenia klastra**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-176">In the **Environments** view, click **Add** to the right of **Cluster Connection**.</span></span>  <span data-ttu-id="0b73b-177">Określ nazwę połączenia "mysftestcluster", punkt końcowy klastra o "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" i usługi Azure Active Directory lub poświadczeń certyfikatu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="0b73b-177">Specify a connection name of "mysftestcluster", a cluster endpoint of "tcp://mysftestcluster.westus.cloudapp.azure.com:19000", and the Azure Active Directory or certificate credentials for the cluster.</span></span> <span data-ttu-id="0b73b-178">Dla poświadczeń usługi Azure Active Directory, należy zdefiniować poświadczeń ma być używana do łączenia się z klastrem w **Username** i **hasło** pola.</span><span class="sxs-lookup"><span data-stu-id="0b73b-178">For Azure Active Directory credentials, define the credentials you want to use to connect to the cluster in the **Username** and **Password** fields.</span></span> <span data-ttu-id="0b73b-179">Do uwierzytelniania opartego na certyfikatach, zdefiniuj kodowania Base64 plik certyfikatu klienta w **certyfikatu klienta** pola.</span><span class="sxs-lookup"><span data-stu-id="0b73b-179">For certificate-based authentication, define the Base64 encoding of the client certificate file in the **Client Certificate** field.</span></span>  <span data-ttu-id="0b73b-180">Zapoznaj się z pomocą wyskakującego o to pole, aby uzyskać informacje dotyczące sposobu uzyskania tej wartości.</span><span class="sxs-lookup"><span data-stu-id="0b73b-180">See the help pop-up on that field for info on how to get that value.</span></span>  <span data-ttu-id="0b73b-181">Jeśli certyfikat jest chroniony hasłem, należy określić hasło w **hasło** pola.</span><span class="sxs-lookup"><span data-stu-id="0b73b-181">If your certificate is password-protected, define the password in the **Password** field.</span></span>  <span data-ttu-id="0b73b-182">Kliknij przycisk **zapisać** można zapisać definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-182">Click **Save** to save the release definition.</span></span>

![Dodaj połączenie klastra][add-cluster-connection] 

<span data-ttu-id="0b73b-184">Kliknij przycisk **Uruchom agenta**, a następnie wybierz pozycję **hostowane VS2017** dla **kolejki wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="0b73b-184">Click **Run on agent**, then select **Hosted VS2017** for **Deployment queue**.</span></span> <span data-ttu-id="0b73b-185">Kliknij przycisk **zapisać** można zapisać definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-185">Click **Save** to save the release definition.</span></span>

![Uruchom agenta][run-on-agent]

<span data-ttu-id="0b73b-187">Wybierz **+ wersji** -> **Tworzenie wersji** -> **Utwórz** ręczne tworzenie zlecenia.</span><span class="sxs-lookup"><span data-stu-id="0b73b-187">Select **+Release** -> **Create Release** -> **Create** to manually create a release.</span></span>  <span data-ttu-id="0b73b-188">Sprawdź, czy wdrożenie zakończyło się pomyślnie, a aplikacja jest uruchomiona w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0b73b-188">Verify that the deployment succeeded and the application is running in the cluster.</span></span>  <span data-ttu-id="0b73b-189">Otwórz przeglądarkę sieci web i przejdź do [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="0b73b-189">Open a web browser and navigate to [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="0b73b-190">Należy pamiętać, wersja aplikacji, w tym przykładzie jest "1.0.0.20170616.3".</span><span class="sxs-lookup"><span data-stu-id="0b73b-190">Note the application version, in this example it is "1.0.0.20170616.3".</span></span> 

## <a name="commit-and-push-changes-trigger-a-release"></a><span data-ttu-id="0b73b-191">Zatwierdź i Wypchnij zmiany, wyzwalanie wydania</span><span class="sxs-lookup"><span data-stu-id="0b73b-191">Commit and push changes, trigger a release</span></span>
<span data-ttu-id="0b73b-192">Aby sprawdzić, czy działa potoku ciągłej integracji, sprawdzając w pewnych zmian kodu usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="0b73b-192">To verify that the continuous integration pipeline is functioning by checking in some code changes to Team Services.</span></span>    

<span data-ttu-id="0b73b-193">Podczas pisania kodu zmiany automatycznie są śledzone przez program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b73b-193">As you write your code, your changes are automatically tracked by Visual Studio.</span></span> <span data-ttu-id="0b73b-194">Zatwierdź zmiany w lokalnym repozytorium Git, wybierając ikonę (oczekujących zmian</span><span class="sxs-lookup"><span data-stu-id="0b73b-194">Commit changes to your local Git repository by selecting the pending changes icon (</span></span>![Oczekujące][pending]<span data-ttu-id="0b73b-196">) na pasku stanu, w prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="0b73b-196">) from the status bar in the bottom right.</span></span>

<span data-ttu-id="0b73b-197">Na **zmiany** wyświetlić w programie Team Explorer, Dodaj komunikat opisujący aktualizacji i zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="0b73b-197">On the **Changes** view in Team Explorer, add a message describing your update and commit your changes.</span></span>

![Zatwierdź wszystko][changes]

<span data-ttu-id="0b73b-199">Wybierz ikonę paska nieopublikowane zmiany stanu (![nieopublikowane zmiany][unpublished-changes]) lub widoku synchronizacji w programie Team Explorer.</span><span class="sxs-lookup"><span data-stu-id="0b73b-199">Select the unpublished changes status bar icon (![Unpublished changes][unpublished-changes]) or the Sync view in Team Explorer.</span></span> <span data-ttu-id="0b73b-200">Wybierz **Push** można zaktualizować kodu w Team Services/TFS.</span><span class="sxs-lookup"><span data-stu-id="0b73b-200">Select **Push** to update your code in Team Services/TFS.</span></span>

![Wypchnij zmiany][push]

<span data-ttu-id="0b73b-202">Wypychanie zmiany do usługi Team Services automatycznie wyzwala kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-202">Pushing the changes to Team Services automatically triggers a build.</span></span>  <span data-ttu-id="0b73b-203">Po pomyślnym zakończeniu definicji kompilacji, zlecenia zostanie utworzona automatycznie i rozpoczyna uaktualnianie aplikacji w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0b73b-203">When the build definition successfully completes, a release is automatically created and starts upgrading the application on the cluster.</span></span>

<span data-ttu-id="0b73b-204">Aby sprawdzić postęp kompilacji, Przełącz **kompilacje** karcie **Team Explorer** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b73b-204">To check your build progress, switch to the **Builds** tab in **Team Explorer** in Visual Studio.</span></span>  <span data-ttu-id="0b73b-205">Po upewnieniu się, że Kompilacja została wykonana pomyślnie, należy zdefiniować definicji wersji, która wdraża aplikację do klastra.</span><span class="sxs-lookup"><span data-stu-id="0b73b-205">Once you verify that the build executes successfully, define a release definition that deploys your application to a cluster.</span></span>

<span data-ttu-id="0b73b-206">Sprawdź, czy wdrożenie zakończyło się pomyślnie, a aplikacja jest uruchomiona w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0b73b-206">Verify that the deployment succeeded and the application is running in the cluster.</span></span>  <span data-ttu-id="0b73b-207">Otwórz przeglądarkę sieci web i przejdź do [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="0b73b-207">Open a web browser and navigate to [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="0b73b-208">Należy pamiętać, wersja aplikacji, w tym przykładzie jest "1.0.0.20170815.3".</span><span class="sxs-lookup"><span data-stu-id="0b73b-208">Note the application version, in this example it is "1.0.0.20170815.3".</span></span>

![Service Fabric Explorer][sfx1]

## <a name="update-the-application"></a><span data-ttu-id="0b73b-210">Aktualizowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-210">Update the application</span></span>
<span data-ttu-id="0b73b-211">Zmiany kodu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-211">Make code changes in the application.</span></span>  <span data-ttu-id="0b73b-212">Zapisz i zatwierdź zmiany po poprzednich kroków.</span><span class="sxs-lookup"><span data-stu-id="0b73b-212">Save and commit the changes, following the previous steps.</span></span>

<span data-ttu-id="0b73b-213">Po rozpoczęciu uaktualnienia aplikacji, możesz obserwować postęp uaktualniania w narzędziu Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="0b73b-213">Once the upgrade of the application begins, you can watch the upgrade progress in Service Fabric Explorer:</span></span>

![Service Fabric Explorer][sfx2]

<span data-ttu-id="0b73b-215">Uaktualnianie aplikacji może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0b73b-215">The application upgrade may take several minutes.</span></span> <span data-ttu-id="0b73b-216">Po ukończeniu uaktualniania aplikacja zostanie uruchomiona następnej wersji.</span><span class="sxs-lookup"><span data-stu-id="0b73b-216">When the upgrade is complete, the application will be running the next version.</span></span>  <span data-ttu-id="0b73b-217">W tym przykładzie "1.0.0.20170815.4".</span><span class="sxs-lookup"><span data-stu-id="0b73b-217">In this example "1.0.0.20170815.4".</span></span>

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a><span data-ttu-id="0b73b-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b73b-219">Next steps</span></span>
<span data-ttu-id="0b73b-220">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="0b73b-220">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0b73b-221">Dodaj do kontroli źródła do projektu</span><span class="sxs-lookup"><span data-stu-id="0b73b-221">Add source control to your project</span></span>
> * <span data-ttu-id="0b73b-222">Tworzenie definicji kompilacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-222">Create a build definition</span></span>
> * <span data-ttu-id="0b73b-223">Utwórz definicję zlecenia</span><span class="sxs-lookup"><span data-stu-id="0b73b-223">Create a release definition</span></span>
> * <span data-ttu-id="0b73b-224">Automatyczne wdrażanie i uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-224">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="0b73b-225">Teraz, wdrożonych aplikacji i skonfigurować ciągłej integracji spróbować wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0b73b-225">Now that you have deployed an application and configured continuous integration, try the following:</span></span>
- [<span data-ttu-id="0b73b-226">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-226">Upgrade an app</span></span>](service-fabric-application-upgrade.md)
- [<span data-ttu-id="0b73b-227">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0b73b-227">Test an app</span></span>](service-fabric-testability-overview.md) 
- [<span data-ttu-id="0b73b-228">Monitorowanie i diagnozowanie</span><span class="sxs-lookup"><span data-stu-id="0b73b-228">Monitor and diagnose</span></span>](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png