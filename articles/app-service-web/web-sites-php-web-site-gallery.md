---
title: "Tworzenie aplikacji sieci Web WordPress w usłudze Azure App Service | Microsoft Docs"
description: "Dowiedz się, jak utworzyć nową aplikację sieci Web platformy Azure dla bloga WordPress przy użyciu witryny Azure Portal."
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="4d827-103">Tworzenie aplikacji sieci Web WordPress w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4d827-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="4d827-104">Ten samouczek pokazuje, jak wdrożyć witrynę bloga WordPress z poziomu portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d827-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="4d827-105">Po użyciu samouczka będziesz mieć witrynę bloga WordPress uruchomioną w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4d827-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="4d827-107">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="4d827-107">You'll learn:</span></span>

* <span data-ttu-id="4d827-108">Jak znajdować szablon aplikacji w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d827-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="4d827-109">Jak utworzyć aplikację sieci Web w usłudze Azure App Service przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="4d827-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="4d827-110">Jak konfigurować ustawienia usługi Azure App Service dla nowej aplikacji sieci Web i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4d827-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="4d827-111">Portal Azure Marketplace udostępnia szeroką gamę popularnych aplikacji sieci Web opracowanych przez firmę Microsoft, inne firmy oraz zespoły związane z inicjatywami dotyczącymi oprogramowania typu open source.</span><span class="sxs-lookup"><span data-stu-id="4d827-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="4d827-112">Aplikacje sieci Web są tworzone w różnych popularnych platformach, takich jak [PHP](/develop/nodejs/) w tym przykładzie WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) i [Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="4d827-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="4d827-113">Jedynym oprogramowaniem potrzebnym do utworzenia aplikacji sieci Web z poziomu portalu Azure Marketplace jest przeglądarka, za pomocą której korzystasz z witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d827-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="4d827-114">Witryna WordPress wdrażana w tym samouczku korzysta z bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="4d827-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="4d827-115">Jeśli chcesz zamiast tego użyć usługi SQL Database, zobacz stronę rozwiązania [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="4d827-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="4d827-116">Rozwiązanie **Project Nami** jest również dostępne za pośrednictwem portalu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d827-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="4d827-117">Do wykonania kroków tego samouczka potrzebne jest konto platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4d827-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="4d827-118">Jeśli nie masz konta, możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) lub [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4d827-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="4d827-119">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="4d827-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="4d827-120">W tej lokalizacji możesz od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="4d827-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="4d827-121">Wybieranie platformy WordPress i konfigurowanie dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4d827-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="4d827-122">Zaloguj się do [Portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d827-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4d827-123">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="4d827-123">Click **New**.</span></span>
   
    ![Kliknięcie przycisku Nowe][5]
3. <span data-ttu-id="4d827-125">Wyszukaj wyrażenie **WordPress**, a następnie kliknij pozycję **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="4d827-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="4d827-126">Jeśli chcesz użyć usługi SQL Database zamiast MySQL, wyszukaj wyrażenie **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="4d827-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![Pozycja WordPress na liście][7]
4. <span data-ttu-id="4d827-128">Po przeczytaniu opisu aplikacji WordPress kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4d827-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Przycisk Utwórz](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="4d827-130">Wprowadź nazwę aplikacji sieci Web w polu **Aplikacja sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="4d827-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="4d827-131">Ta nazwa musi być unikatowa w domenie azurewebsites.net, ponieważ adres URL aplikacji sieci Web będzie miał format {nazwa}.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="4d827-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="4d827-132">Jeśli wprowadzona nazwa nie jest unikatowa, w polu tekstowym jest wyświetlany czerwony wykrzyknik.</span><span class="sxs-lookup"><span data-stu-id="4d827-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="4d827-133">Jeśli masz więcej niż jedną subskrypcję, wybierz odpowiednią subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="4d827-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="4d827-134">Wybierz **grupę zasobów** lub utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="4d827-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="4d827-135">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d827-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="4d827-136">Wybierz pozycję **Plan usługi App Service/Lokalizacja** lub utwórz nowy plan.</span><span class="sxs-lookup"><span data-stu-id="4d827-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="4d827-137">Aby uzyskać więcej informacji na temat planów usługi App Service, zobacz [Omówienie planów usługi Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d827-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="4d827-138">Kliknij pozycję **Baza danych**, a następnie w bloku **Nowa baza danych MySQL** podaj wartości wymagane do skonfigurowania bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="4d827-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="4d827-139">a.</span><span class="sxs-lookup"><span data-stu-id="4d827-139">a.</span></span> <span data-ttu-id="4d827-140">Wprowadź nową nazwę lub pozostaw nazwę domyślną.</span><span class="sxs-lookup"><span data-stu-id="4d827-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="4d827-141">b.</span><span class="sxs-lookup"><span data-stu-id="4d827-141">b.</span></span> <span data-ttu-id="4d827-142">Pozostaw opcję **Typ bazy danych** ustawioną na wartość **Udostępniona**.</span><span class="sxs-lookup"><span data-stu-id="4d827-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="4d827-143">c.</span><span class="sxs-lookup"><span data-stu-id="4d827-143">c.</span></span> <span data-ttu-id="4d827-144">Wybierz tę samą lokalizację, którą wybrano dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4d827-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="4d827-145">d.</span><span class="sxs-lookup"><span data-stu-id="4d827-145">d.</span></span> <span data-ttu-id="4d827-146">Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="4d827-146">Choose a pricing tier.</span></span> <span data-ttu-id="4d827-147">Warstwa Mercury (bezpłatnie z minimalnymi dopuszczalnymi połączeniami i miejscem na dysku) jest odpowiednia dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="4d827-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="4d827-148">W bloku **Nowa baza danych MySQL** kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d827-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="4d827-149">W bloku **WordPress** zaakceptuj postanowienia prawne, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4d827-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="4d827-151">Zazwyczaj tworzenie aplikacji sieci Web przez usługę Azure App Service trwa nie dłużej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="4d827-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="4d827-152">Możesz obserwować postęp, klikając ikonę dzwonka w górnej części strony portalu.</span><span class="sxs-lookup"><span data-stu-id="4d827-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Wskaźnik postępu](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="4d827-154">Uruchamianie aplikacji sieci Web WordPress i zarządzanie nią</span><span class="sxs-lookup"><span data-stu-id="4d827-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="4d827-155">Po ukończeniu tworzenia aplikacji sieci Web przejdź w witrynie Azure Portal do grupy zasobów, w której utworzono aplikację, aby wyświetlić aplikację sieci Web i bazę danych.</span><span class="sxs-lookup"><span data-stu-id="4d827-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="4d827-156">Dodatkowym zasobem z ikoną żarówki jest usługa [Application Insights](/services/application-insights/), która umożliwia monitorowanie aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4d827-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="4d827-157">W bloku **Grupa zasobów** kliknij wiersz aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4d827-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="4d827-159">W bloku Aplikacja sieci Web kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="4d827-159">In the Web app blade, click **Browse**.</span></span>
   
    ![Adres URL witryny][browse]
4. <span data-ttu-id="4d827-161">Na stronie **Welcome** (Powitanie) platformy WordPress wprowadź informacje konfiguracyjne wymagane przez platformę WordPress, a następnie kliknij pozycję **Install WordPress** (Zainstaluj platformę WordPress).</span><span class="sxs-lookup"><span data-stu-id="4d827-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Konfigurowanie usługi WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="4d827-163">Zaloguj się przy użyciu poświadczeń utworzonych na stronie **Welcome** (Powitanie).</span><span class="sxs-lookup"><span data-stu-id="4d827-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="4d827-164">Zostanie otwarta strona pulpitu nawigacyjnego witryny.</span><span class="sxs-lookup"><span data-stu-id="4d827-164">Your site Dashboard page opens.</span></span>    
   
    ![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="4d827-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d827-166">Next steps</span></span>
<span data-ttu-id="4d827-167">Przedstawiono sposób tworzenia i wdrożenia aplikacji sieci Web PHP z poziomu galerii.</span><span class="sxs-lookup"><span data-stu-id="4d827-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="4d827-168">Aby uzyskać więcej informacji na temat używania struktury PHP na platformie Azure, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4d827-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="4d827-169">Aby uzyskać więcej informacji na temat sposobu pracy z aplikacjami Web Apps w usłudze App Service, zobacz linki po lewej stronie (szerokie okna przeglądarki) lub w górnej części strony (wąskie okna przeglądarki).</span><span class="sxs-lookup"><span data-stu-id="4d827-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="4d827-170">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="4d827-170">What's changed</span></span>
* <span data-ttu-id="4d827-171">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="4d827-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
