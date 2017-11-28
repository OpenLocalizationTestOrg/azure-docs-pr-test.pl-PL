---
title: "aaaDjango i bazy danych SQL na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych SQL i wdróż je tooAzure aplikacji usługi sieci Web aplikacji."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="ec0e8-103">Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec0e8-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="ec0e8-104">W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="ec0e8-105">W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="ec0e8-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="ec0e8-106">Firma Microsoft dowiesz się, jak toouse bazy danych SQL hostowanej na platformie Azure, jak tooconfigure hello toouse aplikacji sieci web bazy danych SQL i jak toopublish hello aplikacji sieci web za[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ec0e8-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="ec0e8-107">Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="ec0e8-108">Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].</span><span class="sxs-lookup"><span data-stu-id="ec0e8-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec0e8-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ec0e8-109">Prerequisites</span></span>
* <span data-ttu-id="ec0e8-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ec0e8-110">Visual Studio 2015</span></span>
* <span data-ttu-id="ec0e8-111">[32-bitowe środowisko Python w wersji 2.7]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="ec0e8-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="ec0e8-113">[Python Tools 2.2 for Visual Studio przykładów VSIX]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="ec0e8-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="ec0e8-115">Django 1.9 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="ec0e8-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ec0e8-116">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ec0e8-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="ec0e8-118">Utwórz hello projektu</span><span class="sxs-lookup"><span data-stu-id="ec0e8-118">Create hello Project</span></span>
<span data-ttu-id="ec0e8-119">W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="ec0e8-120">Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="ec0e8-121">Utworzymy lokalnej bazy danych przy użyciu systemu sqlite.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="ec0e8-122">Następnie hello aplikacji sieci web zostanie uruchomiony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="ec0e8-123">W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="ec0e8-124">Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="ec0e8-125">Wybierz **projektu sieci Web Django sond** i kliknij przycisk OK toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="ec0e8-127">Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="ec0e8-128">Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-128">Select **Install into a virtual environment**.</span></span>

     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="ec0e8-130">Wybierz **Python 2.7** jako podstawowy interpreter hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="ec0e8-132">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="ec0e8-133">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="ec0e8-134">Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych sqlite w folderze projektu hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="ec0e8-135">Wykonaj hello toocreate monity użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="ec0e8-136">Upewnij się, że aplikacja hello działa, naciskając <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="ec0e8-137">Kliknij przycisk **Zaloguj** z paska nawigacji hello u góry hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="ec0e8-139">Wprowadź poświadczenia hello hello użytkownika, który został utworzony podczas synchronizowania bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="ec0e8-141">Kliknij pozycję **Utwórz przykładową ankietę**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-141">Click **Create Sample Polls**.</span></span>

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="ec0e8-143">Kliknij ankietę i zagłosuj.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-143">Click on a poll and vote.</span></span>

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="ec0e8-145">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="ec0e8-145">Create a SQL Database</span></span>
<span data-ttu-id="ec0e8-146">W przypadku bazy danych hello utworzymy bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="ec0e8-147">Można utworzyć bazy danych, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="ec0e8-148">Zaloguj się do hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="ec0e8-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="ec0e8-149">U dołu okienka nawigacji hello hello, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="ec0e8-150">, kliknij przycisk **dane i magazyn** > **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="ec0e8-151">Skonfiguruj hello nowej bazy danych SQL, tworząc nową grupę zasobów i wybierz Witaj dla niej odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="ec0e8-152">Po utworzeniu hello bazy danych SQL, kliknij przycisk **Otwórz w programie Visual Studio** w hello bloku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="ec0e8-153">Kliknij przycisk **skonfigurowanie zapory**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="ec0e8-154">W hello **ustawienia zapory** bloku, Dodaj regułę zapory z **START IP** i **KOŃCOWEMU adresowi IP** ustawić toohello publicznego adresu IP komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="ec0e8-155">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-155">Click **Save**.</span></span>

   <span data-ttu-id="ec0e8-156">Dzięki temu serwer bazy danych toohello połączeń z komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="ec0e8-157">W bloku bazy danych powitania kliknij **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="ec0e8-158">Witaj kopiowania przycisk tooput hello wartości **ADO.NET** hello w Schowku.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="ec0e8-159">Skonfiguruj hello projektu</span><span class="sxs-lookup"><span data-stu-id="ec0e8-159">Configure hello Project</span></span>
<span data-ttu-id="ec0e8-160">W tej sekcji skonfigurujemy naszych sieci web aplikacji toouse hello bazy danych SQL, którą właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="ec0e8-161">Firma Microsoft będzie także zainstalować dodatkowe baz toouse wymagane pakiety języka Python przy użyciu platformy Django.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="ec0e8-162">Następnie hello aplikacji sieci web zostanie uruchomiony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="ec0e8-163">W programie Visual Studio Otwórz **settings.py**, z hello *ProjectName* folderu.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="ec0e8-164">Wklej tymczasowo parametry połączenia hello w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="ec0e8-165">Witaj parametry połączenia mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="ec0e8-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="ec0e8-166">Edytowanie definicji hello `DATABASES` wartości hello toouse powyżej.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="ec0e8-167">W Eksploratorze rozwiązań w obszarze **środowiska Python**, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="ec0e8-168">Zainstaluj pakiet hello `pyodbc` przy użyciu **pip**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="ec0e8-170">Zainstaluj pakiet hello `django-pyodbc-azure` przy użyciu **pip**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="ec0e8-172">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="ec0e8-173">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="ec0e8-174">Spowoduje to utworzenie tabel hello hello bazy danych SQL utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="ec0e8-175">Wykonaj hello toocreate monity użytkownika, który nie ma toomatch hello użytkownika w bazie danych sqlite hello utworzone w pierwszej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="ec0e8-176">Uruchamianie aplikacji hello z `F5`.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-176">Run hello application with `F5`.</span></span> <span data-ttu-id="ec0e8-177">Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w bazie danych SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="ec0e8-178">Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="ec0e8-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="ec0e8-179">Hello zestawu .NET SDK usługi Azure zapewnia łatwy sposób toodeploy Twojej aplikacji usługi sieci Web aplikacji tooAzure aplikacji sieci web w sieci web.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="ec0e8-180">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="ec0e8-182">Kliknij pozycję **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="ec0e8-183">Polecenie **nowy** toocreate nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="ec0e8-184">Wypełnij następujące pola hello i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="ec0e8-185">**Nazwa aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="ec0e8-185">**Web App name**</span></span>
   * <span data-ttu-id="ec0e8-186">**Plan usługi App Service**</span><span class="sxs-lookup"><span data-stu-id="ec0e8-186">**App Service plan**</span></span>
   * <span data-ttu-id="ec0e8-187">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="ec0e8-187">**Resource group**</span></span>
   * <span data-ttu-id="ec0e8-188">**Region**</span><span class="sxs-lookup"><span data-stu-id="ec0e8-188">**Region**</span></span>
   * <span data-ttu-id="ec0e8-189">Pozostaw **serwera bazy danych** ustawić także**bazy danych**</span><span class="sxs-lookup"><span data-stu-id="ec0e8-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="ec0e8-190">Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="ec0e8-191">Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="ec0e8-192">Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **SQL** bazy danych hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="ec0e8-193">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ec0e8-193">Congratulations!</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="ec0e8-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec0e8-195">Next steps</span></span>
<span data-ttu-id="ec0e8-196">Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Django i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="ec0e8-197">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="ec0e8-198">[Projekty sieci Web]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-198">[Web Projects]</span></span>
  * <span data-ttu-id="ec0e8-199">[Projekty usługi w chmurze]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="ec0e8-200">[Debugowanie zdalne na platformie Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="ec0e8-201">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-201">[Django Documentation]</span></span>
* <span data-ttu-id="ec0e8-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="ec0e8-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ec0e8-203">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="ec0e8-203">What's changed</span></span>
* <span data-ttu-id="ec0e8-204">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Dokumentacja platformy Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
