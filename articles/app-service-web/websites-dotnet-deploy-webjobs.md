---
title: "Wdrażanie zadań WebJob za pomocą programu Visual Studio"
description: "Dowiedz się, jak wdrożyć zadań Webjob Azure do usługi Azure App Service aplikacje sieci Web przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="8e768-103">Wdrażanie zadań WebJob za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e768-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="8e768-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8e768-104">Overview</span></span>
<span data-ttu-id="8e768-105">W tym temacie wyjaśniono, jak używać programu Visual Studio, aby wdrożyć projekt aplikacji konsoli w aplikacji sieci web w [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) jako [zadań WebJob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="8e768-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="8e768-106">Informacje o sposobie wdrażania przy użyciu zadań Webjob [Azure Portal](https://portal.azure.com), zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="8e768-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="8e768-107">Gdy program Visual Studio wdroży projekt aplikacji konsoli włączone zadań Webjob, wykonuje dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="8e768-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="8e768-108">Kopiuje pliki środowiska uruchomieniowego do odpowiedniego folderu w aplikacji sieci web (*App_Data/zadania/ciągłego* dla ciągłe zadania Webjob, *App_Data/zadania/wyzwalane* dla zadań Webjob zaplanowanych, jak i na żądanie).</span><span class="sxs-lookup"><span data-stu-id="8e768-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="8e768-109">Konfiguruje [zadania harmonogramu Azure](#scheduler) dla zadań Webjob, które są zaplanowane do uruchomienia w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="8e768-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="8e768-110">(To nie potrzebne do ciągłe zadania Webjob.)</span><span class="sxs-lookup"><span data-stu-id="8e768-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="8e768-111">Projekt z obsługą zadań Webjob ma następujące elementy dodane do niej:</span><span class="sxs-lookup"><span data-stu-id="8e768-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="8e768-112">[Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e768-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="8e768-113">A [zadania webjob publikowania settings.json](#publishsettings) plik zawierający ustawienia wdrażania i harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="8e768-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram przedstawiający, co jest dodawany do aplikacji konsoli, aby umożliwić wdrożenie jako zadanie WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="8e768-115">Można dodać te elementy do istniejącego projektu aplikacji konsoli lub użyj szablonu, aby utworzyć nowy projekt aplikacji konsoli włączone zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="8e768-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="8e768-116">Wdróż projekt jako zadanie WebJob samodzielnie lub połączyć ją z projektu sieci web tak, aby automatycznie wdraża zawsze, gdy wdrażanie projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="8e768-117">Aby powiązać projekty, Visual Studio zawiera nazwę projektu włączone zadań Webjob w [list.json webjob](#webjobslist) plik w projekcie sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram przedstawiający projektu zadania WebJob łączenie do projektu sieci web](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="8e768-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8e768-119">Prerequisites</span></span>
<span data-ttu-id="8e768-120">Funkcje wdrażania zadania Webjob są dostępne w programie Visual Studio, podczas instalowania zestawu Azure SDK dla platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="8e768-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="8e768-121">[Zestaw Azure SDK dla platformy .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8e768-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="8e768-122"><a id="convert"></a>Włącz wdrożenie zadań Webjob dla istniejący projekt aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="8e768-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="8e768-123">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="8e768-123">You have two options:</span></span>

* <span data-ttu-id="8e768-124">[Włącz automatyczne wdrażanie projektu sieci web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="8e768-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="8e768-125">Skonfiguruj istniejący projekt aplikacji konsoli, aby go automatycznie wdraża jako zadanie WebJob podczas wdrażania projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="8e768-126">Użyj tej opcji, jeśli chcesz uruchomić WebJob w tej samej aplikacji sieci web, w którym można uruchomić aplikacji sieci web pokrewne.</span><span class="sxs-lookup"><span data-stu-id="8e768-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="8e768-127">[Włącz wdrożenie bez projektu sieci web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="8e768-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="8e768-128">Skonfiguruj istniejący projekt aplikacji konsoli, aby wdrożyć jako zadanie WebJob przez siebie, nie łącz do projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="8e768-129">Użyj tej opcji, jeśli chcesz uruchomić zadanie WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="8e768-130">Można to zrobić, aby można było skalowanie zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="8e768-131"><a id="convertlink"></a>Włącz automatyczne wdrażanie zadań Webjob z projektu sieci web</span><span class="sxs-lookup"><span data-stu-id="8e768-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="8e768-132">Kliknij prawym przyciskiem myszy projekt sieci web w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **istniejący projekt jako zadanie WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e768-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Istniejący projekt jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="8e768-134">[Dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8e768-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="8e768-135">W **Nazwa projektu** listy rozwijanej wybierz pozycję projekt aplikacji konsoli do dodania jako zadanie WebJob.</span><span class="sxs-lookup"><span data-stu-id="8e768-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Wybieranie projektu w oknie dialogowym Dodawanie zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="8e768-137">Zakończenie [dodać zadania WebJob Azure](#configure) okna dialogowego, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e768-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="8e768-138"><a id="convertnolink"></a>Włącz wdrożenie zadań Webjob bez projektu sieci web</span><span class="sxs-lookup"><span data-stu-id="8e768-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="8e768-139">Kliknij prawym przyciskiem myszy projekt aplikacji konsoli w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** .</span><span class="sxs-lookup"><span data-stu-id="8e768-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="8e768-141">[Dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe z projekt wybrany w **Nazwa projektu** pole.</span><span class="sxs-lookup"><span data-stu-id="8e768-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="8e768-142">Zakończenie [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e768-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="8e768-143">**Publikowanie w sieci Web** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="8e768-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="8e768-144">Jeśli nie chcesz opublikować natychmiast, zamknąć kreatora.</span><span class="sxs-lookup"><span data-stu-id="8e768-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="8e768-145">Ustawienia, które zostały wprowadzone są zapisywane dla, jeśli chcesz [wdrażanie projektu](#deploy).</span><span class="sxs-lookup"><span data-stu-id="8e768-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="8e768-146"><a id="create"></a>Utwórz nowy projekt z obsługą zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="8e768-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="8e768-147">Aby utworzyć nowy projekt z obsługą zadań Webjob, można użyć szablonu projektu aplikacji Konsolowej i włączyć wdrożenie zadań Webjob, zgodnie z objaśnieniem w [poprzedniej sekcji](#convert).</span><span class="sxs-lookup"><span data-stu-id="8e768-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="8e768-148">Alternatywnie można użyć szablonu nowy projekt zadania Webjob:</span><span class="sxs-lookup"><span data-stu-id="8e768-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="8e768-149">Szablon dla niezależnych zadania WebJob nowy projekt zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="8e768-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="8e768-150">Tworzenie projektu i skonfigurować go do wdrożenia przez samego siebie jako zadanie WebJob z żadnego linku do projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="8e768-151">Użyj tej opcji, jeśli chcesz uruchomić zadanie WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="8e768-152">Można to zrobić, aby można było skalowanie zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="8e768-153">Użyj szablonu nowy projekt zadania Webjob dla zadania WebJob powiązany projekt sieci web</span><span class="sxs-lookup"><span data-stu-id="8e768-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="8e768-154">Utwórz projekt, który jest skonfigurowany do wdrożenia automatycznie jako zadanie WebJob podczas wdrażania projektu sieci web, w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="8e768-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="8e768-155">Użyj tej opcji, jeśli chcesz uruchomić WebJob w tej samej aplikacji sieci web, w którym można uruchomić aplikacji sieci web pokrewne.</span><span class="sxs-lookup"><span data-stu-id="8e768-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="8e768-156">Szablon nowego projektu zadania Webjob automatycznie instaluje pakiety NuGet i zawiera kod w *Program.cs* dla [zestaw SDK zadań Webjob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="8e768-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="8e768-157">Jeśli nie chcesz korzystać z zestawu SDK zadań Webjob, usunąć ani zmienić `host.RunAndBlock` instrukcji w *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="8e768-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="8e768-158"><a id="createnolink"></a>Szablon dla niezależnych zadania WebJob nowy projekt zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="8e768-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="8e768-159">Kliknij przycisk **pliku** > **nowy projekt**, a następnie w **nowy projekt** kliknij okno dialogowe **chmury** > **zadań WebJob Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="8e768-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Okno dialogowe nowego projektu przedstawiający szablonu zadania WebJob](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="8e768-161">Postępuj zgodnie z instrukcjami pokazano wcześniej do [Aplikacja konsoli projektu niezależne projektu zadania Webjob](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="8e768-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="8e768-162"><a id="createlink"></a>Użyj szablonu nowy projekt zadania Webjob dla zadania WebJob powiązany projekt sieci web</span><span class="sxs-lookup"><span data-stu-id="8e768-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="8e768-163">Kliknij prawym przyciskiem myszy projekt sieci web w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e768-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Nowy wpis menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="8e768-165">[Dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8e768-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="8e768-166">Zakończenie [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e768-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="8e768-167"><a id="configure"></a>Okno dialogowe Dodawanie zadania WebJob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8e768-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="8e768-168">**Dodać zadania WebJob Azure** oknie dialogowym można wprowadzić nazwę zadania WebJob i uruchom tryb WebJob.</span><span class="sxs-lookup"><span data-stu-id="8e768-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Dodawanie zadania WebJob Azure w oknie dialogowym](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="8e768-170">Pola w tym oknie dialogowym odpowiadają polom na **nowe zadanie** okna dialogowego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8e768-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="8e768-171">Aby uzyskać więcej informacji, zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="8e768-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="8e768-172">Informacji o wdrażaniu wiersza polecenia, zobacz [Włączanie wiersza polecenia lub ciągłego dostarczania Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="8e768-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="8e768-173">Jeśli zdecydujesz, że chcesz zmienić typ zadania WebJob i utwórz je ponownie po wdrożeniu zadanie WebJob, należy usunąć plik zadań webjob publikowania settings.json.</span><span class="sxs-lookup"><span data-stu-id="8e768-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="8e768-174">Spowoduje to Visual Studio pokazuj opcje publikowania, dzięki czemu można zmieniać typ zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="8e768-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="8e768-175">Jeśli wdrożyć zadanie WebJob i późniejszej zmiany w trybie uruchamiania z ciągłego nieciągły lub odwrotnie, Visual Studio tworzy nowe zadanie WebJob na platformie Azure, podczas ponownego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="8e768-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="8e768-176">Jeśli zmienisz inne ustawienia harmonogramu, ale pozostaw tryb uruchamiania takie same lub przełączać się między zaplanowane i na żądanie, Visual Studio aktualizuje istniejące zadanie zamiast Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="8e768-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="8e768-177"><a id="publishsettings"></a>zadania webjob — Opublikuj settings.json</span><span class="sxs-lookup"><span data-stu-id="8e768-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="8e768-178">Po skonfigurowaniu aplikacji konsoli dla zadań Webjob wdrożenia programu Visual Studio instaluje [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pakietu i magazyny planowania informacji w *zadania webjob publikowania settings.json* pliku w projekcie *właściwości* folderu projektu zadania Webjob.</span><span class="sxs-lookup"><span data-stu-id="8e768-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="8e768-179">Oto przykład tego pliku:</span><span class="sxs-lookup"><span data-stu-id="8e768-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="8e768-180">Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="8e768-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="8e768-181">Schemat pliku są przechowywane w [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) i można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="8e768-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="8e768-182"><a id="webjobslist"></a>list.json zadań webjob</span><span class="sxs-lookup"><span data-stu-id="8e768-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="8e768-183">Po połączeniu włączone zadań Webjob projektu do projektu sieci web programu Visual Studio przechowuje Nazwa projektu zadania Webjob w *list.json webjob* plik w projekcie sieci web *właściwości* folderu.</span><span class="sxs-lookup"><span data-stu-id="8e768-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="8e768-184">Lista może zawierać wiele projektów zadań Webjob, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8e768-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

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

<span data-ttu-id="8e768-185">Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="8e768-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="8e768-186">Schemat pliku są przechowywane w [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) i można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="8e768-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="8e768-187"><a id="deploy"></a>Wdrażanie projektu zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="8e768-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="8e768-188">Powiązane do projektu sieci web projektu zadania Webjob automatycznie wdraża z projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e768-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="8e768-189">Aby uzyskać informacje dotyczące wdrażania projektu sieci web, zobacz [sposobu wdrażania aplikacji sieci Web](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8e768-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="8e768-190">Aby wdrożyć projekt zadania Webjob samodzielnie, kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** .</span><span class="sxs-lookup"><span data-stu-id="8e768-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="8e768-192">Dla niezależnych zadania WebJob, taki sam **publikowanie w sieci Web** kreatora, który jest używany dla projektów sieci web jest wyświetlana, ale mniej dostępne zmienić ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8e768-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="8e768-193"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e768-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="8e768-194">Ten artykuł ma wyjaśniono sposób wdrażania zadań Webjob za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e768-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="8e768-195">Aby uzyskać więcej informacji na temat sposobu wdrażania zadań Webjob Azure, zobacz [zadań Webjob Azure - zalecane zasoby — wdrożenia](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="8e768-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

