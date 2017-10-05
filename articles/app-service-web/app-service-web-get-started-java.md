---
title: "Tworzenie pierwszej aplikacji internetowej w środowisku Java na platformie Azure"
description: "Dowiedz się, jak można uruchamiać aplikacje internetowe w usłudze App Service, wdrażając podstawową aplikację w środowisku Java."
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="fc183-103">Tworzenie pierwszej aplikacji internetowej w środowisku Java na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fc183-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="fc183-104">Funkcja [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) usługi [Azure App Service](../app-service/app-service-value-prop-what-is.md) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="fc183-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="fc183-105">W tym przewodniku Szybki start pokazano, jak wdrożyć aplikację internetową w języku Java przy użyciu środowiska [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="fc183-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![„Hello Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="fc183-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fc183-108">Prerequisites</span></span>

<span data-ttu-id="fc183-109">Aby ukończyć ten przewodnik Szybki Start, zainstaluj:</span><span class="sxs-lookup"><span data-stu-id="fc183-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="fc183-110">Bezpłatne środowisko [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fc183-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="fc183-111">W tym przewodniku Szybki start używane jest środowisko Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="fc183-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="fc183-112">[Zestaw narzędzi platformy Azure dla środowiska Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="fc183-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="fc183-113">Tworzenie dynamicznego projektu internetowego w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="fc183-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="fc183-114">W środowisku Eclipse wybierz pozycję **File** > **New** > **Dynamic Web Project** (Plik > Nowy > Dynamiczny projekt internetowy).</span><span class="sxs-lookup"><span data-stu-id="fc183-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="fc183-115">W oknie dialogowym **New Dynamic Web Project** (Nowy dynamiczny projekt internetowy) wpisz nazwę projektu **MyFirstJavaOnAzureWebApp**, a następnie wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="fc183-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Okno dialogowe New Dynamic Web Project (Nowy dynamiczny projekt internetowy)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="fc183-117">Dodawanie strony JSP</span><span class="sxs-lookup"><span data-stu-id="fc183-117">Add a JSP page</span></span>

<span data-ttu-id="fc183-118">Jeśli obszar Project Explorer (Eksplorator projektów) nie jest wyświetlany, przywróć go.</span><span class="sxs-lookup"><span data-stu-id="fc183-118">If Project Explorer is not displayed, restore it.</span></span>

![Obszar roboczy Java EE dla środowiska Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="fc183-120">W obszarze Project Explorer (Eksplorator projektów) rozwiń projekt **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="fc183-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="fc183-121">Kliknij prawym przyciskiem myszy folder **WebContent**, a następnie kliknij pozycję **New** > **JSP File** (Nowy > Plik JSP).</span><span class="sxs-lookup"><span data-stu-id="fc183-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu dla nowego pliku JSP w obszarze Project Explorer (Eksplorator projektów)](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="fc183-123">W oknie dialogowym **New JSP File** (Nowy plik JSP):</span><span class="sxs-lookup"><span data-stu-id="fc183-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="fc183-124">Jako nazwę pliku podaj wartość **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="fc183-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="fc183-125">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="fc183-125">Select **Finish**.</span></span>

  ![Okno dialogowe New JSP File (Nowy plik JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="fc183-127">W pliku index.jsp zastąp element `<body></body>` następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="fc183-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="fc183-128">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="fc183-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="fc183-129">Publikowanie aplikacji internetowej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fc183-129">Publish the web app to Azure</span></span>

<span data-ttu-id="fc183-130">W obszarze Project Explorer (Eksplorator projektów) kliknij projekt prawym przyciskiem myszy, a następnie wybierz pozycję **Azure** > **Publish as Azure Web App** (Publikuj jako aplikację internetową platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="fc183-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu kontekstowe Publish as Azure Web App (Publikuj jako aplikację internetową platformy Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="fc183-132">W oknie dialogowym **Azure Sign In** (Logowanie do platformy Azure) zachowaj opcję **Interactive** (Interaktywne), a następnie wybierz pozycję **Sign in** (Zaloguj).</span><span class="sxs-lookup"><span data-stu-id="fc183-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="fc183-133">Postępuj zgodnie z instrukcjami dotyczącymi logowania.</span><span class="sxs-lookup"><span data-stu-id="fc183-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="fc183-134">Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)</span><span class="sxs-lookup"><span data-stu-id="fc183-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="fc183-135">Po zalogowaniu się na koncie platformy Azure zostanie wyświetlone okno dialogowe **Deploy Web App** (Wdrażanie aplikacji internetowej).</span><span class="sxs-lookup"><span data-stu-id="fc183-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="fc183-136">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fc183-136">Select **Create**.</span></span>

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="fc183-138">Okno dialogowe Create App Service (Tworzenie usługi App Service)</span><span class="sxs-lookup"><span data-stu-id="fc183-138">Create App Service dialog box</span></span>

<span data-ttu-id="fc183-139">Zostanie wyświetlone okno dialogowe **Create App Service** (Tworzenie usługi App Service) z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="fc183-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="fc183-140">Liczba **170602185241** wyświetlana na poniższym obrazie będzie inna w Twoim oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="fc183-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="fc183-142">W oknie dialogowym **Create App Service** (Tworzenie usługi App Service):</span><span class="sxs-lookup"><span data-stu-id="fc183-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="fc183-143">Zachowaj wygenerowaną nazwę aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="fc183-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="fc183-144">Ta nazwa musi być unikatowa w obrębie całej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc183-144">This name must be unique across Azure.</span></span> <span data-ttu-id="fc183-145">Nazwa jest częścią adresu URL aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="fc183-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="fc183-146">Przykład: jeśli nazwa aplikacji internetowej to **MyJavaWebApp**, adres URL to *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="fc183-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="fc183-147">Zachowaj domyślny kontener internetowy.</span><span class="sxs-lookup"><span data-stu-id="fc183-147">Keep the default web container.</span></span>
* <span data-ttu-id="fc183-148">Wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc183-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="fc183-149">Na karcie **App service plan** (Plan usługi App Service):</span><span class="sxs-lookup"><span data-stu-id="fc183-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="fc183-150">**Create new** (Utwórz nowy): zachowaj wartość domyślną, czyli nazwę planu usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="fc183-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="fc183-151">**Location** (Lokalizacja): wybierz pozycję **West Europe** (Europa Zachodnia) lub lokalizację w Twoim pobliżu.</span><span class="sxs-lookup"><span data-stu-id="fc183-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="fc183-152">**Pricing tier** (Warstwa cenowa): wybierz opcję Free (Bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="fc183-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="fc183-153">Aby uzyskać informacje o funkcjach, zobacz [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/) (Cennik usługi App Service).</span><span class="sxs-lookup"><span data-stu-id="fc183-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="fc183-155">Karta Resource group (Grupa zasobów)</span><span class="sxs-lookup"><span data-stu-id="fc183-155">Resource group tab</span></span>

<span data-ttu-id="fc183-156">Wybierz kartę **Resource group** (Grupa zasobów). Zachowaj domyślnie wygenerowaną wartość dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc183-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Karta Resource group (Grupa zasobów)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="fc183-158">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fc183-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="fc183-159">Za pomocą zestawu narzędzi platformy Azure zostanie utworzona aplikacja internetowa i wyświetlone okno dialogowe postępu.</span><span class="sxs-lookup"><span data-stu-id="fc183-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Okno dialogowe Create App Service Progress (Postęp tworzenia usługi App Service)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="fc183-161">Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)</span><span class="sxs-lookup"><span data-stu-id="fc183-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="fc183-162">W oknie dialogowym **Deploy Web App** (Wdrażanie aplikacji internetowej) wybierz pozycję **Deploy to root** (Wdróż w katalogu głównym).</span><span class="sxs-lookup"><span data-stu-id="fc183-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="fc183-163">Jeśli istnieje usługa App Service w lokalizacji *wingtiptoys.azurewebsites.net* i nie wybierzesz wdrożenia w katalogu głównym, to aplikacja internetowa o nazwie **MyFirstJavaOnAzureWebApp** zostanie wdrożona w lokalizacji *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="fc183-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="fc183-165">Okno dialogowe zawiera wybory dokonane dla platformy Azure, zestawu JDK i kontenera internetowego.</span><span class="sxs-lookup"><span data-stu-id="fc183-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="fc183-166">Wybierz pozycję **Deploy** (Wdróż), aby opublikować aplikację internetową na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fc183-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="fc183-167">Po zakończeniu publikowania wybierz link **Published** (Opublikowano) w oknie dialogowym **Azure Activity Log** (Dziennik aktywności platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="fc183-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Okno dialogowe Azure Activity Log (Dziennik aktywności platformy Azure)](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="fc183-169">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="fc183-169">Congratulations!</span></span> <span data-ttu-id="fc183-170">Aplikacja internetowa została pomyślnie wdrożona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fc183-170">You have successfully deployed your web app to Azure.</span></span> 

![„Hello Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="fc183-173">Aktualizowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="fc183-173">Update the web app</span></span>

<span data-ttu-id="fc183-174">Zmień przykładowy kod JSP na inny komunikat.</span><span class="sxs-lookup"><span data-stu-id="fc183-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="fc183-175">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="fc183-175">Save the changes.</span></span>

<span data-ttu-id="fc183-176">W obszarze Project Explorer (Eksplorator projektów) kliknij projekt prawym przyciskiem myszy, a następnie wybierz pozycję **Azure** > **Publish as Azure Web App** (Publikuj jako aplikację internetową platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="fc183-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="fc183-177">Zostanie wyświetlone okno dialogowe **Deploy Web App** (Wdrażanie aplikacji internetowej), w którym będzie wyświetlona wcześniej utworzona usługa App Service.</span><span class="sxs-lookup"><span data-stu-id="fc183-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="fc183-178">Wybieraj pozycję **Deploy to root** (Wdróż w katalogu głównym) za każdym razem, gdy ma miejsce publikowanie.</span><span class="sxs-lookup"><span data-stu-id="fc183-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="fc183-179">Wybierz aplikację internetową, a następnie wybierz pozycję **Deploy** (Wdróż), co spowoduje opublikowanie zmian.</span><span class="sxs-lookup"><span data-stu-id="fc183-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="fc183-180">Gdy zostanie wyświetlony link **Publishing** (Publikowanie), wybierz go, aby przejść do aplikacji internetowej i wyświetlić zmiany.</span><span class="sxs-lookup"><span data-stu-id="fc183-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="fc183-181">Zarządzanie aplikacją internetową</span><span class="sxs-lookup"><span data-stu-id="fc183-181">Manage the web app</span></span>

<span data-ttu-id="fc183-182">Przejdź do witryny <a href="https://portal.azure.com" target="_blank">Azure Portal</a>, aby wyświetlić utworzoną aplikację internetową.</span><span class="sxs-lookup"><span data-stu-id="fc183-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="fc183-183">W menu po lewej stronie kliknij pozycję **Grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fc183-183">From the left menu, select **Resource Groups**.</span></span>

![Nawigacja w portalu do grupy zasobów](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="fc183-185">Wybierz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc183-185">Select the resource group.</span></span> <span data-ttu-id="fc183-186">Na stronie znajdują się zasoby utworzone w ramach tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="fc183-186">The page shows the resources that you created in this quickstart.</span></span>

![Grupa zasobów myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="fc183-188">Wybierz aplikację internetową (**webapp-170602193915** na powyższym obrazie).</span><span class="sxs-lookup"><span data-stu-id="fc183-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="fc183-189">Zostanie wyświetlona strona **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="fc183-189">The **Overview** page appears.</span></span> <span data-ttu-id="fc183-190">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fc183-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="fc183-191">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="fc183-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="fc183-192">Na kartach po lewej stronie strony są pokazane poszczególne konfiguracje, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="fc183-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Strona usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="fc183-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc183-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc183-195">Mapowanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="fc183-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
