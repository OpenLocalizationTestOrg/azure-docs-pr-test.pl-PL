---
title: "Ciągłego dostarczania Git i Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować projektach zespołowych Visual Studio Team Services, można użyć do automatycznego tworzenia i wdrażania dla funkcji aplikacji sieci Web w usłudze Azure App Service lub w chmurze usługi Git."
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="a1791-103">Ciągłe dostarczanie na platformę Azure za pomocą usługi Visual Studio Team Services i Git</span><span class="sxs-lookup"><span data-stu-id="a1791-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="a1791-104">Projekty zespołowe Visual Studio Team Services umożliwia hosta repozytorium Git do kodu źródłowego i automatycznie kompilacji i wdrażania aplikacji sieci web platformy Azure lub usługi w chmurze zawsze, gdy wypychanie zatwierdzeń do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1791-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="a1791-105">Będziesz potrzebować programu Visual Studio 2013 oraz zainstalowany zestaw SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="a1791-106">Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a1791-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="a1791-107">Zainstaluj zestaw Azure SDK z [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="a1791-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="a1791-108">Musisz mieć konto usługi Visual Studio Team Services do ukończenia tego samouczka: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="a1791-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="a1791-109">Aby skonfigurować usługi w chmurze spowoduje automatyczne utworzenie i wdrażanie na platformie Azure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="a1791-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="a1791-110">1: Tworzenie repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="a1791-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="a1791-111">Jeśli nie masz już konto usługi Visual Studio Team Services, możesz ją uzyskać, [tutaj](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="a1791-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="a1791-112">Podczas tworzenia projektu zespołowego, wybierz Git jako system kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a1791-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="a1791-113">Postępuj zgodnie z instrukcjami, aby połączyć program Visual Studio do projektu zespołowego.</span><span class="sxs-lookup"><span data-stu-id="a1791-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="a1791-114">W **Team Explorer**, wybierz **Klonuj to repozytorium** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="a1791-115">Określ lokalizację kopii lokalnej, a następnie wybierz pozycję **klonowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1791-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="a1791-116">2: utworzenie projektu i przekazać go do repozytorium</span><span class="sxs-lookup"><span data-stu-id="a1791-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="a1791-117">W **Team Explorer**w **rozwiązań** wybierz **nowy** łącze, aby utworzyć nowy projekt w lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1791-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="a1791-118">Wykonując kroki opisane w tym przewodniku można wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacji).</span><span class="sxs-lookup"><span data-stu-id="a1791-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="a1791-119">Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a1791-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="a1791-120">Upewnij się, że projekt jest przeznaczony dla programu .NET Framework 4 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="a1791-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="a1791-121">W przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web programu ASP.NET MVC i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="a1791-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="a1791-122">Jeśli chcesz utworzyć aplikację sieci web, wybierz **aplikacji sieci Web ASP.NET** projektu szablonu, a następnie wybierz pozycję **MVC**.</span><span class="sxs-lookup"><span data-stu-id="a1791-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="a1791-123">Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a1791-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="a1791-124">Otwórz menu skrótów dla rozwiązania i wybierz polecenie **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="a1791-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="a1791-125">Jest to po raz pierwszy w programie Visual Studio Team Services użyto Git, należy podać niektóre informacje w celu identyfikacji w usłudze Git.</span><span class="sxs-lookup"><span data-stu-id="a1791-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="a1791-126">W **oczekujących zmian** obszar **Team Explorer**, wprowadź nazwy użytkownika i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="a1791-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="a1791-127">Wprowadź komentarz dotyczący zatwierdzenia, a następnie wybierz pozycję **zatwierdzania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1791-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="a1791-128">Należy pamiętać, opcje, aby dołączyć lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="a1791-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="a1791-129">Jeśli odpowiednie zmiany, są wykluczone, wybierz **obejmują wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="a1791-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="a1791-130">Zostały teraz zatwierdzone zmiany w lokalnej kopii repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1791-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="a1791-131">Następnie zsynchronizować te zmiany z serwerem, wybierając **synchronizacji** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="a1791-132">3: Połącz projekt na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a1791-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="a1791-133">Teraz, gdy masz repozytorium Git w Visual Studio Team Services z kodu źródłowego w nim można przystąpić do repozytorium git połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="a1791-134">W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając pozycję + ikony na dole po lewej i wybierając polecenie **usługi w chmurze** lub **aplikacji sieci Web** , a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="a1791-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="a1791-135">Usługi w chmurze, można wybrać **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="a1791-136">W przypadku aplikacji sieci web, wybierz **Konfigurowanie wdrażania z kontroli źródła** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="a1791-137">W kreatorze, w polu tekstowym wprowadź nazwę konta usługi Visual Studio Team Services, a następnie wybierz pozycję **autoryzować teraz** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="a1791-138">Może być konieczne podanie do logowania.</span><span class="sxs-lookup"><span data-stu-id="a1791-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="a1791-139">W **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** do autoryzacji Azure, aby skonfigurować projekt zespołowy w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1791-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="a1791-140">Po autoryzacji zakończy się powodzeniem, zostanie wyświetlona lista rozwijana zawierający projektach zespołowych Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1791-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="a1791-141">Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach, a następnie wybierz przycisk wyboru w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="a1791-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="a1791-142">Przy następnym wypychanie zatwierdzeń do repozytorium, Visual Studio Team Services skompiluje oraz wdrażanie projektu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="a1791-143">4: wyzwolenia kompilowania i wdrożenie projektu</span><span class="sxs-lookup"><span data-stu-id="a1791-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="a1791-144">W programie Visual Studio otwarcia pliku i zmodyfikuj go.</span><span class="sxs-lookup"><span data-stu-id="a1791-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="a1791-145">Na przykład zmienić plik `_Layout.cshtml` pod widokami\\udostępniony folder w roli sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="a1791-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="a1791-146">Edytuj tekst stopki dla lokacji i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="a1791-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="a1791-147">W **Eksploratora rozwiązań**, otwórz menu skrótów węzła rozwiązania, węzła projektu lub pliku zmienione, a następnie wybierz pozycję **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="a1791-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="a1791-148">Wpisz komentarz i wybierz **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="a1791-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="a1791-149">Wybierz **synchronizacji** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="a1791-150">Wybierz **wypychania** łącze do wypychania Twojego zatwierdzenia w repozytorium w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1791-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="a1791-151">(Można również użyć **synchronizacji** przycisk, aby skopiować zatwierdzenia w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1791-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="a1791-152">Różnica jest to, że **synchronizacji** również pobiera najnowsze zmiany z repozytorium.)</span><span class="sxs-lookup"><span data-stu-id="a1791-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="a1791-153">Wybierz **macierzystego** przycisk, aby powrócić do **Team Explorer** strony głównej.</span><span class="sxs-lookup"><span data-stu-id="a1791-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="a1791-154">Wybierz **kompilacje** Aby wyświetlić kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="a1791-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="a1791-155">**Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="a1791-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="a1791-156">Aby wyświetlić szczegółowy dziennik w trakcie kompilacji, kliknij dwukrotnie nazwę kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="a1791-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="a1791-157">Gdy kompilacja jest w toku, Przyjrzyjmy się definicję kompilacji, który został utworzony, gdy Kreator jest używany do łączenia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="a1791-158">Otwórz menu skrótów dla definicji kompilacji i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="a1791-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="a1791-159">W **wyzwalacza** kartę, zobaczysz, że definicji kompilacji jest ustawiony na każdym zaewidencjonowania, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a1791-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="a1791-160">(Dla usługi w chmurze programu Visual Studio Team Services tworzy i wdraża głównej gałęzi do środowiska pomostowego automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a1791-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="a1791-161">Nadal musisz wykonać krok wykonywany ręcznie do wdrożenia na stronie.</span><span class="sxs-lookup"><span data-stu-id="a1791-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="a1791-162">Dla aplikacji sieci web, która nie ma w środowisku przemieszczania wdraża gałęzi głównej bezpośrednio do witryny na żywo.</span><span class="sxs-lookup"><span data-stu-id="a1791-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="a1791-163">W **procesu** karcie widać środowiska wdrażania jest ustawiona na nazwę Twojej chmury usługi lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1791-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="a1791-164">Określ wartości dla właściwości, jeśli chcesz, aby wartości innej niż wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="a1791-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="a1791-165">Właściwości publikowania platformy Azure są w **wdrożenia** sekcji, a także mogą wymagać ustawić parametry MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a1791-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="a1791-166">Na przykład w chmurze projekt usługi, aby określić konfigurację usługi innego niż "Chmura" Ustaw MSbuild parametrów `/p:TargetProfile=[YourProfile]` gdzie *[YourProfile]* pasuje do pliku konfiguracji usługi z nazwą jak element ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="a1791-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="a1791-167">W poniższej tabeli przedstawiono dostępne właściwości w **wdrożenia** sekcji:</span><span class="sxs-lookup"><span data-stu-id="a1791-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="a1791-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1791-168">Property</span></span> | <span data-ttu-id="a1791-169">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="a1791-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a1791-170">Zezwalaj na niezaufane certyfikaty</span><span class="sxs-lookup"><span data-stu-id="a1791-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="a1791-171">W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny.</span><span class="sxs-lookup"><span data-stu-id="a1791-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="a1791-172">Zezwalaj na uaktualnienie</span><span class="sxs-lookup"><span data-stu-id="a1791-172">Allow Upgrade</span></span> |<span data-ttu-id="a1791-173">Umożliwia wdrożenie, aby zaktualizować istniejące wdrożenie zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="a1791-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="a1791-174">Zachowuje adres IP.</span><span class="sxs-lookup"><span data-stu-id="a1791-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="a1791-175">Nie usuwaj</span><span class="sxs-lookup"><span data-stu-id="a1791-175">Do Not Delete</span></span> |<span data-ttu-id="a1791-176">Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona).</span><span class="sxs-lookup"><span data-stu-id="a1791-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="a1791-177">Ścieżka do ustawienia wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a1791-177">Path to Deployment Settings</span></span> |<span data-ttu-id="a1791-178">Ścieżka do pliku .pubxml dla aplikacji sieci web, względem głównego folderu repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1791-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="a1791-179">Ignorowane dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a1791-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="a1791-180">Środowisko wdrażania SharePoint</span><span class="sxs-lookup"><span data-stu-id="a1791-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="a1791-181">Taka sama jak nazwa usługi.</span><span class="sxs-lookup"><span data-stu-id="a1791-181">The same as the service name.</span></span> |
    | <span data-ttu-id="a1791-182">Środowisko wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a1791-182">Azure Deployment Environment</span></span> |<span data-ttu-id="a1791-183">Nazwa sieci web aplikacji lub w chmurze usługi.</span><span class="sxs-lookup"><span data-stu-id="a1791-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="a1791-184">Do tego czasu kompilacji powinien zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a1791-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="a1791-185">Dwukrotne kliknięcie nazwy kompilacji programu Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="a1791-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="a1791-186">W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), skojarzone wdrożenia można obejrzeć w **wdrożeń** karcie, gdy środowisko tymczasowe jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="a1791-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="a1791-187">Przejdź do adresu URL witryny.</span><span class="sxs-lookup"><span data-stu-id="a1791-187">Browse to your site's URL.</span></span> <span data-ttu-id="a1791-188">Dla aplikacji sieci web, wystarczy wybrać **Przeglądaj** przycisk w portalu.</span><span class="sxs-lookup"><span data-stu-id="a1791-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="a1791-189">Usługi w chmurze, wybierz adres URL w **szybki przegląd** sekcji **pulpitu nawigacyjnego** strony zawierającej środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="a1791-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="a1791-190">Wdrożenia z ciągłej integracji usług w chmurze są publikowane w środowisku przemieszczania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a1791-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="a1791-191">Możesz zmienić to ustawienie **alternatywny środowiska usługi w chmurze** właściwości **produkcji**.</span><span class="sxs-lookup"><span data-stu-id="a1791-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="a1791-192">Oto, gdy adres URL witryny jest na stronie pulpitu nawigacyjnego usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a1791-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="a1791-193">Na nowej karcie przeglądarki będą otwierane w celu wyświetlenia uruchomionej witryny.</span><span class="sxs-lookup"><span data-stu-id="a1791-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="a1791-194">Inne zmiany do projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="a1791-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="a1791-195">Najnowszego jest oznaczony jako aktywny.</span><span class="sxs-lookup"><span data-stu-id="a1791-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="a1791-196">5: należy ponownie wdrożyć wcześniejszą kompilację</span><span class="sxs-lookup"><span data-stu-id="a1791-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="a1791-197">Ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a1791-197">This step is optional.</span></span> <span data-ttu-id="a1791-198">W klasycznym portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz polecenie **ponownie wdrożyć** do tyłu witryny wcześniej zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="a1791-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="a1791-199">Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a1791-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="a1791-200">6: Zmień wdrożenia produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="a1791-200">6: Change the Production deployment</span></span>
<span data-ttu-id="a1791-201">Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska przemieszczania do środowiska produkcyjnego, wybierając **wymiany** w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="a1791-202">Nowo wdrożonym środowiska przemieszczania jest podwyższany do środowiska produkcyjnego i poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="a1791-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="a1791-203">Aktywne wdrożenie może się różnić w produkcyjne i przejściowe środowisk, ale Historia wdrażania ostatnie kompilacji jest taka sama niezależnie od środowiska.</span><span class="sxs-lookup"><span data-stu-id="a1791-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="a1791-204">7: wdrażanie z gałęzi roboczej.</span><span class="sxs-lookup"><span data-stu-id="a1791-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="a1791-205">Korzystając z narzędzia Git, zwykle wprowadzono zmiany w gałęzi roboczych i integracji w gałęzi głównej przy projektowaniu osiągnie stan zakończenia.</span><span class="sxs-lookup"><span data-stu-id="a1791-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="a1791-206">Podczas fazy opracowywania projektu należy do tworzenia i wdrażania gałąź roboczą do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a1791-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="a1791-207">W **Team Explorer**, wybierz **Home** przycisk, a następnie wybierz pozycję **gałęzie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1791-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="a1791-208">Wybierz **nowa gałąź** łącza.</span><span class="sxs-lookup"><span data-stu-id="a1791-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="a1791-209">Wprowadź nazwę gałęzi, takie jak "działa", a następnie wybierz **utwórz gałąź**.</span><span class="sxs-lookup"><span data-stu-id="a1791-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="a1791-210">Spowoduje to utworzenie nowej lokalnej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="a1791-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="a1791-211">Opublikuj gałęzi.</span><span class="sxs-lookup"><span data-stu-id="a1791-211">Publish the branch.</span></span> <span data-ttu-id="a1791-212">Wybierz nazwę gałęzi w **nieopublikowanych gałęzi**i wybierz polecenie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="a1791-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="a1791-213">Domyślnie tylko zmiany do gałęzi głównej wyzwolić kompilację ciągłe.</span><span class="sxs-lookup"><span data-stu-id="a1791-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="a1791-214">Aby skonfigurować ciągłe kompilacji dla gałęzi roboczej, należy wybrać **kompilacje** strony **Team Explorer**i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="a1791-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="a1791-215">Otwórz **ustawienia źródła** kartę.</span><span class="sxs-lookup"><span data-stu-id="a1791-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="a1791-216">W obszarze **monitorowane gałęzi dla ciągłej integracji i kompilacji**, wybierz **kliknij tutaj, aby dodać nowy wiersz**.</span><span class="sxs-lookup"><span data-stu-id="a1791-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="a1791-217">Określ gałęzi, z której zostały utworzone, takich jak system plików refs/głowic/pracy.</span><span class="sxs-lookup"><span data-stu-id="a1791-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="a1791-218">Zmiany w kodzie, otwórz menu skrótów zmienionego pliku, a następnie wybierz **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="a1791-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="a1791-219">Wybierz **niezsynchronizowane zatwierdzeń** łącza, a następnie wybierz pozycję **synchronizacji** przycisk lub **Push** łącza w celu skopiowania zmiany z kopią gałąź pracy w Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1791-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="a1791-220">Przejdź do **kompilacje** wyświetlić i Znajdź kompilacji, który właśnie został wywołany gałąź roboczą.</span><span class="sxs-lookup"><span data-stu-id="a1791-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1791-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1791-221">Next steps</span></span>
<span data-ttu-id="a1791-222">Aby dowiedzieć się więcej porad na przy użyciu narzędzia Git w usłudze Visual Studio Team Services, zobacz [opracowanie i udostępnianie kodu w programie Visual Studio w usłudze Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) oraz informacji dotyczących korzystania z repozytorium Git, który nie jest zarządzany przez program Visual Studio Team Services do publikowania na platformie Azure, zobacz [ciągłe wdrażanie w usłudze Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a1791-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="a1791-223">Aby uzyskać więcej informacji o programie Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="a1791-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
