---
title: "aaaDeploy zadań Webjob przy użyciu programu Visual Studio"
description: "Dowiedz się, jak toodeploy tooAzure zadań Webjob Azure Web Apps App Service przy użyciu programu Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="c2ac0-103">Wdrażanie zadań WebJob za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2ac0-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="c2ac0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c2ac0-104">Overview</span></span>
<span data-ttu-id="c2ac0-105">W tym temacie wyjaśniono, jak toouse Visual Studio toodeploy aplikacji konsoli projektu aplikacji sieci web tooa w [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) jako [zadań WebJob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="c2ac0-106">Aby dowiedzieć się jak hello toodeploy zadań Webjob przy użyciu [Azure Portal](https://portal.azure.com), zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="c2ac0-107">Gdy program Visual Studio wdroży projekt aplikacji konsoli włączone zadań Webjob, wykonuje dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="c2ac0-108">Pliki środowiska uruchomieniowego kopie toohello odpowiedni folder w aplikacji sieci web hello (*App_Data/zadania/ciągłego* dla ciągłe zadania Webjob, *App_Data/zadania/wyzwalane* dla zadań Webjob zaplanowanych, jak i na żądanie).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="c2ac0-109">Konfiguruje [zadania harmonogramu Azure](#scheduler) dla zadań Webjob, które są zaplanowane toorun w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="c2ac0-110">(To nie potrzebne do ciągłe zadania Webjob.)</span><span class="sxs-lookup"><span data-stu-id="c2ac0-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="c2ac0-111">Projekt z obsługą zadań Webjob ma powitania po tooit dodanych elementów:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="c2ac0-112">Witaj [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="c2ac0-113">A [zadania webjob publikowania settings.json](#publishsettings) plik zawierający ustawienia wdrażania i harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram przedstawiający, co jest dodawana tooa aplikacji konsoli tooenable wdrożenia jako zadanie WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="c2ac0-115">Można dodać te tooan elementów istniejący projekt aplikacji konsoli lub użyj szablonu toocreate nowy projekt aplikacji konsoli włączone zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="c2ac0-116">Wdróż projekt jako zadanie WebJob samodzielnie lub połączyć ją tooa projektu sieci web tak, aby automatycznie wdraża przy każdym wdrożeniem hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="c2ac0-117">projekty toolink programu Visual Studio zawiera nazwę hello hello włączone zadań Webjob projektu w [list.json webjob](#webjobslist) plik w projekcie sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagram przedstawiający projektu zadania WebJob łączenie tooweb projektu](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="c2ac0-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c2ac0-119">Prerequisites</span></span>
<span data-ttu-id="c2ac0-120">Funkcje wdrażania zadania Webjob są dostępne w programie Visual Studio, po zainstalowaniu hello Azure SDK dla platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="c2ac0-121">[Zestaw Azure SDK dla platformy .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="c2ac0-122"><a id="convert"></a>Włącz wdrożenie zadań Webjob dla istniejący projekt aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="c2ac0-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="c2ac0-123">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-123">You have two options:</span></span>

* <span data-ttu-id="c2ac0-124">[Włącz automatyczne wdrażanie projektu sieci web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="c2ac0-125">Skonfiguruj istniejący projekt aplikacji konsoli, aby go automatycznie wdraża jako zadanie WebJob podczas wdrażania projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="c2ac0-126">Użyj tej opcji, jeśli chcesz toorun WebJob w hello tej samej aplikacji sieci web, w którym można uruchomić hello związane z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="c2ac0-127">[Włącz wdrożenie bez projektu sieci web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="c2ac0-128">Należy skonfigurować samodzielnie, istniejące toodeploy projekt aplikacji konsoli jako zadanie WebJob z żadnego projektu sieci web tooa łącza.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="c2ac0-129">Ta opcja ma toorun zadania WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="c2ac0-130">Toodo może być to w celu tooscale stanie toobe zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="c2ac0-131"><a id="convertlink"></a>Włącz automatyczne wdrażanie zadań Webjob z projektu sieci web</span><span class="sxs-lookup"><span data-stu-id="c2ac0-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="c2ac0-132">Kliknij prawym przyciskiem myszy projekt sieci web hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **istniejący projekt jako zadanie WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Istniejący projekt jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="c2ac0-134">Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="c2ac0-135">W hello **Nazwa projektu** listy rozwijanej, tooadd projekt aplikacji konsoli wybierz hello jako zadanie WebJob.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Wybieranie projektu w oknie dialogowym Dodawanie zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="c2ac0-137">Zakończenie hello [dodać zadania WebJob Azure](#configure) okna dialogowego, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="c2ac0-138"><a id="convertnolink"></a>Włącz wdrożenie zadań Webjob bez projektu sieci web</span><span class="sxs-lookup"><span data-stu-id="c2ac0-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="c2ac0-139">Kliknij prawym przyciskiem myszy projekt aplikacji konsoli hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** .</span><span class="sxs-lookup"><span data-stu-id="c2ac0-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="c2ac0-141">Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe z hello projekt wybrany w hello **Nazwa projektu** pole.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="c2ac0-142">Zakończenie hello [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="c2ac0-143">Witaj **publikowanie w sieci Web** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="c2ac0-144">Jeśli nie chcesz od razu toopublish, zamknij kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="c2ac0-145">Hello ustawień, które zostały wprowadzone są zapisywane dla należy zbyt[wdrażanie projektu hello](#deploy).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="c2ac0-146"><a id="create"></a>Utwórz nowy projekt z obsługą zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="c2ac0-147">toocreate nowy projekt z obsługą zadań Webjob, można użyć hello konsoli projektu szablonu i włączyć zadania Webjob wdrożenia aplikacji zgodnie z objaśnieniem w [hello poprzedniej sekcji](#convert).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="c2ac0-148">Alternatywnie można użyć szablonu nowy projekt zadania Webjob hello:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="c2ac0-149">Szablon hello zadań Webjob nowy projekt dla niezależnych zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="c2ac0-150">Tworzenie projektu i skonfiguruj go toodeploy przez samego siebie jako zadanie WebJob z żadnego projektu sieci web tooa łącza.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="c2ac0-151">Ta opcja ma toorun zadania WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="c2ac0-152">Toodo może być to w celu tooscale stanie toobe zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="c2ac0-153">Szablon hello zadań Webjob nowego projektu dla projektu sieci web połączonej tooa zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="c2ac0-154">Utwórz projekt, który jest skonfigurowany toodeploy automatycznie jako zadanie WebJob, gdy projekt sieci web w hello wdrożonej tego samego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="c2ac0-155">Użyj tej opcji, jeśli chcesz toorun WebJob w hello tej samej aplikacji sieci web, w którym można uruchomić hello związane z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ac0-156">Szablon nowego projektu zadania Webjob Hello automatycznie instaluje pakiety NuGet i zawiera kod w *Program.cs* dla hello [zestaw SDK zadań Webjob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="c2ac0-157">Jeśli nie chcesz hello toouse zestaw SDK zadań Webjob, usunąć ani zmienić hello `host.RunAndBlock` instrukcji w *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="c2ac0-158"><a id="createnolink"></a>Szablon hello zadań Webjob nowy projekt dla niezależnych zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="c2ac0-159">Kliknij przycisk **pliku** > **nowy projekt**, a następnie w hello **nowy projekt** kliknij okno dialogowe **chmury**  >   **Zadanie WebJob platformy Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Okno dialogowe nowego projektu przedstawiający szablonu zadania WebJob](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="c2ac0-161">Postępuj zgodnie ze wskazówkami hello przedstawiona wcześniej zbyt[upewnij hello projekt aplikacji konsoli niezależne projektu zadania Webjob](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="c2ac0-162"><a id="createlink"></a>Szablon hello zadań Webjob nowego projektu dla projektu sieci web połączonej tooa zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="c2ac0-163">Kliknij prawym przyciskiem myszy projekt sieci web hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Nowy wpis menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="c2ac0-165">Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="c2ac0-166">Zakończenie hello [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="c2ac0-167"><a id="configure"></a>okno dialogowe Dodawanie zadania WebJob Azure Hello</span><span class="sxs-lookup"><span data-stu-id="c2ac0-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="c2ac0-168">Witaj **dodać zadania WebJob Azure** oknie dialogowym można wprowadzić nazwę zadania WebJob hello i uruchom tryb WebJob.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Dodawanie zadania WebJob Azure w oknie dialogowym](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="c2ac0-170">Witaj pola w tym oknie dialogowym odpowiadają toofields na powitania **nowe zadanie** dialogowe hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="c2ac0-171">Aby uzyskać więcej informacji, zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="c2ac0-172">Informacji o wdrażaniu wiersza polecenia, zobacz [Włączanie wiersza polecenia lub ciągłego dostarczania Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="c2ac0-173">Jeśli zdecydujesz się toochange hello typu zadania WebJob i utwórz je ponownie po wdrożeniu zadanie WebJob, konieczne będzie toodelete hello zadań webjob publikowania settings.json pliku.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="c2ac0-174">Spowoduje to Visual Studio Pokaż hello opcje publikowania, dzięki czemu można zmieniać hello typu zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="c2ac0-175">Jeśli zadanie WebJob wdrożyć, a później zmieni hello w trybie uruchamiania z ciągłego ciągłego toonon lub odwrotnie, Visual Studio tworzy nowe zadania WebJob na platformie Azure podczas ponownego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="c2ac0-176">Jeśli zmienisz inne ustawienia harmonogramu, ale pozostaw Uruchom tryb hello takie same lub przełączać się między zaplanowane i na żądanie, aktualizacji programu Visual Studio hello istniejące zadanie zamiast tworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="c2ac0-177"><a id="publishsettings"></a>zadania webjob — Opublikuj settings.json</span><span class="sxs-lookup"><span data-stu-id="c2ac0-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="c2ac0-178">Po skonfigurowaniu aplikacji konsoli dla zadań Webjob wdrożenia programu Visual Studio instaluje hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pakietu i planowania informacji w magazynach *zadania webjob publikowania settings.json*  plik w projekcie hello *właściwości* folderu projektu zadania Webjob hello.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="c2ac0-179">Oto przykład tego pliku:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="c2ac0-180">Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="c2ac0-181">Schemat pliku Hello jest przechowywany w [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) i można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="c2ac0-182"><a id="webjobslist"></a>list.json zadań webjob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="c2ac0-183">Po połączeniu projektu sieci web tooa włączone zadań Webjob projektu programu Visual Studio przechowuje hello Nazwa projektu zadania Webjob hello w *list.json webjob* plik w projekcie sieci web hello *właściwości* folderu.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="c2ac0-184">listy Hello może zawierać wiele projektów zadań Webjob, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c2ac0-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="c2ac0-185">Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="c2ac0-186">Schemat pliku Hello jest przechowywany w [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) i można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="c2ac0-187"><a id="deploy"></a>Wdrażanie projektu zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="c2ac0-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="c2ac0-188">Dołączono tooa projektu sieci web projektu zadania Webjob automatycznie wdraża z hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="c2ac0-189">Aby uzyskać informacje dotyczące wdrażania projektu sieci web, zobacz [jak tooWeb toodeploy aplikacji](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="c2ac0-190">toodeploy projektu zadania Webjob przez siebie, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** .</span><span class="sxs-lookup"><span data-stu-id="c2ac0-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="c2ac0-192">Niezależnie od zadania WebJob hello sam **publikowanie w sieci Web** kreatora, który jest używany dla projektów sieci web jest wyświetlana, ale mniej toochange dostępne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="c2ac0-193"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2ac0-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="c2ac0-194">Ten artykuł zawiera opis sposobu toodeploy zadań Webjob za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2ac0-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="c2ac0-195">Aby uzyskać więcej informacji na temat toodeploy zadań Webjob Azure, zobacz temat [zadań Webjob Azure - zalecane zasoby — wdrożenia](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="c2ac0-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

