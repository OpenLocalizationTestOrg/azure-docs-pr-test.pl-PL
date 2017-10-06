---
title: dostarczanie aaaContinuous Git i Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure programu Visual Studio Team Services projekty zespołowe toouse Git tooautomatically tworzenie i wdrażanie toohello funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="e4f00-103">TooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services i Git</span><span class="sxs-lookup"><span data-stu-id="e4f00-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="e4f00-104">Można użyć toohost projektów programu Visual Studio Team Services team repozytorium Git do kodu źródłowego i automatycznie tworzenie i wdrażanie aplikacji sieci web tooAzure lub usług w chmurze przy każdym push repozytorium toohello zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="e4f00-105">Będziesz potrzebować programu Visual Studio 2013 oraz hello zainstalowany zestaw SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f00-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="e4f00-106">Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając hello **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj hello zestawu Azure SDK w [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="e4f00-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="e4f00-107">Należy toocomplete konta usługi Visual Studio Team Services w tym samouczku: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="e4f00-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="e4f00-108">tooset się tooautomatically usługi chmury tworzenie i wdrażanie tooAzure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e4f00-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="e4f00-109">1: Tworzenie repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="e4f00-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="e4f00-110">Jeśli nie masz już konto usługi Visual Studio Team Services, możesz ją uzyskać, [tutaj](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="e4f00-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="e4f00-111">Podczas tworzenia projektu zespołowego, wybierz Git jako system kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="e4f00-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="e4f00-112">Postępuj zgodnie z projektu zespołowego tooyour hello instrukcje tooconnect programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4f00-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="e4f00-113">W **Team Explorer**, wybierz hello **Klonuj to repozytorium** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="e4f00-114">Określ lokalizację hello hello kopii lokalnej, a następnie wybierz pozycję hello **klonowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="e4f00-115">2: utworzenie projektu i przekazać go toohello repozytorium</span><span class="sxs-lookup"><span data-stu-id="e4f00-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="e4f00-116">W **Team Explorer**, w hello **rozwiązań** wybierz hello **nowy** toocreate nowy projekt w repozytorium lokalne powitania łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="e4f00-117">Możesz wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacja) przez hello następujące kroki w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="e4f00-118">Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e4f00-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="e4f00-119">Upewnij się, że elementy docelowe projektu hello hello .NET Framework 4 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="e4f00-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="e4f00-120">W przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web programu ASP.NET MVC i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="e4f00-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="e4f00-121">Toocreate aplikacji sieci web, wybierz opcję hello **aplikacji sieci Web ASP.NET** projektu szablonu, a następnie wybierz pozycję **MVC**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="e4f00-122">Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e4f00-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="e4f00-123">Otwórz menu skrótów hello hello rozwiązania i wybierz polecenie **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="e4f00-124">Jeśli jest to hello używano Git w Visual Studio Team Services po raz pierwszy, musisz tooprovide tooidentify niektórych informacji samodzielnie w usłudze Git.</span><span class="sxs-lookup"><span data-stu-id="e4f00-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="e4f00-125">W hello **oczekujących zmian** obszar **Team Explorer**, wprowadź nazwy użytkownika i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="e4f00-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="e4f00-126">Wprowadź komentarz dotyczący hello zatwierdzania, a następnie wybierz pozycję hello **zatwierdzania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="e4f00-127">Należy zwrócić uwagę tooinclude opcje hello lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="e4f00-128">Jeśli zmiany hello chcesz są wyłączone, wybierz **obejmują wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="e4f00-129">Masz teraz hello zatwierdzić zmiany w lokalnej kopii hello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="e4f00-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="e4f00-130">Następnie synchronizacji wprowadzonych zmian z serwera hello, wybierając hello **synchronizacji** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="e4f00-131">3: łączenie hello tooAzure projektu</span><span class="sxs-lookup"><span data-stu-id="e4f00-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="e4f00-132">Teraz, gdy masz repozytorium Git w Visual Studio Team Services z kodu źródłowego w nim są gotowe tooconnect Twojego tooAzure repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="e4f00-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="e4f00-133">W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając Witaj + ikonę w lewy dolny hello i wybierając polecenie **usługi w chmurze** lub **aplikacji sieci Web**, a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="e4f00-134">Usługi w chmurze, wybrać hello **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="e4f00-135">W przypadku aplikacji sieci web, wybierz hello **Konfigurowanie wdrażania z kontroli źródła** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="e4f00-136">W Kreatorze hello, wpisz nazwę hello Twojego konta Visual Studio Team Services w polu tekstowym hello i wybierz polecenie hello **autoryzować teraz** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="e4f00-137">Użytkownik może zostać poproszony toosign w.</span><span class="sxs-lookup"><span data-stu-id="e4f00-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="e4f00-138">W hello **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** tooauthorize Azure tooconfigure Twojego zespołu projektu w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e4f00-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="e4f00-139">Po autoryzacji zakończy się powodzeniem, zostanie wyświetlona lista rozwijana zawierający projektach zespołowych Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e4f00-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="e4f00-140">Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach hello hello, a następnie wybierz przycisk znacznika wyboru hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="e4f00-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="e4f00-141">Hello następnym push repozytorium tooyour zatwierdzania, Visual Studio Team Services skompiluje oraz wdrożyć tooAzure Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="e4f00-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="e4f00-142">4: wyzwolenia kompilowania i wdrożenie projektu</span><span class="sxs-lookup"><span data-stu-id="e4f00-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="e4f00-143">W programie Visual Studio otwarcia pliku i zmodyfikuj go.</span><span class="sxs-lookup"><span data-stu-id="e4f00-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="e4f00-144">Na przykład zmienić plik hello `_Layout.cshtml` w obszarze widoki hello\\udostępniony folder w roli sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="e4f00-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="e4f00-145">Edytuj tekst stopki hello hello lokacji i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="e4f00-146">W **Eksploratora rozwiązań**, otwórz menu skrótów hello hello rozwiązania węzła, węzeł projektu lub hello plików można zmienić, a następnie wybierz **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="e4f00-147">Wpisz komentarz i wybierz **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="e4f00-148">Wybierz hello **synchronizacji** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="e4f00-149">Wybierz hello **Push** link toopush repozytorium toohello zatwierdzania w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e4f00-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="e4f00-150">(Można również użyć hello **synchronizacji** przycisk toocopy repozytorium toohello zatwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="e4f00-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="e4f00-151">Hello różnicą jest to, że **synchronizacji** również ściąga hello najnowsze zmiany z repozytorium hello.)</span><span class="sxs-lookup"><span data-stu-id="e4f00-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="e4f00-152">Wybierz hello **macierzystego** toohello tooreturn przycisk **Team Explorer** strony głównej.</span><span class="sxs-lookup"><span data-stu-id="e4f00-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="e4f00-153">Wybierz **kompilacje** tooview hello kompilacje w toku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="e4f00-154">**Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="e4f00-155">tooview szczegółowy dziennik jako hello kompilacji realizowany, kliknij dwukrotnie nazwę hello hello kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="e4f00-156">Podczas kompilacji hello jest w toku, Przyjrzyjmy się hello definicji kompilacji, która została utworzona stosowania hello kreatora toolink tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e4f00-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="e4f00-157">Otwórz menu skrótów powitania dla definicji kompilacji hello i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="e4f00-158">W hello **wyzwalacza** kartę, zobaczysz, że hello definicji kompilacji jest domyślnie toobuild na każdym zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="e4f00-159">(Dla usługi w chmurze, Visual Studio Team Services tworzy i wdraża toohello głównej gałęzi hello automatycznie przemieszczania środowiska.</span><span class="sxs-lookup"><span data-stu-id="e4f00-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="e4f00-160">Nadal masz toodo lokacji na żywo toohello toodeploy krok wykonywany ręcznie.</span><span class="sxs-lookup"><span data-stu-id="e4f00-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="e4f00-161">Dla aplikacji sieci web, która nie ma w środowisku przemieszczania wdrażania hello głównej gałęzi bezpośrednio toohello live lokacji.</span><span class="sxs-lookup"><span data-stu-id="e4f00-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="e4f00-162">W hello **procesu** karcie widać środowiska wdrażania hello jest ustawiona na nazwę toohello Twojego chmury usługi lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4f00-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="e4f00-163">Określ wartości dla właściwości hello, jeśli chcesz, aby wartości innej niż domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="e4f00-164">Witaj właściwości publikowania platformy Azure znajdują się w hello **wdrożenia** sekcji, a także mogą wymagać tooset MSBuild parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4f00-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="e4f00-165">Na przykład w projektu usługi w chmurze, toospecify konfiguracji usługi, innych niż "Chmura" Ustaw parametry MSbuild hello zbyt`/p:TargetProfile=[YourProfile]` gdzie *[YourProfile]* pasuje do pliku konfiguracji usługi z nazwą, np. Element ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="e4f00-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="e4f00-166">Witaj poniższej tabeli przedstawiono dostępne właściwości hello hello **wdrożenia** sekcji:</span><span class="sxs-lookup"><span data-stu-id="e4f00-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="e4f00-167">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e4f00-167">Property</span></span> | <span data-ttu-id="e4f00-168">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="e4f00-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e4f00-169">Zezwalaj na niezaufane certyfikaty</span><span class="sxs-lookup"><span data-stu-id="e4f00-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="e4f00-170">W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny.</span><span class="sxs-lookup"><span data-stu-id="e4f00-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="e4f00-171">Zezwalaj na uaktualnienie</span><span class="sxs-lookup"><span data-stu-id="e4f00-171">Allow Upgrade</span></span> |<span data-ttu-id="e4f00-172">Umożliwia tooupdate wdrożenia hello istniejącego wdrożenia zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="e4f00-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="e4f00-173">Zachowuje hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e4f00-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="e4f00-174">Nie usuwaj</span><span class="sxs-lookup"><span data-stu-id="e4f00-174">Do Not Delete</span></span> |<span data-ttu-id="e4f00-175">Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona).</span><span class="sxs-lookup"><span data-stu-id="e4f00-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="e4f00-176">Ścieżka tooDeployment ustawienia</span><span class="sxs-lookup"><span data-stu-id="e4f00-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="e4f00-177">Witaj ścieżki tooyour .pubxml pliku dla aplikacji sieci web, toohello względną głównego folderu repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="e4f00-178">Ignorowane dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e4f00-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="e4f00-179">Środowisko wdrażania SharePoint</span><span class="sxs-lookup"><span data-stu-id="e4f00-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="e4f00-180">Witaj takie same jak nazwa usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="e4f00-181">Środowisko wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4f00-181">Azure Deployment Environment</span></span> |<span data-ttu-id="e4f00-182">Witaj aplikacji lub w chmurze nazwę usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4f00-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="e4f00-183">Do tego czasu kompilacji powinien zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4f00-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="e4f00-184">Dwukrotne kliknięcie nazwy kompilacji hello Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="e4f00-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="e4f00-185">W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), można wyświetlić hello skojarzone wdrożenie na powitania **wdrożeń** karcie po wybraniu hello przemieszczania środowiska.</span><span class="sxs-lookup"><span data-stu-id="e4f00-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="e4f00-186">Adres URL witryny tooyour przeglądania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="e4f00-187">Dla aplikacji sieci web, wystarczy wybrać hello **Przeglądaj** przycisk w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="e4f00-188">Usługi w chmurze, wybierz adres URL hello hello **szybki przegląd** sekcji hello **pulpitu nawigacyjnego** strony zawierającej hello środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="e4f00-189">Wdrożenia z ciągłej integracji usług w chmurze są środowiska przemieszczania opublikowanych toohello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4f00-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="e4f00-190">Można zmienić to ustawienie hello **alternatywny środowiska usługi w chmurze** właściwości zbyt**produkcji**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="e4f00-191">Oto, gdy adres URL witryny hello znajduje się na stronie pulpitu nawigacyjnego usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="e4f00-192">Na nowej karcie przeglądarki zostanie otwarty tooreveal uruchomionej witryny.</span><span class="sxs-lookup"><span data-stu-id="e4f00-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="e4f00-193">Po wprowadzeniu innych zmian projektu tooyour, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="e4f00-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="e4f00-194">Witaj najnowszych jeden jest oznaczony jako aktywny.</span><span class="sxs-lookup"><span data-stu-id="e4f00-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="e4f00-195">5: należy ponownie wdrożyć wcześniejszą kompilację</span><span class="sxs-lookup"><span data-stu-id="e4f00-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="e4f00-196">Ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e4f00-196">This step is optional.</span></span> <span data-ttu-id="e4f00-197">Witaj klasycznego portalu Azure, wybierz wcześniejsze wdrożenie i wybierz **ponownie wdrożyć** toorewind tooan Twojego lokacji do wcześniej w zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="e4f00-198">Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e4f00-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="e4f00-199">6: Zmień hello wdrożenia produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="e4f00-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="e4f00-200">Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska produkcyjnego toohello dla hello przemieszczania, wybierając **wymiany** w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f00-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="e4f00-201">Hello nowo wdrożone środowiska przemieszczania jest awansowana tooProduction i hello poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="e4f00-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="e4f00-202">Hello aktywnych wdrożeń mogą być różne dla środowisk przemieszczania i hello produkcji, ale Historia wdrażania hello ostatnie kompilacji jest hello sama niezależnie od tego środowiska.</span><span class="sxs-lookup"><span data-stu-id="e4f00-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="e4f00-203">7: wdrażanie z gałęzi roboczej.</span><span class="sxs-lookup"><span data-stu-id="e4f00-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="e4f00-204">Korzystając z narzędzia Git, zwykle wprowadzono zmiany w gałęzi roboczych i integrowanie hello głównej gałęzi przy projektowaniu osiągnie stan zakończenia.</span><span class="sxs-lookup"><span data-stu-id="e4f00-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="e4f00-205">W fazie hello rozwoju projektu możesz mają toobuild i wdrożyć tooAzure gałęzi roboczych hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="e4f00-206">W **Team Explorer**, wybierz hello **Home** przycisk, a następnie wybierz pozycję hello **gałęzie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e4f00-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="e4f00-207">Wybierz hello **nowa gałąź** łącza.</span><span class="sxs-lookup"><span data-stu-id="e4f00-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="e4f00-208">Wprowadź nazwę hello hello gałęzi, takie jak "działa" i wybierz polecenie **utwórz gałąź**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="e4f00-209">Spowoduje to utworzenie nowej lokalnej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="e4f00-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="e4f00-210">Opublikuj gałęzi hello.</span><span class="sxs-lookup"><span data-stu-id="e4f00-210">Publish hello branch.</span></span> <span data-ttu-id="e4f00-211">Wybierz nazwę gałęzi hello w **nieopublikowanych gałęzi**i wybierz polecenie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="e4f00-212">Domyślnie tylko zmiany toohello głównej gałęzi wyzwalacza ciągłego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e4f00-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="e4f00-213">tooset się ciągłe kompilacji dla gałęzi roboczej, wybierz hello **kompilacje** strony **Team Explorer**i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="e4f00-214">Otwórz hello **ustawienia źródła** kartę. W obszarze **monitorowane gałęzi dla ciągłej integracji i kompilacji**, wybierz **kliknij tutaj tooadd nowy wiersz**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="e4f00-215">Określ hello gałęzi, z której zostały utworzone, takich jak system plików refs/głowic/pracy.</span><span class="sxs-lookup"><span data-stu-id="e4f00-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="e4f00-216">Zmiany w kodzie hello hello Otwórz menu skrótów dla pliku hello zmienione, a następnie wybierz pozycję **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="e4f00-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="e4f00-217">Wybierz hello **niezsynchronizowane zatwierdzeń** łącza, a następnie wybierz pozycję hello **synchronizacji** przycisku lub hello **Push** link toocopy hello zmienia toohello kopię gałąź roboczą hello w programie Visual Studio Usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="e4f00-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="e4f00-218">Przejdź toohello **kompilacje** wyświetlić i Znajdź gałąź roboczą hello hello kompilacji, który właśnie został wywołany.</span><span class="sxs-lookup"><span data-stu-id="e4f00-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4f00-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4f00-219">Next steps</span></span>
<span data-ttu-id="e4f00-220">Zobacz więcej porad w usłudze Visual Studio Team Services przy użyciu narzędzia Git toolearn [opracowanie i udostępnianie kodu w usłudze Git przy użyciu programu Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) oraz aby uzyskać informacje dotyczące korzystania z repozytorium Git, który nie jest zarządzany przez toopublish Visual Studio Team Services tooAzure, zobacz [tooAzure ciągłego wdrażania aplikacji usługi](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e4f00-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="e4f00-221">Aby uzyskać więcej informacji o programie Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="e4f00-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
