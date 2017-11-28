---
title: "aaaDeploy aplikacji WordPress w portalu Azure w ciągu pięciu minut hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łatwo jest toorun aplikacje sieci web w usłudze App Service, wdrażając aplikacji WordPress. Wyniki będą widoczne od razu."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="86252-104">Wdrażanie aplikacji WordPress w hello portalu Azure w ciągu pięciu minut</span><span class="sxs-lookup"><span data-stu-id="86252-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="86252-105">W tym samouczku przedstawiono sposób toodeploy pierwszego [WordPress](https://wordpress.org/) sieci web aplikacji zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) w minutach.</span><span class="sxs-lookup"><span data-stu-id="86252-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Witryna WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="86252-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86252-107">Prerequisites</span></span>
<span data-ttu-id="86252-108">Potrzebujesz konta platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86252-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="86252-109">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="86252-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="86252-110">Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86252-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="86252-111">Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="86252-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="86252-112">Wdrażanie aplikacji WordPress hello</span><span class="sxs-lookup"><span data-stu-id="86252-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="86252-113">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86252-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="86252-114">Otwórz link [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="86252-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="86252-115">To łącze jest tooimmediately skrótów skonfiguruj nową aplikację WordPress w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="86252-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="86252-116">W polu **Nazwa aplikacji** wpisz nazwę aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="86252-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="86252-117">Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `azurewebsites.net` domeny.</span><span class="sxs-lookup"><span data-stu-id="86252-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="86252-118">W **grupy zasobów**, kliknij przycisk **Utwórz nowy** toocreate nowy [grupy zasobów](../azure-resource-manager/resource-group-overview.md), następnie nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="86252-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="86252-119">W polu **Dostawca bazy danych** wybierz pozycję **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="86252-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="86252-120">Kliknij pozycję **Plan/lokalizacja usługi App Service** > **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="86252-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="86252-121">Skonfiguruj hello [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pokazany:</span><span class="sxs-lookup"><span data-stu-id="86252-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="86252-122">W **planu usługi aplikacji**, żądana nazwa hello typu.</span><span class="sxs-lookup"><span data-stu-id="86252-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="86252-123">W **lokalizacji**, wybierz plan toohost lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="86252-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="86252-124">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F1** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="86252-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="86252-125">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="86252-125">Click **OK**.</span></span>

8. <span data-ttu-id="86252-126">Kliknij pozycję **Baza danych** > **Utwórz nową**.</span><span class="sxs-lookup"><span data-stu-id="86252-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="86252-127">Skonfiguruj hello bazy danych SQL, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="86252-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="86252-128">W polu **Nazwa bazy danych** wpisz nazwę bazy danych.</span><span class="sxs-lookup"><span data-stu-id="86252-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="86252-129">W **lokalizacji**, wybierz hello tej samej lokalizacji co hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86252-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="86252-130">Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Mercury** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="86252-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="86252-131">Kliknij pozycję **Postanowienia prawne**, a następnie pozycję **Zakup**.</span><span class="sxs-lookup"><span data-stu-id="86252-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="86252-132">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="86252-132">Click **OK**.</span></span>

9. <span data-ttu-id="86252-133">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="86252-133">Click **Create**.</span></span>

    <span data-ttu-id="86252-134">Platforma Azure utworzy teraz aplikację WordPress zgodnie z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="86252-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="86252-135">Powinno być widoczne powiadomienie **Wdrażanie rozpoczęte...**.</span><span class="sxs-lookup"><span data-stu-id="86252-135">You should see a **Deployment started...** notification.</span></span>

    ![Wdrażanie rozpoczęte — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="86252-137">Uruchamianie aplikacji sieci Web WordPress i zarządzanie nią</span><span class="sxs-lookup"><span data-stu-id="86252-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="86252-138">Po zakończeniu wdrażania aplikacji przez platformę Azure zostanie wyświetlone kolejne powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="86252-138">When Azure completes app deployment you see another notification.</span></span>

![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="86252-140">Kliknij powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="86252-140">Click hello notification.</span></span> <span data-ttu-id="86252-141">Jeśli pominięte go, należy zawsze do niego dostęp, klikając hello dzwonka powiadomień (![powiadomień poniższych — pierwszy WordPress w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="86252-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="86252-142">Powinien zostać wyświetlony [blok](../azure-resource-manager/resource-group-portal.md#manage-resources) zarządzania aplikacją sieci Web (*blok*: strona portalu otwierana poziomo).</span><span class="sxs-lookup"><span data-stu-id="86252-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="86252-143">W hello górnej części strony Przegląd hello, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="86252-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Przeglądanie — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="86252-145">Teraz zostanie wyświetlony hello WordPress **powitalnej** strony.</span><span class="sxs-lookup"><span data-stu-id="86252-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="86252-146">Skonfiguruj hello WordPress instalację i rozpocząć odtwarzanie z nim!</span><span class="sxs-lookup"><span data-stu-id="86252-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Konfiguracja platformy WordPress — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="86252-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86252-148">Next steps</span></span>
* <span data-ttu-id="86252-149">[Tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web Laravel](app-service-web-php-get-started.md) — Dowiedz się hello podstawowe umiejętności toorun dowolnej aplikacji sieci web PHP na platformie Azure, takich jak:</span><span class="sxs-lookup"><span data-stu-id="86252-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="86252-150">tworzenie i konfigurowanie aplikacji na platformie Azure z poziomu programu PowerShell/Bash;</span><span class="sxs-lookup"><span data-stu-id="86252-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="86252-151">ustawianie wersji języka PHP;</span><span class="sxs-lookup"><span data-stu-id="86252-151">Set PHP version.</span></span>
    * <span data-ttu-id="86252-152">Użyj pliku początkowej, który nie znajduje się w katalogu aplikacji hello głównego.</span><span class="sxs-lookup"><span data-stu-id="86252-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="86252-153">włączanie automatyzacji narzędzia Composer;</span><span class="sxs-lookup"><span data-stu-id="86252-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="86252-154">uzyskiwanie dostępu do zmiennych określonych dla środowiska;</span><span class="sxs-lookup"><span data-stu-id="86252-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="86252-155">rozwiązywanie typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="86252-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="86252-156">[Wdrażanie tooAzure Twojego kodu usługi aplikacji —](web-sites-deploy.md)— Dowiedz się, jak toodeploy z FTP lub źródło kontroli repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="86252-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="86252-157">[Dodawanie funkcji tooyour pierwszej aplikacji sieci web](app-service-web-get-started-2.md) -podjąć toohello Twojej aplikacji Azure obok poziomu.</span><span class="sxs-lookup"><span data-stu-id="86252-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="86252-158">Uwierzytelniaj użytkowników.</span><span class="sxs-lookup"><span data-stu-id="86252-158">Authenticate your users.</span></span> <span data-ttu-id="86252-159">Skaluj ją zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="86252-159">Scale it based on demand.</span></span> <span data-ttu-id="86252-160">Skonfiguruj alerty dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="86252-160">Set up some performance alerts.</span></span> <span data-ttu-id="86252-161">Wszystkie te czynności możesz wykonać za pomocą kilku kliknięć.</span><span class="sxs-lookup"><span data-stu-id="86252-161">All with a few clicks.</span></span>
