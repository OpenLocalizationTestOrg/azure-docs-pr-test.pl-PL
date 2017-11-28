---
title: "aaaDeploy Umbraco aplikacji sieci web w portalu Azure w ciągu pięciu minut hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łatwo jest toorun aplikacje sieci web w usłudze App Service, wdrażając przykładową aplikację ASP.NET. Wyniki będą widoczne od razu."
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
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="d1fa8-104">Wdrażanie aplikacji sieci web Umbraco w hello portalu Azure w ciągu pięciu minut</span><span class="sxs-lookup"><span data-stu-id="d1fa8-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="d1fa8-105">Ten samouczek ułatwia wdrażanie n [Umbraco](https://our.umbraco.org/) sieci web aplikacji zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) w minutach.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplikacja Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="d1fa8-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1fa8-107">Prerequisites</span></span>
<span data-ttu-id="d1fa8-108">Potrzebujesz konta platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="d1fa8-109">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d1fa8-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="d1fa8-110">Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="d1fa8-111">Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="d1fa8-112">Wdrażanie aplikacji ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="d1fa8-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="d1fa8-113">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1fa8-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d1fa8-114">Otwórz link [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="d1fa8-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="d1fa8-115">To łącze jest tooimmediately skrótów skonfiguruj nową aplikację Umbraco w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="d1fa8-116">W polu **Nazwa aplikacji** wpisz nazwę aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="d1fa8-117">Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `azurewebsites.net` domeny.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="d1fa8-118">W **grupy zasobów**, kliknij przycisk **Utwórz nowy** toocreate nowy [grupy zasobów](../azure-resource-manager/resource-group-overview.md), następnie nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="d1fa8-119">Kliknij pozycję **Plan/lokalizacja usługi App Service** > **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="d1fa8-120">Skonfiguruj hello [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pokazany:</span><span class="sxs-lookup"><span data-stu-id="d1fa8-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="d1fa8-121">W **planu usługi aplikacji**, żądana nazwa hello typu.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="d1fa8-122">W **lokalizacji**, wybierz plan toohost lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="d1fa8-123">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F1** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d1fa8-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-124">Click **OK**.</span></span>

    <span data-ttu-id="d1fa8-125">Umbraco CMS konfiguracji powinna wyglądać tak jak powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="d1fa8-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Konfiguracja w toku — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="d1fa8-127">Kliknij opcję **Baza danych SQL** > **Utwórz nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="d1fa8-128">Skonfiguruj hello bazy danych SQL, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="d1fa8-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="d1fa8-129">W polu **Nazwa** wpisz nazwę, np. **mojaBazaDanych**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="d1fa8-130">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d1fa8-131">Kliknij pozycję **Serwer docelowy** > **Utwórz nowy serwer**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="d1fa8-132">Skonfiguruj powitania serwera bazy danych, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="d1fa8-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="d1fa8-133">W polu **Nazwa serwera** wpisz nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="d1fa8-134">Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `.database.windows.net` domeny.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="d1fa8-135">W **identyfikator logowania administratora serwera**, hello typu potrzebne administratora nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="d1fa8-136">W **hasło** i **Potwierdź hasło**, typ hello wymagane hasło.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="d1fa8-137">W lokalizacji wybierz hello tej samej lokalizacji, używane w przypadku aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="d1fa8-138">Upewnij się, że **Zezwalaj usługom platformy azure tooaccess serwera** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="d1fa8-139">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="d1fa8-140">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-140">Click **Select**.</span></span>

13. <span data-ttu-id="d1fa8-141">Kliknij przycisk **ustawienia aplikacji w sieci Web**, określ hello bazy danych użytkownika i hasło i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="d1fa8-142">Umbraco CMS konfiguracji powinna wyglądać tak jak powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="d1fa8-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Konfiguracja ukończona — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="d1fa8-144">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-144">Click **Create**.</span></span>
    
    <span data-ttu-id="d1fa8-145">Platforma Azure utworzy teraz aplikację Umbraco zgodnie z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="d1fa8-146">Powinno być widoczne powiadomienie **Wdrażanie rozpoczęte...**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-146">You should see a **Deployment started...** notification.</span></span>

    ![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="d1fa8-148">Uruchamianie aplikacji sieci Web Umbraco i zarządzanie nią</span><span class="sxs-lookup"><span data-stu-id="d1fa8-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="d1fa8-149">Po zakończeniu wdrażania aplikacji przez platformę Azure zostanie wyświetlone kolejne powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-149">When Azure completes app deployment you see another notification.</span></span>

![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="d1fa8-151">Kliknij powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-151">Click hello notification.</span></span> <span data-ttu-id="d1fa8-152">Jeśli pominięte go, należy zawsze do niego dostęp, klikając hello dzwonka powiadomień (![powiadomień poniższych — pierwszy program Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="d1fa8-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="d1fa8-153">Powinien zostać wyświetlony [blok](../azure-resource-manager/resource-group-portal.md#manage-resources) zarządzania aplikacją sieci Web (*blok*: strona portalu otwierana poziomo).</span><span class="sxs-lookup"><span data-stu-id="d1fa8-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="d1fa8-154">W hello górnej części strony Przegląd hello, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Przeglądanie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="d1fa8-156">Teraz zostanie wyświetlony hello Umbraco **powitalnej** strony.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="d1fa8-157">Skonfiguruj hello Umbraco instalację i rozpocząć odtwarzanie z nim!</span><span class="sxs-lookup"><span data-stu-id="d1fa8-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Konfiguracja aplikacji Umbraco — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="d1fa8-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1fa8-159">Next steps</span></span>
* <span data-ttu-id="d1fa8-160">[Wdrażanie tooAzure aplikacji sieci web ASP.NET App Service przy użyciu programu Visual Studio](app-service-web-get-started-dotnet.md) — Dowiedz się, jak toocreate nowej aplikacji sieci web platformy Azure w programie Visual Studio przy użyciu jednego z hello uwzględnione szablonów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="d1fa8-161">[Wdrażanie tooAzure Twojego kodu usługi aplikacji —](web-sites-deploy.md)— Dowiedz się, jak toodeploy z FTP lub źródło kontroli repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="d1fa8-162">[Dodawanie funkcji tooyour pierwszej aplikacji sieci web](app-service-web-get-started-2.md) -podjąć toohello Twojej aplikacji Azure obok poziomu.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="d1fa8-163">Uwierzytelniaj użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-163">Authenticate your users.</span></span> <span data-ttu-id="d1fa8-164">Skaluj ją zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-164">Scale it based on demand.</span></span> <span data-ttu-id="d1fa8-165">Skonfiguruj alerty dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-165">Set up some performance alerts.</span></span> <span data-ttu-id="d1fa8-166">Wszystkie te czynności możesz wykonać za pomocą kilku kliknięć.</span><span class="sxs-lookup"><span data-stu-id="d1fa8-166">All with a few clicks.</span></span>
