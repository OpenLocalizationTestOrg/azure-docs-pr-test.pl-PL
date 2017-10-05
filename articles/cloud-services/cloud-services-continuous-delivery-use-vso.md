---
title: "Ciągłego dostarczania z Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania programu Visual Studio Team Services projektów zespołowych do automatycznego tworzenia i wdrażania dla funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="05931-103">Ciągłe dostarczanie na platformę Azure za pomocą usługi Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="05931-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="05931-104">Można skonfigurować programu Visual Studio Team Services projektów zespołowych do automatycznego tworzenia i wdrażania aplikacji sieci web platformy Azure lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="05931-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="05931-105">(Informacje o tym, jak skonfigurować ciągłe kompilacji i wdrożyć przy użyciu systemu *lokalnymi* Team Foundation Server, zobacz [ciągłego dostarczania dla usług w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="05931-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="05931-106">Ten samouczek zakłada, że używasz programu Visual Studio 2013 i zainstalować zestaw Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="05931-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="05931-107">Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="05931-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="05931-108">Zainstaluj zestaw Azure SDK z [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="05931-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="05931-109">Musisz mieć konto usługi Visual Studio Team Services do ukończenia tego samouczka: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="05931-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="05931-110">Aby skonfigurować usługi w chmurze spowoduje automatyczne utworzenie i wdrażanie na platformie Azure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="05931-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="05931-111">1: Tworzenie projektu zespołowego</span><span class="sxs-lookup"><span data-stu-id="05931-111">1: Create a team project</span></span>
<span data-ttu-id="05931-112">Postępuj zgodnie z instrukcjami [tutaj](http://go.microsoft.com/fwlink/?LinkId=512980) do tworzenia projektu zespołowego i połączyć je z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05931-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="05931-113">W tym przewodniku przyjęto założenie, że używasz kontroli wersji typu Team Foundation (TFVC) jako rozwiązania do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="05931-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="05931-114">Jeśli chcesz użyć do kontroli wersji Git, zobacz [wersji Git tego przewodnika](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="05931-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="05931-115">2: projektów z kontrolą źródła</span><span class="sxs-lookup"><span data-stu-id="05931-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="05931-116">W programie Visual Studio Otwórz rozwiązanie, które mają zostać wdrożone lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="05931-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="05931-117">Wykonując kroki opisane w tym przewodniku można wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacji).</span><span class="sxs-lookup"><span data-stu-id="05931-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="05931-118">Jeśli chcesz utworzyć nowe rozwiązanie, Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="05931-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="05931-119">Upewnij się, że projekt jest przeznaczony dla platformy .NET Framework 4 lub 4.5, a w przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web platformy ASP.NET MVC i roli proces roboczy i wybierz polecenie aplikacji internetowej dla roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="05931-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="05931-120">Po wyświetleniu monitu wybierz **aplikacji internetowej**.</span><span class="sxs-lookup"><span data-stu-id="05931-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="05931-121">Jeśli chcesz utworzyć aplikację sieci web, wybierz szablon projektu aplikacji sieci Web ASP.NET, a następnie wybierz MVC.</span><span class="sxs-lookup"><span data-stu-id="05931-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="05931-122">Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="05931-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05931-123">Visual Studio Team Services obsługuje tylko CI wdrożenia aplikacji sieci Web w usłudze Visual Studio w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="05931-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="05931-124">Projekt witryny sieci Web jest poza zakresem.</span><span class="sxs-lookup"><span data-stu-id="05931-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="05931-125">Otwórz menu kontekstowe dla rozwiązania i wybierz polecenie **Dodaj rozwiązanie do kontroli źródła**.</span><span class="sxs-lookup"><span data-stu-id="05931-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="05931-126">Zaakceptuj lub zmień ustawienia domyślne i wybierz **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05931-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="05931-127">Po zakończeniu procesu ikony kontroli źródła są wyświetlane w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="05931-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="05931-128">Otwórz menu skrótów dla rozwiązania i wybierz polecenie **Zaewidencjonuj**.</span><span class="sxs-lookup"><span data-stu-id="05931-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="05931-129">W **oczekujących zmian** obszar **Team Explorer**, wpisz komentarz do zaewidencjonowania i wybierz **Zaewidencjonuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05931-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="05931-130">Należy pamiętać, opcje, aby dołączyć lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="05931-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="05931-131">Jeśli to konieczne, zmian są wyłączone, wybierz **obejmują wszystkie** łącza.</span><span class="sxs-lookup"><span data-stu-id="05931-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="05931-132">3: Połącz projekt na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="05931-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="05931-133">Teraz, gdy masz projektu zespołowego VS Team Services z kodu źródłowego w nim można przystąpić do projektu zespołowego połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="05931-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="05931-134">W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając  **+**  ikony na dole po lewej i wybierając polecenie **usługi w chmurze**lub **sieci Web aplikacji** , a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="05931-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="05931-135">Wybierz **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.</span><span class="sxs-lookup"><span data-stu-id="05931-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="05931-136">W kreatorze, wpisz nazwę konta usługi Visual Studio Team Services w pliku tekstowym i kliknij przycisk **autoryzować teraz** łącza.</span><span class="sxs-lookup"><span data-stu-id="05931-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="05931-137">Może być konieczne podanie do logowania.</span><span class="sxs-lookup"><span data-stu-id="05931-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="05931-138">W **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** przycisk, aby autoryzować Azure, aby skonfigurować projekt zespołowy w programie VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="05931-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="05931-139">Po autoryzacji zakończy się powodzeniem, użytkownik widzi listy rozwijanej zawierającego listę projektach zespołowych Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="05931-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="05931-140">Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach, a następnie wybierz przycisk wyboru w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="05931-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="05931-141">Po projektu, pojawi się instrukcje dotyczące ewidencjonowania zmiany do projektu zespołowego Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="05931-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="05931-142">Na następnym zaewidencjonowania Visual Studio Team Services skompiluje oraz wdrażanie projektu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="05931-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="05931-143">Spróbuj to teraz po kliknięciu **Zaewidencjonuj, z programu Visual Studio** łącza, a następnie **Uruchom Visual Studio** łącza (lub równoważne **Visual Studio** przycisk w dolnej części ekran portalu).</span><span class="sxs-lookup"><span data-stu-id="05931-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="05931-144">4: wyzwolenia kompilowania i wdrożenie projektu</span><span class="sxs-lookup"><span data-stu-id="05931-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="05931-145">W programie Visual Studio **Team Explorer**, wybierz **Eksploratora kontroli źródła** łącza.</span><span class="sxs-lookup"><span data-stu-id="05931-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="05931-146">Przejdź do pliku rozwiązania, a następnie otwórz go.</span><span class="sxs-lookup"><span data-stu-id="05931-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="05931-147">W **Eksploratora rozwiązań**, otwarcie pliku i go zmienić.</span><span class="sxs-lookup"><span data-stu-id="05931-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="05931-148">Na przykład zmienić plik `_Layout.cshtml` pod widokami\\udostępniony folder w roli sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="05931-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="05931-149">Edytuj logo witryny i wybierz **Ctrl + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="05931-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="05931-150">W **Team Explorer**, wybierz **oczekujących zmian** łącza.</span><span class="sxs-lookup"><span data-stu-id="05931-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="05931-151">Wprowadź komentarz, a następnie wybierz pozycję **Zaewidencjonuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05931-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="05931-152">Wybierz **macierzystego** przycisk, aby powrócić do **Team Explorer** strony głównej.</span><span class="sxs-lookup"><span data-stu-id="05931-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="05931-153">Wybierz **kompilacje** łącze, aby wyświetlić kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="05931-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="05931-154">**Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="05931-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="05931-155">Kliknij dwukrotnie nazwę kompilacji w toku, aby wyświetlić szczegółowy dziennik w trakcie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05931-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="05931-156">Gdy kompilacja jest w toku, Przyjrzyjmy się definicję kompilacji, który został utworzony, gdy są połączone TFS na platformie Azure za pomocą kreatora.</span><span class="sxs-lookup"><span data-stu-id="05931-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="05931-157">Otwórz menu skrótów dla definicji kompilacji i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="05931-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="05931-158">W **wyzwalacza** kartę, zobaczysz, że definicji kompilacji jest ustawiony na każdym zaewidencjonowania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="05931-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="05931-159">W **procesu** karcie widać środowiska wdrażania jest ustawiona na nazwę Twojej chmury usługi lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="05931-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="05931-160">Podczas pracy z aplikacjami sieci web, właściwości, które widać może się różnić od tych przedstawionych w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="05931-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="05931-161">Określ wartości dla właściwości, jeśli chcesz, aby wartości innej niż wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="05931-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="05931-162">Właściwości publikowania platformy Azure są w **wdrożenia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="05931-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="05931-163">W poniższej tabeli przedstawiono dostępne właściwości w **wdrożenia** sekcji:</span><span class="sxs-lookup"><span data-stu-id="05931-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="05931-164">Właściwość</span><span class="sxs-lookup"><span data-stu-id="05931-164">Property</span></span> | <span data-ttu-id="05931-165">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="05931-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="05931-166">Zezwalaj na niezaufane certyfikaty</span><span class="sxs-lookup"><span data-stu-id="05931-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="05931-167">W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny.</span><span class="sxs-lookup"><span data-stu-id="05931-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="05931-168">Zezwalaj na uaktualnienie</span><span class="sxs-lookup"><span data-stu-id="05931-168">Allow Upgrade</span></span> |<span data-ttu-id="05931-169">Umożliwia wdrożenie, aby zaktualizować istniejące wdrożenie zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="05931-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="05931-170">Zachowuje adres IP.</span><span class="sxs-lookup"><span data-stu-id="05931-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="05931-171">Nie usuwaj</span><span class="sxs-lookup"><span data-stu-id="05931-171">Do Not Delete</span></span> |<span data-ttu-id="05931-172">Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona).</span><span class="sxs-lookup"><span data-stu-id="05931-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="05931-173">Ścieżka do ustawienia wdrożenia</span><span class="sxs-lookup"><span data-stu-id="05931-173">Path to Deployment Settings</span></span> |<span data-ttu-id="05931-174">Ścieżka do pliku .pubxml dla aplikacji sieci web, względem głównego folderu repozytorium.</span><span class="sxs-lookup"><span data-stu-id="05931-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="05931-175">Ignorowane dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="05931-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="05931-176">Środowisko wdrażania SharePoint</span><span class="sxs-lookup"><span data-stu-id="05931-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="05931-177">Taka sama jak nazwa usługi.</span><span class="sxs-lookup"><span data-stu-id="05931-177">The same as the service name.</span></span> |
    | <span data-ttu-id="05931-178">Środowisko wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="05931-178">Azure Deployment Environment</span></span> |<span data-ttu-id="05931-179">Nazwa sieci web aplikacji lub w chmurze usługi.</span><span class="sxs-lookup"><span data-stu-id="05931-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="05931-180">Jeśli używasz wielu konfiguracji usługi (.cscfg pliki), można będzie określić konfigurację żądanej usługi w **kompilacji, zaawansowane, argumenty programu MSBuild** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="05931-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="05931-181">Na przykład, aby używać ServiceConfiguration.Test.cscfg, ustaw argumenty programu MSBuild opcji wiersza `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="05931-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="05931-182">Do tego czasu kompilacji powinien zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="05931-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="05931-183">Dwukrotne kliknięcie nazwy kompilacji programu Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="05931-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="05931-184">W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), skojarzone wdrożenia można obejrzeć w **wdrożeń** karcie, gdy środowisko tymczasowe jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="05931-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="05931-185">Przejdź do adresu URL witryny.</span><span class="sxs-lookup"><span data-stu-id="05931-185">Browse to your site's URL.</span></span> <span data-ttu-id="05931-186">Dla aplikacji sieci web, wystarczy kliknąć **Przeglądaj** przycisk paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="05931-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="05931-187">Usługi w chmurze, wybierz adres URL w **szybki przegląd** sekcji **pulpitu nawigacyjnego** strony zawierającej środowiska przemieszczania dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="05931-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="05931-188">Wdrożenia z ciągłej integracji usług w chmurze są publikowane w środowisku przemieszczania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="05931-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="05931-189">Możesz zmienić to ustawienie **alternatywny środowiska usługi w chmurze** właściwości **produkcji**.</span><span class="sxs-lookup"><span data-stu-id="05931-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="05931-190">Zrzut ekranu przedstawia, gdy adres URL witryny jest na stronie pulpitu nawigacyjnego usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="05931-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="05931-191">Na nowej karcie przeglądarki będą otwierane w celu wyświetlenia uruchomionej witryny.</span><span class="sxs-lookup"><span data-stu-id="05931-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="05931-192">Dla usług w chmurze, jeśli inne zmiany do projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="05931-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="05931-193">Najnowszego oznaczony jako aktywny.</span><span class="sxs-lookup"><span data-stu-id="05931-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="05931-194">5: należy ponownie wdrożyć wcześniejszą kompilację</span><span class="sxs-lookup"><span data-stu-id="05931-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="05931-195">Ten krok ma zastosowanie do usługi w chmurze i jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="05931-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="05931-196">W klasycznym portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz **ponownie wdrożyć** przycisku do tyłu witryny wcześniej zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="05931-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="05931-197">Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="05931-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="05931-198">6: Zmień wdrożenia produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="05931-198">6: Change the Production deployment</span></span>
<span data-ttu-id="05931-199">Ten krok ma zastosowanie tylko do usługi w chmurze, nie aplikacje sieci web.</span><span class="sxs-lookup"><span data-stu-id="05931-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="05931-200">Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska przemieszczania do środowiska produkcyjnego, wybierając **wymiany** przycisk w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="05931-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="05931-201">Nowo wdrożonym środowiska przemieszczania jest podwyższany do środowiska produkcyjnego i poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="05931-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="05931-202">Aktywne wdrożenie może się różnić w produkcyjne i przejściowe środowisk, ale Historia wdrażania ostatnie kompilacji jest taka sama niezależnie od środowiska.</span><span class="sxs-lookup"><span data-stu-id="05931-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="05931-203">7: Uruchom testy jednostkowe</span><span class="sxs-lookup"><span data-stu-id="05931-203">7: Run unit tests</span></span>
<span data-ttu-id="05931-204">Ten krok dotyczy tylko sieci web apps, nie usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="05931-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="05931-205">Aby zawiesić bramki jakości wdrożenia, można uruchomić testów jednostkowych i w razie awarii, można zatrzymać wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="05931-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="05931-206">W programie Visual Studio Dodaj jednostkowy projekt testowy.</span><span class="sxs-lookup"><span data-stu-id="05931-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="05931-207">Dodaj odwołania projektu do projektu, który ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="05931-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="05931-208">Dodanie niektórych testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="05931-208">Add some unit tests.</span></span> <span data-ttu-id="05931-209">Aby rozpocząć, spróbuj fikcyjny test, który będzie zawsze przekazuj.</span><span class="sxs-lookup"><span data-stu-id="05931-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="05931-210">Przeprowadź edycję definicji kompilacji, wybierz **procesu** , a następnie rozwiń węzeł **testu** węzła.</span><span class="sxs-lookup"><span data-stu-id="05931-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="05931-211">Ustaw **niepowodzenie kompilacji w przypadku niepowodzenia testu** na wartość True.</span><span class="sxs-lookup"><span data-stu-id="05931-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="05931-212">Oznacza to, że wdrożenie nie zostanie przeprowadzone, chyba, że testy zostały zaliczone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="05931-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="05931-213">Kolejka jest nowa kompilacja.</span><span class="sxs-lookup"><span data-stu-id="05931-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="05931-214">Podczas kompilacji jest kontynuowanie, sprawdzić postęp.</span><span class="sxs-lookup"><span data-stu-id="05931-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="05931-215">Po zakończeniu kompilacji, sprawdź wyniki testu.</span><span class="sxs-lookup"><span data-stu-id="05931-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="05931-216">Spróbuj utworzyć test, który zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="05931-216">Try creating a test that will fail.</span></span> <span data-ttu-id="05931-217">Dodaj nowego testu przez skopiowanie pierwsza z nich, zmień jego nazwę, a w komentarz wiersz kodu, stwierdzający, że notimplementedexception — jest oczekiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="05931-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="05931-218">Zaewidencjonuj zmiany do kolejki nowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05931-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="05931-219">Wyświetlić wyniki testów, aby zobaczyć szczegóły dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="05931-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="05931-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05931-220">Next steps</span></span>
<span data-ttu-id="05931-221">Aby uzyskać więcej informacji na temat testowania w programie Visual Studio Team Services jednostek, zobacz [Uruchom testy jednostkowe w kompilacji](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="05931-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="05931-222">Jeśli używasz programu Git, zobacz [udostępnianie kodu w usłudze Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) i [ciągłe wdrażanie w usłudze Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="05931-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="05931-223">Aby uzyskać więcej informacji na temat programu Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="05931-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
