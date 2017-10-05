---
title: "Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio"
description: "Dowiedz się, jak używać narzędzi Python Tools for Visual Studio do utworzenia aplikacji sieci Web Django przechowującej dane w wystąpieniu bazy danych MySQL, a następnie, jak ją wdrożyć w funkcji Web Apps w usłudze Azure App Service."
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
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="34ffb-103">Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34ffb-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="34ffb-104">W ramach tego samouczka użyjesz narzędzi [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) w celu utworzenia prostej aplikacji sieci Web z ankietą, wykorzystując jeden z przykładowych szablonów PTVS.</span><span class="sxs-lookup"><span data-stu-id="34ffb-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="34ffb-105">Dowiesz się, jak używać usługi MySQL hostowanej na platformie Azure, jak skonfigurować aplikację sieci Web pod kątem MySQL i jak opublikować tę aplikację w funkcji [Web Apps w usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="34ffb-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="34ffb-106">Informacje zawarte w tym samouczku są również dostępne w poniższym klipie wideo:</span><span class="sxs-lookup"><span data-stu-id="34ffb-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="34ffb-107">[PTVS 2.1: Aplikacja Django z obsługą MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="34ffb-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="34ffb-108">Więcej artykułów o programowaniu aplikacji Web Apps w usłudze Azure App Service przy użyciu narzędzi PTVS, środowisk sieci Web Bottle, Flask i Django oraz usług baz danych Azure Table Storage, MySQL i SQL Database możesz znaleźć w [Centrum deweloperów języka Python].</span><span class="sxs-lookup"><span data-stu-id="34ffb-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="34ffb-109">Chociaż ten artykuł dotyczy usługi App Service, opisane kroki są podobne do programowania [usług Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="34ffb-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34ffb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34ffb-110">Prerequisites</span></span>
* <span data-ttu-id="34ffb-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="34ffb-111">Visual Studio 2015</span></span>
* <span data-ttu-id="34ffb-112">[32-bitowe środowisko Python w wersji 2.7] lub [32-bitowe środowisko Python w wersji 3.4]</span><span class="sxs-lookup"><span data-stu-id="34ffb-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="34ffb-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="34ffb-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="34ffb-114">[Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="34ffb-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="34ffb-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="34ffb-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="34ffb-116">Django 1.9 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="34ffb-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="34ffb-117">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="34ffb-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="34ffb-118">Karta kredytowa nie jest wymagana i nie musisz się do niczego zobowiązywać.</span><span class="sxs-lookup"><span data-stu-id="34ffb-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="34ffb-119">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="34ffb-119">Create the Project</span></span>
<span data-ttu-id="34ffb-120">W tej sekcji utworzysz projekt programu Visual Studio przy użyciu przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="34ffb-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="34ffb-121">Utworzysz środowisko wirtualne i zainstalujesz wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="34ffb-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="34ffb-122">Utworzysz także lokalną bazę danych przy użyciu systemu SQLite.</span><span class="sxs-lookup"><span data-stu-id="34ffb-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="34ffb-123">Następnie uruchomisz aplikację lokalnie.</span><span class="sxs-lookup"><span data-stu-id="34ffb-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="34ffb-124">W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="34ffb-125">Szablony projektu z [Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio] są dostępne w menu **Python**, **Przykłady**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="34ffb-126">Wybierz pozycję **Polls Django Web Project** (Projekt sieci Web Django z ankietą) i kliknij przycisk OK, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="34ffb-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="34ffb-128">Zostanie wyświetlony monit o zainstalowanie pakietów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="34ffb-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="34ffb-129">Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-129">Select **Install into a virtual environment**.</span></span>
   
    ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="34ffb-131">Wybierz jako podstawowy interpreter **Python 2.7** lub **Python 3.4**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="34ffb-133">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="34ffb-134">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="34ffb-135">Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych SQLite w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="34ffb-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="34ffb-136">Postępuj zgodnie z monitami, aby utworzyć użytkownika.</span><span class="sxs-lookup"><span data-stu-id="34ffb-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="34ffb-137">Sprawdź, czy aplikacja działa, naciskając `F5`.</span><span class="sxs-lookup"><span data-stu-id="34ffb-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="34ffb-138">Kliknij pozycję **Zaloguj** na górnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="34ffb-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Pasek nawigacyjny Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="34ffb-140">Wprowadź poświadczenia użytkownika, który został utworzony podczas synchronizowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="34ffb-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Formularz logowania](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="34ffb-142">Kliknij pozycję **Utwórz przykładową ankietę**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-142">Click **Create Sample Polls**.</span></span>
    
     ![Tworzenie przykładowej ankiety](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="34ffb-144">Kliknij ankietę i zagłosuj.</span><span class="sxs-lookup"><span data-stu-id="34ffb-144">Click on a poll and vote.</span></span>
    
     ![Głosowanie w przykładowej ankiecie](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="34ffb-146">Tworzenie bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="34ffb-146">Create a MySQL Database</span></span>
<span data-ttu-id="34ffb-147">Utworzysz bazę danych ClearDB MySQL hostowaną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34ffb-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="34ffb-148">Ewentualnie możesz utworzyć własną maszynę wirtualną działającą na platformie Azure, a następnie samodzielnie zainstalować środowisko MySQL i administrować nim.</span><span class="sxs-lookup"><span data-stu-id="34ffb-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="34ffb-149">Wykonując poniższe kroki, możesz utworzyć bazę danych z użyciem planu Free.</span><span class="sxs-lookup"><span data-stu-id="34ffb-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="34ffb-150">Zaloguj się do [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="34ffb-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="34ffb-151">W górnej części okienka nawigacji kliknij kolejno pozycje: **NOWE**, **Dane i przechowywanie**, **Baza danych MySQL**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="34ffb-152">Skonfiguruj nową bazę danych MySQL, tworząc nową grupę zasobów i wybierając dla niej odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="34ffb-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="34ffb-153">Po utworzeniu bazy danych MySQL kliknij przycisk **Właściwości** w bloku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="34ffb-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="34ffb-154">Użyj przycisku kopiowania, aby umieścić wartość elementu **PARAMETRY POŁĄCZENIA** w Schowku.</span><span class="sxs-lookup"><span data-stu-id="34ffb-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="34ffb-155">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="34ffb-155">Configure the Project</span></span>
<span data-ttu-id="34ffb-156">W tej sekcji skonfigurujesz swoją aplikację sieci Web tak, aby używała utworzonej przed chwilą bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="34ffb-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="34ffb-157">Zainstalujesz również dodatkowe pakiety Python niezbędne do korzystania z baz danych MySQL w Django.</span><span class="sxs-lookup"><span data-stu-id="34ffb-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="34ffb-158">Następnie uruchomisz aplikację sieci Web lokalnie.</span><span class="sxs-lookup"><span data-stu-id="34ffb-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="34ffb-159">W programie Visual Studio otwórz plik **settings.py** z folderu *NazwaProjektu*.</span><span class="sxs-lookup"><span data-stu-id="34ffb-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="34ffb-160">Wklej tymczasowo parametry połączenia w edytorze.</span><span class="sxs-lookup"><span data-stu-id="34ffb-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="34ffb-161">Parametry połączenia mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="34ffb-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="34ffb-162">Zmień domyślny **APARAT** bazy danych na MySQL i ustaw wartości elementów **NAZWA**, **UŻYTKOWNIK**, **HASŁO** i **HOST** zgodnie z elementem **PARAMETRY POŁĄCZENIA**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="34ffb-163">W Eksploratorze rozwiązań w obszarze **Środowiska Python** kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz polecenie **Zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="34ffb-164">Zainstaluj pakiet `mysqlclient`, korzystając z polecenia **pip**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Okno dialogowe Instalowanie pakietu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="34ffb-166">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="34ffb-167">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="34ffb-168">Spowoduje to utworzenie tabel w bazie danych MySQL utworzonej w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="34ffb-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="34ffb-169">Postępuj zgodnie z monitami, aby utworzyć użytkownika. Nie musi on być taki sam, jak użytkownik w bazie danych SQLite utworzonej w pierwszej sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="34ffb-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="34ffb-170">Uruchom aplikację klawiszem `F5`.</span><span class="sxs-lookup"><span data-stu-id="34ffb-170">Run the application with `F5`.</span></span> <span data-ttu-id="34ffb-171">Ankieta utworzona za pomocą funkcji **Tworzenie przykładowej ankiety** oraz dane przesłane podczas głosowania zostaną zserializowane w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="34ffb-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="34ffb-172">Publikowanie aplikacji sieci Web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="34ffb-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="34ffb-173">Zestaw .NET SDK platformy Azure pozwala łatwo wdrożyć aplikację sieci Web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="34ffb-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="34ffb-174">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="34ffb-176">Kliknij pozycję **Usługa aplikacji Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="34ffb-177">Kliknij pozycję **Nowa**, aby utworzyć nową aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="34ffb-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="34ffb-178">Wypełnij poniższe pola i kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="34ffb-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="34ffb-179">**Nazwa aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="34ffb-179">**Web App name**</span></span>
   * <span data-ttu-id="34ffb-180">**Plan usługi App Service**</span><span class="sxs-lookup"><span data-stu-id="34ffb-180">**App Service plan**</span></span>
   * <span data-ttu-id="34ffb-181">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="34ffb-181">**Resource group**</span></span>
   * <span data-ttu-id="34ffb-182">**Region**</span><span class="sxs-lookup"><span data-stu-id="34ffb-182">**Region**</span></span>
   * <span data-ttu-id="34ffb-183">W polu **Serwer bazy danych** pozostaw wartość **Brak bazy danych**</span><span class="sxs-lookup"><span data-stu-id="34ffb-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="34ffb-184">Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="34ffb-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="34ffb-185">Opublikowana aplikacja sieci Web zostanie automatycznie otwarta w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="34ffb-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="34ffb-186">Aplikacja sieci Web powinna działać zgodnie z oczekiwaniami i z wykorzystaniem bazy danych **MySQL** hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34ffb-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="34ffb-188">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="34ffb-188">Congratulations!</span></span> <span data-ttu-id="34ffb-189">Twoja aplikacja sieci Web oparta na bazie danych MySQL została pomyślnie opublikowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34ffb-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34ffb-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34ffb-190">Next steps</span></span>
<span data-ttu-id="34ffb-191">Aby dowiedzieć się więcej na temat narzędzi Python Tools for Visual Studio, Django i MySQL, kliknij poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="34ffb-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="34ffb-192">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="34ffb-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="34ffb-193">[Projekty sieci Web]</span><span class="sxs-lookup"><span data-stu-id="34ffb-193">[Web Projects]</span></span>
  * <span data-ttu-id="34ffb-194">[Projekty usługi w chmurze]</span><span class="sxs-lookup"><span data-stu-id="34ffb-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="34ffb-195">[Debugowanie zdalne na platformie Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="34ffb-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="34ffb-196">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="34ffb-196">[Django Documentation]</span></span>
* <span data-ttu-id="34ffb-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="34ffb-197">[MySQL]</span></span>

<span data-ttu-id="34ffb-198">Więcej informacji możesz znaleźć w [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="34ffb-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centrum deweloperów języka Python]: /develop/python/
[usług Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
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
