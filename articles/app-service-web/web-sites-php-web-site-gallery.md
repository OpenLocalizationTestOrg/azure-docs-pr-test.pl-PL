---
title: "aaaCreate aplikacji sieci web WordPress w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure nowej sieci web aplikacji dla bloga WordPress przy użyciu hello portalu Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="4750c-103">Tworzenie aplikacji sieci Web WordPress w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4750c-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="4750c-104">Ten samouczek pokazuje, jak toodeploy bloga WordPress lokacji z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4750c-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="4750c-105">Po zakończeniu korzystania z samouczka hello będziesz mieć własne witrynę bloga WordPress i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="4750c-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="4750c-107">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="4750c-107">You'll learn:</span></span>

* <span data-ttu-id="4750c-108">Jak toofind szablonem aplikacji w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4750c-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="4750c-109">Jak toocreate aplikacji sieci web w aplikacji Azure usługi, który jest oparty na szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="4750c-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="4750c-110">Jak ustawienia usługi Azure App Service tooconfigure hello nowej sieci web, aplikacji i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4750c-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="4750c-111">Hello Azure Marketplace udostępnia szeroką gamę popularnych aplikacji sieci web opracowany przez firmę Microsoft, inne firmy i inicjatyw oprogramowania typu open source.</span><span class="sxs-lookup"><span data-stu-id="4750c-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="4750c-112">aplikacje sieci web Hello są tworzone przy użyciu różnych popularnych platformach, takich jak [PHP](/develop/nodejs/) w tym przykładzie WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), i [Python](/develop/python/), tooname w kilku.</span><span class="sxs-lookup"><span data-stu-id="4750c-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="4750c-113">toocreate aplikacji sieci web z portalu Azure Marketplace hello tylko oprogramowanie potrzebne jest hello przeglądarka, której używasz hello hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4750c-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="4750c-114">Witaj witryna WordPress wdrażana w tym samouczku korzysta hello bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="4750c-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="4750c-115">Jeśli chcesz, aby używany tooinstead bazy danych SQL z bazą danych hello, zobacz [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="4750c-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="4750c-116">**Project Nami** jest również dostępny za pośrednictwem hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4750c-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="4750c-117">toocomplete tego samouczka jest potrzebne konto Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4750c-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="4750c-118">Jeśli nie masz konta, możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) lub [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4750c-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="4750c-119">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="4750c-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="4750c-120">W tej lokalizacji możesz od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="4750c-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="4750c-121">Wybieranie platformy WordPress i konfigurowanie dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4750c-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="4750c-122">Zaloguj się za toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4750c-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4750c-123">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="4750c-123">Click **New**.</span></span>
   
    ![Kliknięcie przycisku Nowe][5]
3. <span data-ttu-id="4750c-125">Wyszukaj wyrażenie **WordPress**, a następnie kliknij pozycję **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="4750c-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="4750c-126">Jeśli chcesz toouse SQL Database zamiast MySQL, wyszukaj **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="4750c-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![Pozycja WordPress na liście][7]
4. <span data-ttu-id="4750c-128">Po przeczytaniu opisu aplikacji WordPress hello hello, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4750c-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Przycisk Utwórz](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="4750c-130">Wprowadź nazwę dla aplikacji sieci web hello w hello **aplikacji sieci Web** pole.</span><span class="sxs-lookup"><span data-stu-id="4750c-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="4750c-131">Ta nazwa musi być unikatowa w domenie azurewebsites.net hello, ponieważ adres URL aplikacji sieci web hello hello będzie {nazwa}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="4750c-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="4750c-132">Jeśli wprowadzona nazwa hello nie jest unikatowa, w polu tekstowym hello zostanie wyświetlony czerwony wykrzyknik.</span><span class="sxs-lookup"><span data-stu-id="4750c-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="4750c-133">Jeśli masz więcej niż jedną subskrypcję, wybierz hello co chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="4750c-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="4750c-134">Wybierz **grupę zasobów** lub utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="4750c-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="4750c-135">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4750c-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="4750c-136">Wybierz pozycję **Plan usługi App Service/Lokalizacja** lub utwórz nowy plan.</span><span class="sxs-lookup"><span data-stu-id="4750c-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="4750c-137">Aby uzyskać więcej informacji na temat planów usługi App Service, zobacz [Omówienie planów usługi Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4750c-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="4750c-138">Kliknij przycisk **bazy danych**, a następnie w hello **Nowa baza danych MySQL** bloku Podaj wartości hello wymagane do konfigurowania bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="4750c-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="4750c-139">a.</span><span class="sxs-lookup"><span data-stu-id="4750c-139">a.</span></span> <span data-ttu-id="4750c-140">Wprowadź nową nazwę lub pozostaw nazwę domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="4750c-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="4750c-141">b.</span><span class="sxs-lookup"><span data-stu-id="4750c-141">b.</span></span> <span data-ttu-id="4750c-142">Pozostaw hello **typ bazy danych** ustawić także**Shared**.</span><span class="sxs-lookup"><span data-stu-id="4750c-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="4750c-143">c.</span><span class="sxs-lookup"><span data-stu-id="4750c-143">c.</span></span> <span data-ttu-id="4750c-144">Wybierz hello wybranych w tej samej lokalizacji, co który hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4750c-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="4750c-145">d.</span><span class="sxs-lookup"><span data-stu-id="4750c-145">d.</span></span> <span data-ttu-id="4750c-146">Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="4750c-146">Choose a pricing tier.</span></span> <span data-ttu-id="4750c-147">Warstwa Mercury (bezpłatnie z minimalnymi dopuszczalnymi połączeniami i miejscem na dysku) jest odpowiednia dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="4750c-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="4750c-148">W hello **Nowa baza danych MySQL** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4750c-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="4750c-149">W hello **WordPress** bloku, zaakceptuj postanowienia prawne hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4750c-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="4750c-151">Usługa aplikacji Azure tworzy hello aplikacji sieci web, zazwyczaj w mniej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="4750c-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="4750c-152">Możesz obserwować postęp hello, klikając ikonę dzwonka hello u góry hello hello strony portalu.</span><span class="sxs-lookup"><span data-stu-id="4750c-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Wskaźnik postępu](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="4750c-154">Uruchamianie aplikacji sieci Web WordPress i zarządzanie nią</span><span class="sxs-lookup"><span data-stu-id="4750c-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="4750c-155">Po zakończeniu tworzenia aplikacji sieci web hello Przejdź w hello Azure Portal toohello grupie zasobów, w którym została utworzona aplikacja hello, i widoczne hello aplikacji sieci web i hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4750c-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="4750c-156">Witaj dodatkowym zasobem z ikoną żarówki hello jest [usługi Application Insights](/services/application-insights/), która umożliwia monitorowanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4750c-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="4750c-157">W hello **grupy zasobów** bloku, kliknij wiersz aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="4750c-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="4750c-159">W bloku aplikacja sieci Web powitania kliknij **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="4750c-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![Adres URL witryny][browse]
4. <span data-ttu-id="4750c-161">W hello WordPress **powitalnej** wprowadzania informacji konfiguracyjnych hello wymagane przez platformę WordPress, a następnie kliknij przycisk **zainstalować WordPress**.</span><span class="sxs-lookup"><span data-stu-id="4750c-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Konfigurowanie usługi WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="4750c-163">Zaloguj się za pomocą poświadczeń hello utworzonych na powitania **powitalnej** strony.</span><span class="sxs-lookup"><span data-stu-id="4750c-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="4750c-164">Zostanie otwarta strona pulpitu nawigacyjnego witryny.</span><span class="sxs-lookup"><span data-stu-id="4750c-164">Your site Dashboard page opens.</span></span>    
   
    ![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="4750c-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4750c-166">Next steps</span></span>
<span data-ttu-id="4750c-167">Przedstawiono sposób toocreate i wdrażanie aplikacji sieci web PHP z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="4750c-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="4750c-168">Aby uzyskać więcej informacji na temat używania struktury PHP na platformie Azure, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4750c-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="4750c-169">Aby uzyskać więcej informacji o tym, jak toowork z aplikacjami sieci Web usługi aplikacji, zobacz linki hello na powitania po lewej stronie powitania stronie (szerokie okna przeglądarki) lub u góry hello hello strony (wąskie okna przeglądarki).</span><span class="sxs-lookup"><span data-stu-id="4750c-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="4750c-170">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="4750c-170">What's changed</span></span>
* <span data-ttu-id="4750c-171">Przewodnik toohello zmian z tooApp witryn sieci Web Service, zobacz [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4750c-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
