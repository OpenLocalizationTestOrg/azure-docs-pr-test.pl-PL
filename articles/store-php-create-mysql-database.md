---
title: "aaaCreate i połącz tooa baza danych MySQL na platformie Azure"
description: "Dowiedz się, jak toouse hello Azure toocreate portalu bazę danych MySQL, a następnie połącz tooit z aplikacji sieci web PHP na platformie Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="32ff5-103">Tworzenie i łączenie tooa baza danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="32ff5-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="32ff5-104">Ten samouczek pokazuje, jak hello bazę danych MySQL toocreate [portalu Azure](https://portal.azure.com) (dostawca jest [ClearDB](http://www.cleardb.com/)) i jak tooit tooconnect za pomocą języka PHP sieci web aplikacji uruchomionej [usłudze Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="32ff5-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="32ff5-105">Można również utworzyć bazę danych MySQL jako część [szablon aplikacji Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="32ff5-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="32ff5-106">Utwórz bazę danych MySQL w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="32ff5-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="32ff5-107">toocreate bazy danych MySQL w hello portalu Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="32ff5-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="32ff5-108">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32ff5-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="32ff5-109">W menu po lewej stronie powitania kliknij **nowy** > **dane i magazyn** > **baza danych MySQL**.</span><span class="sxs-lookup"><span data-stu-id="32ff5-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Utwórz bazę danych MySQL na platformie Azure - start](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="32ff5-111">W hello nową bazę danych MySQL [bloku](azure-portal-overview.md), skonfiguruj nową bazę danych MySQL w następujący sposób (*bloku*: strony portalu, który zostanie otwarty w poziomie):</span><span class="sxs-lookup"><span data-stu-id="32ff5-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="32ff5-112">**Nazwa bazy danych**: wpisz nazwę unikatową identyfikację</span><span class="sxs-lookup"><span data-stu-id="32ff5-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="32ff5-113">**Subskrypcja**: Wybierz hello toouse subskrypcji</span><span class="sxs-lookup"><span data-stu-id="32ff5-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="32ff5-114">**Bazy danych typu**: Wybierz **Shared** ekonomicznych lub wolnego warstw, lub **dedykowana** tooget dedykowanego zasobów.</span><span class="sxs-lookup"><span data-stu-id="32ff5-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="32ff5-115">**Grupa zasobów**: Dodaj istniejącą tooan bazy danych MySQL hello [grupy zasobów](azure-resource-manager/resource-group-overview.md) lub umieść je w nowej.</span><span class="sxs-lookup"><span data-stu-id="32ff5-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="32ff5-116">Zasoby w tej samej grupie można łatwo zarządzać razem powitalne.</span><span class="sxs-lookup"><span data-stu-id="32ff5-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="32ff5-117">**Lokalizacja**: Wybierz lokalizację tooyou Zamknij.</span><span class="sxs-lookup"><span data-stu-id="32ff5-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="32ff5-118">Podczas dodawania tooan istniejącej grupy zasobów, możesz lokalizacja grupy zasobów toohello zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="32ff5-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="32ff5-119">**Warstwy cenowej**: kliknij **warstwy cenowej**, następnie wybierz opcję cenową (**Mercury** warstwa jest bezpłatna), a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="32ff5-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="32ff5-120">**Postanowienia prawne**: kliknij **postanowienia prawne**, przejrzyj szczegóły zakupu hello i kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="32ff5-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="32ff5-121">**Numer PIN toodashboard**: zaznaczyć tooaccess bezpośrednio z poziomu pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="32ff5-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="32ff5-122">Jest to szczególnie przydatne, jeśli nie znasz jeszcze nawigacji w portalu.</span><span class="sxs-lookup"><span data-stu-id="32ff5-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="32ff5-123">Witaj następującego zrzutu ekranu jest tylko przykładem sposobu konfigurowania bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="32ff5-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Utwórz bazę danych MySQL na platformie Azure — Konfigurowanie](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="32ff5-125">Po zakończeniu konfigurowania, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="32ff5-125">When you're done configuring, click **Create**.</span></span>

    ![Utwórz bazę danych MySQL na platformie Azure — tworzenie](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="32ff5-127">Zostanie wyświetlone powiadomienie wyskakujące, dzięki czemu będzie wiadomo, że rozpoczęło się wdrażanie.</span><span class="sxs-lookup"><span data-stu-id="32ff5-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Trwa tworzenie bazy danych MySQL na platformie Azure-](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="32ff5-129">Otrzymasz innej wyskakujących po pomyślnym zakończeniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="32ff5-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="32ff5-130">Hello portal również zostanie automatycznie otworzyć bloku bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="32ff5-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="32ff5-131">Połącz tooyour baza danych MySQL</span><span class="sxs-lookup"><span data-stu-id="32ff5-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="32ff5-132">informacje o połączeniu hello toosee dla nowej bazy danych MySQL, wystarczy kliknąć **właściwości** w bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="32ff5-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Utwórz bazę danych MySQL na platformie Azure — blok bazy danych MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="32ff5-134">Informacje o połączeniu można teraz używać we wszystkich aplikacjach sieci web.</span><span class="sxs-lookup"><span data-stu-id="32ff5-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="32ff5-135">Przykład pokazujący, jak informacje o połączeniu hello toouse z prostej aplikacji PHP są dostępne [tutaj](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="32ff5-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="32ff5-136">Łączenie aplikacji sieci web Laravel (od hello PHP get samouczku)</span><span class="sxs-lookup"><span data-stu-id="32ff5-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="32ff5-137">Załóżmy, że użytkownik właśnie zakończono hello samouczek [tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web PHP](app-service-web/app-service-web-php-get-started.md) i mieć [Laravel](https://www.laravel.com/) aplikacji sieci web działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="32ff5-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="32ff5-138">Możesz łatwo dodać aplikację Laravel tooyour możliwości bazy danych.</span><span class="sxs-lookup"><span data-stu-id="32ff5-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="32ff5-139">Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="32ff5-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="32ff5-140">Witaj następujących krokach założono zakończeniu samouczka hello [tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="32ff5-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="32ff5-141">Skonfiguruj aplikację Laravel hello w bazie danych MySQL toohello toopoint środowisko rozwoju lokalnego.</span><span class="sxs-lookup"><span data-stu-id="32ff5-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="32ff5-142">toodo, otwórz `.env` z aplikacji Laravel katalogu głównego i skonfigurować opcje bazy danych MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="32ff5-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="32ff5-143">W hello **właściwości** bloku może hello nazwę bazy danych MySQL lub może nie być hello jedną wyświetlany w hello **Nazwa bazy danych** pola.</span><span class="sxs-lookup"><span data-stu-id="32ff5-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="32ff5-144">Jest lepsze toocheck hello bazy danych parametru w hello **ciąg połączenia** pola.</span><span class="sxs-lookup"><span data-stu-id="32ff5-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Trwa tworzenie bazy danych MySQL na platformie Azure-](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="32ff5-146">Witaj najszybszy sposób tooverify, ma dostęp MySQL jest toouse [Laravel przez domyślne uwierzytelnianie szkieletów](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="32ff5-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="32ff5-147">W hello terminal wiersza polecenia Uruchom następujące polecenia z katalogu głównego aplikacji Laravel hello:</span><span class="sxs-lookup"><span data-stu-id="32ff5-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="32ff5-148">pierwsze polecenie Hello tworzy tabele hello na platformie Azure, oparte na wstępnie zdefiniowanych migracje w hello `database/migrations` katalogu, a drugie polecenie hello rusztowania hello podstawowe widoków i tras do uwierzytelniania i rejestracja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32ff5-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="32ff5-149">Teraz uruchomić serwera wdrożeniowego hello:</span><span class="sxs-lookup"><span data-stu-id="32ff5-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="32ff5-150">W przeglądarce hello Przejdź toohttp://localhost:8000 i zarejestrować nowego użytkownika, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="32ff5-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Połączenia bazy danych tooMySQL na platformie Azure — zarejestrowania użytkownika](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="32ff5-152">Wykonaj hello interfejsu użytkownika monitu hello ukończenia rejestracji.</span><span class="sxs-lookup"><span data-stu-id="32ff5-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="32ff5-153">Po zakończeniu rejestracji, będziesz się logować.</span><span class="sxs-lookup"><span data-stu-id="32ff5-153">Once registration completes, you will be logged in.</span></span>

    ![Połączenia bazy danych tooMySQL na platformie Azure — zarejestrowania użytkownika](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="32ff5-155">Teraz tworzysz aplikację przed hello baza danych MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="32ff5-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="32ff5-156">Teraz, po prostu potrzebujesz tooreplicate Twojego `.env` ustawienia tooyour aplikacji sieci web Azure.</span><span class="sxs-lookup"><span data-stu-id="32ff5-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="32ff5-157">Uruchom następujące polecenia interfejsu wiersza polecenia Azure hello:</span><span class="sxs-lookup"><span data-stu-id="32ff5-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="32ff5-158">Następnie Zatwierdź i Wypchnij tooAzure hello lokalne zmiany wprowadzone wcześniej uruchomionej `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="32ff5-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="32ff5-159">Przeglądaj toohello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="32ff5-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="32ff5-160">Zaloguj się za pomocą poświadczeń użytkownika hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="32ff5-160">Log in using hello user credentials you created earlier.</span></span>

    ![Połączenia bazy danych tooMySQL na platformie Azure — przejście tooAzure aplikacji sieci web](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="32ff5-162">Po zalogowaniu, powinna zostać wyświetlona hello przyjazną ekranu po logowaniu.</span><span class="sxs-lookup"><span data-stu-id="32ff5-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Połączenia bazy danych tooMySQL na platformie Azure — zalogowany](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="32ff5-164">Gratulacje, aplikacji sieci web PHP na platformie Azure jest teraz dostęp do danych z bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="32ff5-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32ff5-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32ff5-165">Next steps</span></span>
<span data-ttu-id="32ff5-166">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="32ff5-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
