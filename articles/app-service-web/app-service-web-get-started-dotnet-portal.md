---
title: "Wdrażanie aplikacji sieci Web Umbraco w witrynie Azure Portal w ciągu pięciu minut | Microsoft Docs"
description: "Dowiedz się, jak łatwo można uruchamiać aplikacje sieci Web w usłudze App Service, wdrażając przykładową aplikację platformy ASP.NET. Wyniki będą widoczne od razu."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="62561-104">Wdrażanie aplikacji sieci Web Umbraco w witrynie Azure Portal w ciągu pięciu minut</span><span class="sxs-lookup"><span data-stu-id="62561-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="62561-105">Ten samouczek ułatwia wdrożenie aplikacji sieci Web [Umbraco](https://our.umbraco.org/) w usłudze [Azure App Service](../app-service/app-service-value-prop-what-is.md) w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="62561-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplikacja Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="62561-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="62561-107">Prerequisites</span></span>
<span data-ttu-id="62561-108">Potrzebujesz konta platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="62561-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="62561-109">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="62561-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="62561-110">Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62561-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="62561-111">Utwórz aplikację startową i testuj ją nawet przez godzinę — bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="62561-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="62561-112">Wdrażanie aplikacji ASP.NET</span><span class="sxs-lookup"><span data-stu-id="62561-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="62561-113">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62561-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="62561-114">Otwórz link [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="62561-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="62561-115">Ten link to skrót umożliwiający natychmiastowe skonfigurowanie nowej aplikacji Umbraco w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="62561-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="62561-116">W polu **Nazwa aplikacji** wpisz nazwę aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="62561-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="62561-117">Jeśli nazwa jest unikatowa w domenie `azurewebsites.net`, w polu zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="62561-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="62561-118">W polu **Grupa zasobów** kliknij pozycję **Utwórz nową** w celu utworzenia nowej [grupy zasobów](../azure-resource-manager/resource-group-overview.md), a następnie nadaj jej nazwę.</span><span class="sxs-lookup"><span data-stu-id="62561-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="62561-119">Kliknij pozycję **Plan/lokalizacja usługi App Service** > **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="62561-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="62561-120">Skonfiguruj [plan usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="62561-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="62561-121">W polu **Plan usługi App Service** wpisz odpowiednią nazwę.</span><span class="sxs-lookup"><span data-stu-id="62561-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="62561-122">W polu **Lokalizacja** wybierz lokalizację na potrzeby hostowania planu.</span><span class="sxs-lookup"><span data-stu-id="62561-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="62561-123">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F1** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="62561-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="62561-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62561-124">Click **OK**.</span></span>

    <span data-ttu-id="62561-125">Konfiguracja aplikacji Umbraco CMS powinna teraz wyglądać podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="62561-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Konfiguracja w toku — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="62561-127">Kliknij opcję **Baza danych SQL** > **Utwórz nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="62561-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="62561-128">Skonfiguruj bazę danych SQL w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="62561-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="62561-129">W polu **Nazwa** wpisz nazwę, np. **mojaBazaDanych**.</span><span class="sxs-lookup"><span data-stu-id="62561-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="62561-130">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="62561-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="62561-131">Kliknij pozycję **Serwer docelowy** > **Utwórz nowy serwer**.</span><span class="sxs-lookup"><span data-stu-id="62561-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="62561-132">Skonfiguruj serwer bazy danych tak, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="62561-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="62561-133">W polu **Nazwa serwera** wpisz nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="62561-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="62561-134">Jeśli nazwa jest unikatowa w domenie `.database.windows.net`, w polu zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="62561-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="62561-135">W polu **Identyfikator logowania administratora serwera** wpisz żądaną nazwę użytkownika administratora.</span><span class="sxs-lookup"><span data-stu-id="62561-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="62561-136">W polach **Hasło** i **Potwierdź hasło** wpisz odpowiednie hasło.</span><span class="sxs-lookup"><span data-stu-id="62561-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="62561-137">W polu Lokalizacja wybierz tę samą lokalizację, która jest używana dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="62561-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="62561-138">Upewnij się, że opcja **Zezwalaj usługom platformy Azure na dostęp do serwera** jest wybrana.</span><span class="sxs-lookup"><span data-stu-id="62561-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="62561-139">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="62561-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="62561-140">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="62561-140">Click **Select**.</span></span>

13. <span data-ttu-id="62561-141">Kliknij pozycję **Ustawienia aplikacji sieci Web**, określ nazwę użytkownika i hasło bazy danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62561-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="62561-142">Konfiguracja aplikacji Umbraco CMS powinna teraz wyglądać podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="62561-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Konfiguracja ukończona — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="62561-144">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="62561-144">Click **Create**.</span></span>
    
    <span data-ttu-id="62561-145">Platforma Azure utworzy teraz aplikację Umbraco zgodnie z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="62561-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="62561-146">Powinno być widoczne powiadomienie **Wdrażanie rozpoczęte...**.</span><span class="sxs-lookup"><span data-stu-id="62561-146">You should see a **Deployment started...** notification.</span></span>

    ![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="62561-148">Uruchamianie aplikacji sieci Web Umbraco i zarządzanie nią</span><span class="sxs-lookup"><span data-stu-id="62561-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="62561-149">Po zakończeniu wdrażania aplikacji przez platformę Azure zostanie wyświetlone kolejne powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="62561-149">When Azure completes app deployment you see another notification.</span></span>

![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="62561-151">Kliknij powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="62561-151">Click the notification.</span></span> <span data-ttu-id="62561-152">Jeśli powiadomienie już zniknęło, zawsze można uzyskać do niego dostęp, klikając dzwonek powiadomień (![Dzwonek powiadomień — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="62561-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="62561-153">Powinien zostać wyświetlony [blok](../azure-resource-manager/resource-group-portal.md#manage-resources) zarządzania aplikacją sieci Web (*blok*: strona portalu otwierana poziomo).</span><span class="sxs-lookup"><span data-stu-id="62561-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="62561-154">W górnej części strony Przegląd kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="62561-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Przeglądanie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="62561-156">Zostanie wyświetlona strona **powitalna** Umbraco.</span><span class="sxs-lookup"><span data-stu-id="62561-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="62561-157">Skonfiguruj instalację aplikacji Umbraco i zacznij ją poznawać!</span><span class="sxs-lookup"><span data-stu-id="62561-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Konfiguracja aplikacji Umbraco — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="62561-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62561-159">Next steps</span></span>
* <span data-ttu-id="62561-160">[Wdrażanie aplikacji sieci Web programu ASP.NET w usłudze Azure App Service przy użyciu programu Visual Studio](app-service-web-get-started-dotnet.md) — dowiedz się, jak utworzyć nową aplikację sieci Web platformy Azure w programie Visual Studio przy użyciu jednego z dołączonych szablonów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62561-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="62561-161">[Deploy your code to Azure App Service](web-sites-deploy.md) (Wdrażanie kodu w usłudze Azure App Service) — informacje o sposobie wdrażania z serwera FTP lub repozytoriów kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="62561-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="62561-162">[Dodawanie funkcji do pierwszej aplikacji sieci Web](app-service-web-get-started-2.md) — przenieś swoją aplikację Azure na wyższy poziom.</span><span class="sxs-lookup"><span data-stu-id="62561-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="62561-163">Uwierzytelniaj użytkowników.</span><span class="sxs-lookup"><span data-stu-id="62561-163">Authenticate your users.</span></span> <span data-ttu-id="62561-164">Skaluj ją zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="62561-164">Scale it based on demand.</span></span> <span data-ttu-id="62561-165">Skonfiguruj alerty dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="62561-165">Set up some performance alerts.</span></span> <span data-ttu-id="62561-166">Wszystkie te czynności możesz wykonać za pomocą kilku kliknięć.</span><span class="sxs-lookup"><span data-stu-id="62561-166">All with a few clicks.</span></span>
