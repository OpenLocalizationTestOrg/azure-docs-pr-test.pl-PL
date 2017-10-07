---
title: dostarczanie aaaContinuous z Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure programu Visual Studio Team Services projekty zespołowe tooautomatically tworzenia i wdrażania toohello funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="5d833-103">TooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5d833-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="5d833-104">Możesz skonfigurować kompilację tooautomatically projektów zespołowych Visual Studio Team Services i wdrażanie aplikacji sieci web tooAzure lub usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5d833-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="5d833-105">(Informacji na temat sposobu tooset kompilacji ciągłego konfigurację i wdrażanie przy użyciu systemu *lokalnymi* Team Foundation Server, zobacz [ciągłego dostarczania dla usług w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="5d833-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="5d833-106">W tym samouczku założono, że masz program Visual Studio 2013 i hello zainstalowany zestaw SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5d833-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="5d833-107">Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając hello **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj hello zestawu Azure SDK w [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="5d833-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="5d833-108">Należy toocomplete konta usługi Visual Studio Team Services w tym samouczku: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="5d833-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="5d833-109">tooset się tooautomatically usługi chmury tworzenie i wdrażanie tooAzure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="5d833-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="5d833-110">1: Tworzenie projektu zespołowego</span><span class="sxs-lookup"><span data-stu-id="5d833-110">1: Create a team project</span></span>
<span data-ttu-id="5d833-111">Postępuj zgodnie z instrukcjami hello [tutaj](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate Twojego zespołu projektu i połączyć ją tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d833-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="5d833-112">W tym przewodniku przyjęto założenie, że używasz kontroli wersji typu Team Foundation (TFVC) jako rozwiązania do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="5d833-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="5d833-113">Jeśli chcesz toouse Git kontroli wersji, zobacz [wersji Git hello tego przewodnika](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="5d833-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="5d833-114">2: Sprawdź w formancie toosource projektu</span><span class="sxs-lookup"><span data-stu-id="5d833-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="5d833-115">W programie Visual Studio Otwórz rozwiązanie hello mają toodeploy lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="5d833-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="5d833-116">Możesz wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacja) przez hello następujące kroki w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="5d833-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="5d833-117">Jeśli toocreate nowe rozwiązanie, należy utworzyć nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5d833-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="5d833-118">Upewnij się, że hello elementy docelowe projektu platformy .NET Framework 4 lub 4.5, a w przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web platformy ASP.NET MVC i roli proces roboczy i wybierz polecenie aplikacji internetowej dla roli sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="5d833-119">Po wyświetleniu monitu wybierz **aplikacji internetowej**.</span><span class="sxs-lookup"><span data-stu-id="5d833-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="5d833-120">Jeśli chcesz toocreate aplikacji sieci web, wybierz szablon projektu aplikacji sieci Web ASP.NET hello, a następnie wybierz MVC.</span><span class="sxs-lookup"><span data-stu-id="5d833-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="5d833-121">Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5d833-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5d833-122">Visual Studio Team Services obsługuje tylko CI wdrożenia aplikacji sieci Web w usłudze Visual Studio w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="5d833-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="5d833-123">Projekt witryny sieci Web jest poza zakresem.</span><span class="sxs-lookup"><span data-stu-id="5d833-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="5d833-124">Otwórz menu kontekstowe hello hello rozwiązania i wybierz polecenie **tooSource rozwiązania Dodaj formant**.</span><span class="sxs-lookup"><span data-stu-id="5d833-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="5d833-125">Zaakceptuj lub zmień ustawienia domyślne hello i wybierz hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d833-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="5d833-126">Po zakończeniu procesu hello ikony kontroli źródła są wyświetlane w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="5d833-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="5d833-127">Otwórz menu skrótów hello hello rozwiązania i wybierz polecenie **Zaewidencjonuj**.</span><span class="sxs-lookup"><span data-stu-id="5d833-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="5d833-128">W hello **oczekujących zmian** obszar **Team Explorer**, wpisz komentarz do zaewidencjonowania hello i wybierz hello **Zaewidencjonuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d833-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="5d833-129">Należy zwrócić uwagę tooinclude opcje hello lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="5d833-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="5d833-130">Jeśli to konieczne, zmian są wyłączone, wybierz hello **obejmują wszystkie** łącza.</span><span class="sxs-lookup"><span data-stu-id="5d833-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="5d833-131">3: łączenie hello tooAzure projektu</span><span class="sxs-lookup"><span data-stu-id="5d833-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="5d833-132">Teraz, gdy masz projektu zespołowego VS Team Services z kodu źródłowego w nim są gotowe tooconnect Twojego zespołu projektu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5d833-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="5d833-133">W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając hello  **+**  ikonę w lewy dolny hello i wybierając polecenie **usługiwchmurze** lub **sieci Web aplikacji** , a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="5d833-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="5d833-134">Wybierz hello **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.</span><span class="sxs-lookup"><span data-stu-id="5d833-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="5d833-135">W Kreatorze hello hello nazwę konta usługi Visual Studio Team Services w polu tekstowym hello i kliknąć przycisk hello **autoryzować teraz** łącza.</span><span class="sxs-lookup"><span data-stu-id="5d833-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="5d833-136">Użytkownik może zostać poproszony toosign w.</span><span class="sxs-lookup"><span data-stu-id="5d833-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="5d833-137">W hello **żądania połączenia** podręczne okno dialogowe, wybierz hello **Akceptuj** tooauthorize przycisk Azure tooconfigure Twojego zespołu projektu w programie VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="5d833-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="5d833-138">Po autoryzacji zakończy się powodzeniem, użytkownik widzi listy rozwijanej zawierającego listę projektach zespołowych Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="5d833-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="5d833-139">Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach hello hello, a następnie wybierz przycisk znacznika wyboru hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="5d833-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="5d833-140">Po projektu, pojawi się instrukcje dotyczące ewidencjonowania projektu zespołowego Visual Studio Team Services tooyour zmiany.</span><span class="sxs-lookup"><span data-stu-id="5d833-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="5d833-141">Na następnego zaewidencjonowania Visual Studio Team Services Skompiluj i wdróż tooAzure Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="5d833-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="5d833-142">Spróbuj teraz tego klikając hello **Zaewidencjonuj, z programu Visual Studio** połączyć, a następnie hello **Uruchom Visual Studio** link (lub równoważne hello **programu Visual Studio** u dołu hello Witaj ekranu portalu).</span><span class="sxs-lookup"><span data-stu-id="5d833-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="5d833-143">4: wyzwolenia kompilowania i wdrożenie projektu</span><span class="sxs-lookup"><span data-stu-id="5d833-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="5d833-144">W programie Visual Studio **Team Explorer**, wybierz hello **Eksploratora kontroli źródła** łącza.</span><span class="sxs-lookup"><span data-stu-id="5d833-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="5d833-145">Przejdź do pliku rozwiązania tooyour i otwórz go.</span><span class="sxs-lookup"><span data-stu-id="5d833-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="5d833-146">W **Eksploratora rozwiązań**, otwarcie pliku i go zmienić.</span><span class="sxs-lookup"><span data-stu-id="5d833-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="5d833-147">Na przykład zmienić plik hello `_Layout.cshtml` w obszarze widoki hello\\udostępniony folder w roli sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="5d833-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="5d833-148">Edytuj logo hello hello witryny i wybierz **Ctrl + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="5d833-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="5d833-149">W **Team Explorer**, wybierz hello **oczekujących zmian** łącza.</span><span class="sxs-lookup"><span data-stu-id="5d833-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="5d833-150">Wprowadź komentarz, a następnie wybierz pozycję hello **Zaewidencjonuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d833-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="5d833-151">Wybierz hello **macierzystego** toohello tooreturn przycisk **Team Explorer** strony głównej.</span><span class="sxs-lookup"><span data-stu-id="5d833-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="5d833-152">Wybierz hello **kompilacje** hello tooview łącze kompilacje w toku.</span><span class="sxs-lookup"><span data-stu-id="5d833-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="5d833-153">**Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="5d833-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="5d833-154">Kliknij dwukrotnie nazwę hello hello kompilacji w toku tooview szczegółowy dziennik w miarę postępów kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="5d833-155">Podczas kompilacji hello jest w toku, Przyjrzyjmy się hello definicji kompilacji, który został utworzony, gdy są połączone TFS tooAzure przy użyciu Kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="5d833-156">Otwórz menu skrótów powitania dla definicji kompilacji hello i wybierz polecenie **edycji definicji kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="5d833-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="5d833-157">W hello **wyzwalacza** kartę, zobaczysz, że hello definicji kompilacji jest domyślnie toobuild na każdym zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="5d833-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="5d833-158">W hello **procesu** karcie widać środowiska wdrażania hello jest ustawiona na nazwę toohello Twojego chmury usługi lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5d833-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="5d833-159">Podczas pracy z aplikacjami sieci web, właściwości hello, widocznej może się różnić z tymi, które przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5d833-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="5d833-160">Określ wartości dla właściwości hello, jeśli chcesz, aby wartości innej niż domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="5d833-161">Witaj właściwości publikowania platformy Azure znajdują się w hello **wdrożenia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5d833-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="5d833-162">Witaj poniższej tabeli przedstawiono dostępne właściwości hello hello **wdrożenia** sekcji:</span><span class="sxs-lookup"><span data-stu-id="5d833-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="5d833-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d833-163">Property</span></span> | <span data-ttu-id="5d833-164">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="5d833-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5d833-165">Zezwalaj na niezaufane certyfikaty</span><span class="sxs-lookup"><span data-stu-id="5d833-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="5d833-166">W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny.</span><span class="sxs-lookup"><span data-stu-id="5d833-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="5d833-167">Zezwalaj na uaktualnienie</span><span class="sxs-lookup"><span data-stu-id="5d833-167">Allow Upgrade</span></span> |<span data-ttu-id="5d833-168">Umożliwia tooupdate wdrożenia hello istniejącego wdrożenia zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="5d833-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="5d833-169">Zachowuje hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5d833-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="5d833-170">Nie usuwaj</span><span class="sxs-lookup"><span data-stu-id="5d833-170">Do Not Delete</span></span> |<span data-ttu-id="5d833-171">Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona).</span><span class="sxs-lookup"><span data-stu-id="5d833-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="5d833-172">Ścieżka tooDeployment ustawienia</span><span class="sxs-lookup"><span data-stu-id="5d833-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="5d833-173">Witaj ścieżki tooyour .pubxml pliku dla aplikacji sieci web, toohello względną głównego folderu repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="5d833-174">Ignorowane dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5d833-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="5d833-175">Środowisko wdrażania SharePoint</span><span class="sxs-lookup"><span data-stu-id="5d833-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="5d833-176">Witaj takie same jak nazwa usługi hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="5d833-177">Środowisko wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5d833-177">Azure Deployment Environment</span></span> |<span data-ttu-id="5d833-178">Witaj aplikacji lub w chmurze nazwę usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="5d833-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="5d833-179">Jeśli używasz wielu konfiguracji usługi (.cscfg pliki), można będzie określić konfigurację żądanej usługi hello w hello **kompilacji, zaawansowane, argumenty programu MSBuild** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="5d833-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="5d833-180">Na przykład toouse ServiceConfiguration.Test.cscfg, ustawić argumenty programu MSBuild opcji wiersza `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="5d833-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="5d833-181">Do tego czasu kompilacji powinien zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5d833-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="5d833-182">Dwukrotne kliknięcie nazwy kompilacji hello Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="5d833-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="5d833-183">W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), można wyświetlić hello skojarzone wdrożenie na powitania **wdrożeń** karcie po wybraniu hello przemieszczania środowiska.</span><span class="sxs-lookup"><span data-stu-id="5d833-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="5d833-184">Adres URL witryny tooyour przeglądania.</span><span class="sxs-lookup"><span data-stu-id="5d833-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="5d833-185">Dla aplikacji sieci web, wystarczy kliknąć hello **Przeglądaj** przycisk na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="5d833-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="5d833-186">Usługi w chmurze, wybierz adres URL hello hello **szybki przegląd** sekcji hello **pulpitu nawigacyjnego** strony zawierającej hello środowiska przemieszczania dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5d833-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="5d833-187">Wdrożenia z ciągłej integracji usług w chmurze są środowiska przemieszczania opublikowanych toohello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5d833-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="5d833-188">Można zmienić to ustawienie hello **alternatywny środowiska usługi w chmurze** właściwości zbyt**produkcji**.</span><span class="sxs-lookup"><span data-stu-id="5d833-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="5d833-189">Ten zrzut ekranu pokazuje gdzie hello na stronie pulpitu nawigacyjnego usługi chmury hello jest adres URL witryny.</span><span class="sxs-lookup"><span data-stu-id="5d833-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="5d833-190">Na nowej karcie przeglądarki zostanie otwarty tooreveal uruchomionej witryny.</span><span class="sxs-lookup"><span data-stu-id="5d833-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="5d833-191">Dla usług w chmurze wprowadzenie innych zmian tooyour projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="5d833-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="5d833-192">Witaj najnowszego oznaczony jako aktywny.</span><span class="sxs-lookup"><span data-stu-id="5d833-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="5d833-193">5: należy ponownie wdrożyć wcześniejszą kompilację</span><span class="sxs-lookup"><span data-stu-id="5d833-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="5d833-194">Ten krok ma zastosowanie toocloud usług i jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="5d833-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="5d833-195">W hello klasycznego portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz hello **ponownie wdrożyć** przycisk toorewind tooan Twojego lokacji do wcześniej w zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="5d833-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="5d833-196">Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5d833-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="5d833-197">6: Zmień hello wdrożenia produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="5d833-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="5d833-198">Ten krok ma zastosowanie tylko toocloud usługi, nie aplikacje sieci web.</span><span class="sxs-lookup"><span data-stu-id="5d833-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="5d833-199">Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska produkcyjnego toohello dla hello przemieszczania, wybierając hello **wymiany** przycisku na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5d833-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="5d833-200">Hello nowo wdrożone środowiska przemieszczania jest awansowana tooProduction i hello poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="5d833-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="5d833-201">Hello aktywnych wdrożeń mogą być różne dla środowisk przemieszczania i hello produkcji, ale Historia wdrażania hello ostatnie kompilacji jest hello sama niezależnie od tego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5d833-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="5d833-202">7: Uruchom testy jednostkowe</span><span class="sxs-lookup"><span data-stu-id="5d833-202">7: Run unit tests</span></span>
<span data-ttu-id="5d833-203">Ten krok ma zastosowanie tylko tooweb aplikacji, nie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5d833-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="5d833-204">tooput bramki jakości, wdrażania, można uruchomić testów jednostkowych i w razie awarii, można zatrzymać hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5d833-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="5d833-205">W programie Visual Studio Dodaj jednostkowy projekt testowy.</span><span class="sxs-lookup"><span data-stu-id="5d833-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="5d833-206">Dodaj odwołania toohello projekt ma tootest.</span><span class="sxs-lookup"><span data-stu-id="5d833-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="5d833-207">Dodanie niektórych testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="5d833-207">Add some unit tests.</span></span> <span data-ttu-id="5d833-208">tooget uruchomiona, spróbuj fikcyjny test, który będzie zawsze przekazuj.</span><span class="sxs-lookup"><span data-stu-id="5d833-208">tooget started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="5d833-209">Przeprowadź edycję definicji kompilacji hello, wybierz hello **procesu** , a następnie rozwiń węzeł hello **testu** węzła.</span><span class="sxs-lookup"><span data-stu-id="5d833-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="5d833-210">Zestaw hello **niepowodzenie kompilacji w przypadku niepowodzenia testu** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5d833-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="5d833-211">Oznacza to, że hello wdrożenia nie występują, chyba że hello testów przebiegu.</span><span class="sxs-lookup"><span data-stu-id="5d833-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="5d833-212">Kolejka jest nowa kompilacja.</span><span class="sxs-lookup"><span data-stu-id="5d833-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="5d833-213">Podczas kompilacji hello jest kontynuowanie, sprawdzić postęp.</span><span class="sxs-lookup"><span data-stu-id="5d833-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="5d833-214">Po zakończeniu kompilacji hello Sprawdź hello wyników testu.</span><span class="sxs-lookup"><span data-stu-id="5d833-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="5d833-215">Spróbuj utworzyć test, który zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5d833-215">Try creating a test that will fail.</span></span> <span data-ttu-id="5d833-216">Dodaj nowego testu przez skopiowanie hello pierwszego z nich, zmień jego nazwę, a w komentarz wiersz hello kodu, stwierdzający, że notimplementedexception — jest oczekiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="5d833-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="5d833-217">Sprawdź w tooqueue zmiany hello nowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5d833-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="5d833-218">Wyświetl szczegóły toosee wyników testu hello o niepowodzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="5d833-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="5d833-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d833-219">Next steps</span></span>
<span data-ttu-id="5d833-220">Aby uzyskać więcej informacji na temat testowania w programie Visual Studio Team Services jednostek, zobacz [Uruchom testy jednostkowe w kompilacji](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="5d833-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="5d833-221">Jeśli używasz programu Git, zobacz [udostępnianie kodu w usłudze Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) i [tooAzure ciągłego wdrażania aplikacji usługi](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5d833-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="5d833-222">Aby uzyskać więcej informacji na temat programu Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="5d833-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
