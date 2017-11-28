---
title: "aaaDjango i bazy danych MySQL na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych MySQL i wdróż je tooAzure aplikacji usługi sieci Web aplikacji."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="c481d-103">Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c481d-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="c481d-104">W tym samouczku użyjesz [narzędzi Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony.</span><span class="sxs-lookup"><span data-stu-id="c481d-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="c481d-105">Dowiesz się, jak toouse usługi MySQL hostowanej na platformie Azure, jak tooconfigure hello toouse aplikacji sieci web MySQL i jak toopublish hello aplikacji sieci web zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c481d-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="c481d-106">Hello informacje zawarte w tym samouczku jest również dostępna w powitania po wideo:</span><span class="sxs-lookup"><span data-stu-id="c481d-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="c481d-107">[PTVS 2.1: Aplikacja Django z obsługą MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="c481d-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="c481d-108">Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="c481d-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="c481d-109">Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].</span><span class="sxs-lookup"><span data-stu-id="c481d-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c481d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c481d-110">Prerequisites</span></span>
* <span data-ttu-id="c481d-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c481d-111">Visual Studio 2015</span></span>
* <span data-ttu-id="c481d-112">[32-bitowe środowisko Python w wersji 2.7] lub [32-bitowe środowisko Python w wersji 3.4]</span><span class="sxs-lookup"><span data-stu-id="c481d-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="c481d-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c481d-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="c481d-114">[Python Tools 2.2 for Visual Studio przykładów VSIX]</span><span class="sxs-lookup"><span data-stu-id="c481d-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="c481d-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="c481d-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="c481d-116">Django 1.9 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="c481d-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="c481d-117">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="c481d-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c481d-118">Karta kredytowa nie jest wymagana i nie musisz się do niczego zobowiązywać.</span><span class="sxs-lookup"><span data-stu-id="c481d-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="c481d-119">Utwórz hello projektu</span><span class="sxs-lookup"><span data-stu-id="c481d-119">Create hello Project</span></span>
<span data-ttu-id="c481d-120">W tej sekcji utworzysz projekt programu Visual Studio przy użyciu przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="c481d-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="c481d-121">Utworzysz środowisko wirtualne i zainstalujesz wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="c481d-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="c481d-122">Utworzysz także lokalną bazę danych przy użyciu systemu SQLite.</span><span class="sxs-lookup"><span data-stu-id="c481d-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="c481d-123">Następnie uruchomisz aplikację hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c481d-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="c481d-124">W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="c481d-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="c481d-125">Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**.</span><span class="sxs-lookup"><span data-stu-id="c481d-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="c481d-126">Wybierz **projektu sieci Web Django sond** i kliknij przycisk OK toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="c481d-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="c481d-128">Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie.</span><span class="sxs-lookup"><span data-stu-id="c481d-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="c481d-129">Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="c481d-129">Select **Install into a virtual environment**.</span></span>
   
    ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="c481d-131">Wybierz **Python 2.7** lub **języka Python 3.4** jako podstawowy interpreter hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="c481d-133">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.</span><span class="sxs-lookup"><span data-stu-id="c481d-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="c481d-134">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="c481d-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="c481d-135">Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych sqlite w folderze projektu hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="c481d-136">Wykonaj hello toocreate monity użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c481d-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="c481d-137">Upewnij się, że aplikacja hello działa, naciskając `F5`.</span><span class="sxs-lookup"><span data-stu-id="c481d-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="c481d-138">Kliknij przycisk **Zaloguj** z paska nawigacji hello u góry hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Pasek nawigacyjny Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="c481d-140">Wprowadź poświadczenia hello hello użytkownika, który został utworzony podczas synchronizowania bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Formularz logowania](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="c481d-142">Kliknij pozycję **Utwórz przykładową ankietę**.</span><span class="sxs-lookup"><span data-stu-id="c481d-142">Click **Create Sample Polls**.</span></span>
    
     ![Tworzenie przykładowej ankiety](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="c481d-144">Kliknij ankietę i zagłosuj.</span><span class="sxs-lookup"><span data-stu-id="c481d-144">Click on a poll and vote.</span></span>
    
     ![Głosowanie w przykładowej ankiecie](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="c481d-146">Tworzenie bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="c481d-146">Create a MySQL Database</span></span>
<span data-ttu-id="c481d-147">W przypadku bazy danych hello utworzysz danych ClearDB MySQL hostowaną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c481d-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="c481d-148">Ewentualnie możesz utworzyć własną maszynę wirtualną działającą na platformie Azure, a następnie samodzielnie zainstalować środowisko MySQL i administrować nim.</span><span class="sxs-lookup"><span data-stu-id="c481d-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="c481d-149">Wykonując poniższe kroki, możesz utworzyć bazę danych z użyciem planu Free.</span><span class="sxs-lookup"><span data-stu-id="c481d-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="c481d-150">Zaloguj się za toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c481d-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="c481d-151">W górnej części okienka nawigacji hello hello, kliknij **nowy**, następnie kliknij przycisk **dane i magazyn**, a następnie kliknij przycisk **baza danych MySQL**.</span><span class="sxs-lookup"><span data-stu-id="c481d-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="c481d-152">Skonfiguruj hello nową bazę danych MySQL, tworząc nową grupę zasobów, a następnie wybierz powitania dla niej odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="c481d-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="c481d-153">Po utworzeniu bazy danych MySQL powitania kliknij **właściwości** w hello bloku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c481d-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="c481d-154">Hello kopiowania przycisk tooput hello wartości **ciąg połączenia** hello w Schowku.</span><span class="sxs-lookup"><span data-stu-id="c481d-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="c481d-155">Skonfiguruj hello projektu</span><span class="sxs-lookup"><span data-stu-id="c481d-155">Configure hello Project</span></span>
<span data-ttu-id="c481d-156">W tej sekcji skonfigurujesz naszych sieci web aplikacji toouse hello baza danych MySQL utworzonej przed chwilą.</span><span class="sxs-lookup"><span data-stu-id="c481d-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="c481d-157">Zainstalujesz również dodatkowe Python pakietów wymagane toouse baz danych MySQL przy użyciu platformy Django.</span><span class="sxs-lookup"><span data-stu-id="c481d-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="c481d-158">Następnie uruchomisz aplikację sieci web hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c481d-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="c481d-159">W programie Visual Studio Otwórz **settings.py**, z hello *ProjectName* folderu.</span><span class="sxs-lookup"><span data-stu-id="c481d-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="c481d-160">Wklej tymczasowo parametry połączenia hello w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="c481d-161">Witaj parametry połączenia mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="c481d-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="c481d-162">Zmień hello domyślna baza danych **aparat** toouse MySQL i ustaw wartości hello **nazwa**, **użytkownika**, **hasło** i  **HOST** z hello **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="c481d-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="c481d-163">W Eksploratorze rozwiązań w obszarze **środowiska Python**, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="c481d-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="c481d-164">Zainstaluj pakiet hello `mysqlclient` przy użyciu **pip**.</span><span class="sxs-lookup"><span data-stu-id="c481d-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Okno dialogowe Instalowanie pakietu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="c481d-166">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.</span><span class="sxs-lookup"><span data-stu-id="c481d-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="c481d-167">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="c481d-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="c481d-168">Spowoduje to utworzenie tabel hello hello bazy danych MySQL utworzonej w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="c481d-169">Wykonaj hello toocreate monity użytkownika, który nie ma toomatch hello użytkownika w bazie danych sqlite hello utworzone w pierwszej sekcji tego artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="c481d-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="c481d-170">Uruchamianie aplikacji hello z `F5`.</span><span class="sxs-lookup"><span data-stu-id="c481d-170">Run hello application with `F5`.</span></span> <span data-ttu-id="c481d-171">Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w hello baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c481d-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="c481d-172">Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="c481d-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="c481d-173">Hello Azure .NET SDK udostępnia toodeploy łatwy sposób tooAzure aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c481d-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="c481d-174">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c481d-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="c481d-176">Kliknij pozycję **Usługa aplikacji Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c481d-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c481d-177">Polecenie **nowy** toocreate nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c481d-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="c481d-178">Wypełnij następujące pola hello i kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="c481d-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="c481d-179">**Nazwa aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="c481d-179">**Web App name**</span></span>
   * <span data-ttu-id="c481d-180">**Plan usługi App Service**</span><span class="sxs-lookup"><span data-stu-id="c481d-180">**App Service plan**</span></span>
   * <span data-ttu-id="c481d-181">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="c481d-181">**Resource group**</span></span>
   * <span data-ttu-id="c481d-182">**Region**</span><span class="sxs-lookup"><span data-stu-id="c481d-182">**Region**</span></span>
   * <span data-ttu-id="c481d-183">Pozostaw **serwera bazy danych** ustawić także**bazy danych**</span><span class="sxs-lookup"><span data-stu-id="c481d-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="c481d-184">Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="c481d-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="c481d-185">Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="c481d-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="c481d-186">Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **MySQL** bazy danych hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c481d-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="c481d-188">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="c481d-188">Congratulations!</span></span> <span data-ttu-id="c481d-189">Został pomyślnie opublikowany Twojej tooAzure aplikacji sieci web opartych na MySQL.</span><span class="sxs-lookup"><span data-stu-id="c481d-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c481d-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c481d-190">Next steps</span></span>
<span data-ttu-id="c481d-191">Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Django i MySQL.</span><span class="sxs-lookup"><span data-stu-id="c481d-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="c481d-192">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c481d-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="c481d-193">[Projekty sieci Web]</span><span class="sxs-lookup"><span data-stu-id="c481d-193">[Web Projects]</span></span>
  * <span data-ttu-id="c481d-194">[Projekty usługi w chmurze]</span><span class="sxs-lookup"><span data-stu-id="c481d-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="c481d-195">[Debugowanie zdalne na platformie Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="c481d-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="c481d-196">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="c481d-196">[Django Documentation]</span></span>
* <span data-ttu-id="c481d-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="c481d-197">[MySQL]</span></span>

<span data-ttu-id="c481d-198">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c481d-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[32-bitowe środowisko Python w wersji 3.4]: http://go.microsoft.com/fwlink/?LinkId=517191
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Dokumentacja platformy Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
