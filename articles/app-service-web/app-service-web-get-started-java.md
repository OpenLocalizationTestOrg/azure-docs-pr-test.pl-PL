---
title: aaaCreate pierwszej aplikacji sieci web Java na platformie Azure
description: "Dowiedz się, jak toorun web apps w usłudze App Service przez wdrożenie podstawowego aplikacji Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="1e801-103">Tworzenie pierwszej aplikacji internetowej w środowisku Java na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1e801-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="1e801-104">Witaj [aplikacje sieci Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funkcji [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e801-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1e801-105">Ta opcja szybkiego startu przedstawia, jak toodeploy Java web app tooApp usługi za pomocą hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="1e801-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![„Hello Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="1e801-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e801-108">Prerequisites</span></span>

<span data-ttu-id="1e801-109">toocomplete tego przewodnika Szybki Start, zainstalować:</span><span class="sxs-lookup"><span data-stu-id="1e801-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="1e801-110">Witaj wolnego [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1e801-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="1e801-111">W tym przewodniku Szybki start używane jest środowisko Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="1e801-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="1e801-112">Witaj [zestawu narzędzi platformy Azure dla programu Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="1e801-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="1e801-113">Tworzenie dynamicznego projektu internetowego w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="1e801-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="1e801-114">W środowisku Eclipse wybierz pozycję **File** > **New** > **Dynamic Web Project** (Plik > Nowy > Dynamiczny projekt internetowy).</span><span class="sxs-lookup"><span data-stu-id="1e801-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="1e801-115">W hello **nowego projektu sieci Web dynamiczne** okno dialogowe, nazwa projektu hello **MyFirstJavaOnAzureWebApp**i wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="1e801-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Okno dialogowe New Dynamic Web Project (Nowy dynamiczny projekt internetowy)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="1e801-117">Dodawanie strony JSP</span><span class="sxs-lookup"><span data-stu-id="1e801-117">Add a JSP page</span></span>

<span data-ttu-id="1e801-118">Jeśli obszar Project Explorer (Eksplorator projektów) nie jest wyświetlany, przywróć go.</span><span class="sxs-lookup"><span data-stu-id="1e801-118">If Project Explorer is not displayed, restore it.</span></span>

![Obszar roboczy Java EE dla środowiska Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="1e801-120">W obszarze Eksplorator projektów rozwiń hello **MyFirstJavaOnAzureWebApp** projektu.</span><span class="sxs-lookup"><span data-stu-id="1e801-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="1e801-121">Kliknij prawym przyciskiem myszy folder **WebContent**, a następnie kliknij pozycję **New** > **JSP File** (Nowy > Plik JSP).</span><span class="sxs-lookup"><span data-stu-id="1e801-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu dla nowego pliku JSP w obszarze Project Explorer (Eksplorator projektów)](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="1e801-123">W hello **New JSP File** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="1e801-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="1e801-124">Nazwa pliku hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="1e801-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="1e801-125">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="1e801-125">Select **Finish**.</span></span>

  ![Okno dialogowe New JSP File (Nowy plik JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="1e801-127">W pliku index.jsp hello Zastąp hello `<body></body>` element z powitania po znaczników:</span><span class="sxs-lookup"><span data-stu-id="1e801-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="1e801-128">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="1e801-129">Publikowanie tooAzure aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="1e801-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="1e801-130">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako aplikacji sieci Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="1e801-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu kontekstowe Publish as Azure Web App (Publikuj jako aplikację internetową platformy Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="1e801-132">W hello **Azure logowania** okno dialogowe, Zachowaj hello **Interactive** opcji, a następnie wybierz **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="1e801-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="1e801-133">Instrukcjami hello logowania.</span><span class="sxs-lookup"><span data-stu-id="1e801-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="1e801-134">Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)</span><span class="sxs-lookup"><span data-stu-id="1e801-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="1e801-135">Po zalogowaniu tooyour konta Azure hello **wdrażanie aplikacji sieci Web** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1e801-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="1e801-136">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e801-136">Select **Create**.</span></span>

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="1e801-138">Okno dialogowe Create App Service (Tworzenie usługi App Service)</span><span class="sxs-lookup"><span data-stu-id="1e801-138">Create App Service dialog box</span></span>

<span data-ttu-id="1e801-139">Witaj **Tworzenie usługi App Service** zostanie wyświetlone okno dialogowe z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="1e801-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="1e801-140">Witaj numer **170602185241** pokazano powitania po obrazu różni się w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="1e801-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="1e801-142">W hello **Tworzenie usługi App Service** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="1e801-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="1e801-143">Zachowaj nazwę hello generowany dla aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="1e801-144">Ta nazwa musi być unikatowa w obrębie całej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1e801-144">This name must be unique across Azure.</span></span> <span data-ttu-id="1e801-145">Nazwa Hello jest częścią hello adres URL aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="1e801-146">Na przykład: Jeśli nazwa aplikacji sieci web hello jest **MyJavaWebApp**, adres URL jest hello *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="1e801-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="1e801-147">Zachowaj hello domyślny kontener sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e801-147">Keep hello default web container.</span></span>
* <span data-ttu-id="1e801-148">Wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1e801-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="1e801-149">Na powitania **plan usługi App service** karty:</span><span class="sxs-lookup"><span data-stu-id="1e801-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="1e801-150">**Utwórz nowe**: Zachowaj domyślne hello, czyli nazwa hello hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e801-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="1e801-151">**Location** (Lokalizacja): wybierz pozycję **West Europe** (Europa Zachodnia) lub lokalizację w Twoim pobliżu.</span><span class="sxs-lookup"><span data-stu-id="1e801-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="1e801-152">**Warstwa cenowa**: Wybierz hello bezpłatną opcją.</span><span class="sxs-lookup"><span data-stu-id="1e801-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="1e801-153">Aby uzyskać informacje o funkcjach, zobacz [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/) (Cennik usługi App Service).</span><span class="sxs-lookup"><span data-stu-id="1e801-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="1e801-155">Karta Resource group (Grupa zasobów)</span><span class="sxs-lookup"><span data-stu-id="1e801-155">Resource group tab</span></span>

<span data-ttu-id="1e801-156">Wybierz hello **grupy zasobów** kartę. Należy zachować wartość domyślną wygenerowany hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1e801-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Karta Resource group (Grupa zasobów)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="1e801-158">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e801-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="1e801-159">Hello Azure Toolkit hello aplikacji sieci web tworzy i wyświetla okno dialogowe postępu.</span><span class="sxs-lookup"><span data-stu-id="1e801-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Okno dialogowe Create App Service Progress (Postęp tworzenia usługi App Service)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="1e801-161">Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)</span><span class="sxs-lookup"><span data-stu-id="1e801-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="1e801-162">W hello **wdrażanie aplikacji sieci Web** okno dialogowe, wybierz opcję **wdrażanie tooroot**.</span><span class="sxs-lookup"><span data-stu-id="1e801-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="1e801-163">Jeśli masz usługę aplikacji na *wingtiptoys.azurewebsites.net* i nie należy wdrażać toohello głównego, hello aplikacji sieci web o nazwie **MyFirstJavaOnAzureWebApp** jest wdrażany za *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="1e801-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="1e801-165">Pokazuje okno dialogowe Hello hello Azure, JDK i opcje kontenera sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e801-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="1e801-166">Wybierz **Wdróż** tooAzure aplikacji sieci web hello toopublish.</span><span class="sxs-lookup"><span data-stu-id="1e801-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="1e801-167">Po zakończeniu publikowania hello, wybierz hello **opublikowano** łącze w hello **dziennika aktywności platformy Azure** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1e801-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Okno dialogowe Azure Activity Log (Dziennik aktywności platformy Azure)](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="1e801-169">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1e801-169">Congratulations!</span></span> <span data-ttu-id="1e801-170">Pomyślnie wdrożono tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e801-170">You have successfully deployed your web app tooAzure.</span></span> 

![„Hello Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="1e801-173">Aktualizowanie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="1e801-173">Update hello web app</span></span>

<span data-ttu-id="1e801-174">Zmień hello przykładowa JSP kodu tooa inną wiadomość.</span><span class="sxs-lookup"><span data-stu-id="1e801-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="1e801-175">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-175">Save hello changes.</span></span>

<span data-ttu-id="1e801-176">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako aplikacji sieci Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="1e801-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="1e801-177">Witaj **wdrażanie aplikacji sieci Web** zostanie wyświetlone okno dialogowe i pokazuje hello wcześniej utworzoną usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e801-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e801-178">Wybierz **wdrażanie tooroot** zawsze publikowania.</span><span class="sxs-lookup"><span data-stu-id="1e801-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="1e801-179">Wybierz aplikację sieci web hello i wybierz **Wdróż**, która publikuje hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="1e801-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="1e801-180">Gdy hello **publikowania** łącze jest wyświetlane, wybierz go w aplikacji sieci web toohello toobrowse i zobaczyć zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="1e801-181">Zarządzanie hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="1e801-181">Manage hello web app</span></span>

<span data-ttu-id="1e801-182">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toosee, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="1e801-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="1e801-183">Wybierz z menu po lewej stronie powitania **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="1e801-183">From hello left menu, select **Resource Groups**.</span></span>

![Grupy tooresource nawigacji w portalu](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="1e801-185">Wybierz grupę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-185">Select hello resource group.</span></span> <span data-ttu-id="1e801-186">na stronie powitania są pokazane hello zasobów, które zostały utworzone w tym Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="1e801-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Grupa zasobów myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="1e801-188">Wybierz hello aplikacji sieci web (**170602193915 aplikacji sieci Web** w hello poprzedzające obraz).</span><span class="sxs-lookup"><span data-stu-id="1e801-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="1e801-189">Witaj **omówienie** zostanie wyświetlona strona.</span><span class="sxs-lookup"><span data-stu-id="1e801-189">hello **Overview** page appears.</span></span> <span data-ttu-id="1e801-190">Ta strona umożliwia widok jak robi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1e801-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="1e801-191">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="1e801-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="1e801-192">Witaj w lewej części strony hello hello kartach hello różne konfiguracje, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="1e801-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Strona usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="1e801-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e801-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e801-195">Mapowanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="1e801-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
