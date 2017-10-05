---
title: "Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio"
description: "Dowiedz się, jak używać narzędzi Python Tools for Visual Studio do tworzenia aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych SQL i wdróż je do aplikacji sieci Web usługi aplikacji Azure."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="8e83f-103">Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e83f-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="8e83f-104">W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] utworzyć prostą sondy sieci web aplikacji przy użyciu jednego z szablonów próbki PTVS.</span><span class="sxs-lookup"><span data-stu-id="8e83f-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="8e83f-105">W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="8e83f-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="8e83f-106">Firma Microsoft dowiesz się, sposobu korzystania z bazy danych SQL hostowanej na platformie Azure, jak skonfigurować aplikację sieci web do używania bazy danych SQL i jak opublikować aplikację sieci web, aby [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8e83f-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="8e83f-107">Zobacz [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8e83f-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="8e83f-108">Chociaż ten artykuł dotyczy usługi App Service, opisane kroki są podobne do programowania [usług Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="8e83f-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e83f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8e83f-109">Prerequisites</span></span>
* <span data-ttu-id="8e83f-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8e83f-110">Visual Studio 2015</span></span>
* <span data-ttu-id="8e83f-111">[32-bitowe środowisko Python w wersji 2.7]</span><span class="sxs-lookup"><span data-stu-id="8e83f-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="8e83f-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8e83f-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="8e83f-113">[Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8e83f-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="8e83f-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="8e83f-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="8e83f-115">Django 1.9 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="8e83f-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="8e83f-116">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="8e83f-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8e83f-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="8e83f-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="8e83f-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="8e83f-118">Create the Project</span></span>
<span data-ttu-id="8e83f-119">W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="8e83f-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="8e83f-120">Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="8e83f-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="8e83f-121">Utworzymy lokalnej bazy danych przy użyciu systemu sqlite.</span><span class="sxs-lookup"><span data-stu-id="8e83f-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="8e83f-122">Następnie aplikacja sieci web zostanie uruchomiony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="8e83f-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="8e83f-123">W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="8e83f-124">Szablony projektu z [Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio] są dostępne w menu **Python**, **Przykłady**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="8e83f-125">Wybierz pozycję **Polls Django Web Project** (Projekt sieci Web Django z ankietą) i kliknij przycisk OK, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="8e83f-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="8e83f-127">Zostanie wyświetlony monit o zainstalowanie pakietów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="8e83f-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="8e83f-128">Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-128">Select **Install into a virtual environment**.</span></span>

     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="8e83f-130">Wybierz jako podstawowy interpreter **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="8e83f-132">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8e83f-133">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="8e83f-134">Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych SQLite w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="8e83f-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="8e83f-135">Postępuj zgodnie z monitami, aby utworzyć użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e83f-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="8e83f-136">Upewnij się, że aplikacja działa, naciskając <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="8e83f-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="8e83f-137">Kliknij pozycję **Zaloguj** na górnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="8e83f-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="8e83f-139">Wprowadź poświadczenia użytkownika, który został utworzony podczas synchronizowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8e83f-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="8e83f-141">Kliknij pozycję **Utwórz przykładową ankietę**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-141">Click **Create Sample Polls**.</span></span>

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="8e83f-143">Kliknij ankietę i zagłosuj.</span><span class="sxs-lookup"><span data-stu-id="8e83f-143">Click on a poll and vote.</span></span>

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="8e83f-145">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="8e83f-145">Create a SQL Database</span></span>
<span data-ttu-id="8e83f-146">Dla bazy danych utworzymy bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="8e83f-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="8e83f-147">Można utworzyć bazy danych, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="8e83f-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="8e83f-148">Zaloguj się do [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="8e83f-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="8e83f-149">W dolnej części okienka nawigacji kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="8e83f-150">, kliknij przycisk **dane i magazyn** > **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="8e83f-151">Skonfiguruj nową bazę danych SQL, tworząc nową grupę zasobów, a następnie wybierz dla niej odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="8e83f-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="8e83f-152">Po utworzeniu bazy danych SQL, kliknij przycisk **Otwórz w programie Visual Studio** w bloku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8e83f-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="8e83f-153">Kliknij przycisk **skonfigurowanie zapory**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="8e83f-154">W **ustawienia zapory** bloku, Dodaj regułę zapory z **START IP** i **KOŃCOWEMU adresowi IP** ustawiona na komputerze deweloperskim publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="8e83f-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="8e83f-155">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-155">Click **Save**.</span></span>

   <span data-ttu-id="8e83f-156">Pozwoli to połączenia z serwerem bazy danych w komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="8e83f-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="8e83f-157">W bloku bazy danych, kliknij **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="8e83f-158">Użyj przycisku kopiowania, aby umieścić wartość elementu **ADO.NET** w Schowku.</span><span class="sxs-lookup"><span data-stu-id="8e83f-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="8e83f-159">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="8e83f-159">Configure the Project</span></span>
<span data-ttu-id="8e83f-160">W tej sekcji skonfigurujemy swoją aplikację sieci web do używania bazy danych SQL, które właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="8e83f-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="8e83f-161">Firma Microsoft będzie także zainstalować dodatkowe pakiety Python niezbędne do używania bazy danych SQL przy użyciu platformy Django.</span><span class="sxs-lookup"><span data-stu-id="8e83f-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="8e83f-162">Następnie aplikacja sieci web zostanie uruchomiony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="8e83f-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="8e83f-163">W programie Visual Studio otwórz plik **settings.py** z folderu *NazwaProjektu*.</span><span class="sxs-lookup"><span data-stu-id="8e83f-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="8e83f-164">Wklej tymczasowo parametry połączenia w edytorze.</span><span class="sxs-lookup"><span data-stu-id="8e83f-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="8e83f-165">Parametry połączenia mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="8e83f-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="8e83f-166">Edytowanie definicji `DATABASES` powyżej wartości.</span><span class="sxs-lookup"><span data-stu-id="8e83f-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="8e83f-167">W Eksploratorze rozwiązań w obszarze **Środowiska Python** kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz polecenie **Zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="8e83f-168">Zainstaluj pakiet `pyodbc`, korzystając z polecenia **pip**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="8e83f-170">Zainstaluj pakiet `django-pyodbc-azure`, korzystając z polecenia **pip**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="8e83f-172">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8e83f-173">Następnie wybierz pozycję **Django — tworzenie administratora**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="8e83f-174">Spowoduje to utworzenie tabel dla bazy danych SQL, utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e83f-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="8e83f-175">Postępuj zgodnie z monitami, aby utworzyć użytkownika, nie musi odpowiadać nazwie użytkownika w bazie danych sqlite utworzone w pierwszej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e83f-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="8e83f-176">Uruchom aplikację klawiszem `F5`.</span><span class="sxs-lookup"><span data-stu-id="8e83f-176">Run the application with `F5`.</span></span> <span data-ttu-id="8e83f-177">Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** oraz dane przesłane podczas głosowania zostaną zserializowane w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8e83f-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="8e83f-178">Publikowanie aplikacji sieci Web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8e83f-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="8e83f-179">Zestaw .NET SDK usługi Azure zapewnia łatwy sposób wdrażania aplikacji sieci web w sieci web do aplikacji sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8e83f-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="8e83f-180">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="8e83f-182">Kliknij pozycję **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="8e83f-183">Kliknij pozycję **Nowa**, aby utworzyć nową aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8e83f-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="8e83f-184">Wypełnij następujące pola i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="8e83f-185">**Nazwa aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="8e83f-185">**Web App name**</span></span>
   * <span data-ttu-id="8e83f-186">**Plan usługi App Service**</span><span class="sxs-lookup"><span data-stu-id="8e83f-186">**App Service plan**</span></span>
   * <span data-ttu-id="8e83f-187">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="8e83f-187">**Resource group**</span></span>
   * <span data-ttu-id="8e83f-188">**Region**</span><span class="sxs-lookup"><span data-stu-id="8e83f-188">**Region**</span></span>
   * <span data-ttu-id="8e83f-189">W polu **Serwer bazy danych** pozostaw wartość **Brak bazy danych**</span><span class="sxs-lookup"><span data-stu-id="8e83f-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="8e83f-190">Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="8e83f-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="8e83f-191">Opublikowana aplikacja sieci Web zostanie automatycznie otwarta w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="8e83f-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="8e83f-192">Powinna zostać wyświetlona aplikacja sieci web działa zgodnie z oczekiwaniami, za pomocą **SQL** bazy danych hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8e83f-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="8e83f-193">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="8e83f-193">Congratulations!</span></span>

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="8e83f-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e83f-195">Next steps</span></span>
<span data-ttu-id="8e83f-196">Skorzystaj z poniższych linków, aby dowiedzieć się więcej informacji na temat narzędzi Python Tools dla programu Visual Studio, Django i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8e83f-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="8e83f-197">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8e83f-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="8e83f-198">[Projekty sieci Web]</span><span class="sxs-lookup"><span data-stu-id="8e83f-198">[Web Projects]</span></span>
  * <span data-ttu-id="8e83f-199">[Projekty usługi w chmurze]</span><span class="sxs-lookup"><span data-stu-id="8e83f-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="8e83f-200">[Debugowanie zdalne na platformie Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="8e83f-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="8e83f-201">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="8e83f-201">[Django Documentation]</span></span>
* <span data-ttu-id="8e83f-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="8e83f-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8e83f-203">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="8e83f-203">What's changed</span></span>
* <span data-ttu-id="8e83f-204">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="8e83f-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="8e83f-205">[Centrum deweloperów języka Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="8e83f-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="8e83f-206">[usług Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="8e83f-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="8e83f-207">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8e83f-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="8e83f-208">[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="8e83f-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="8e83f-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="8e83f-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="8e83f-210">[Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="8e83f-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="8e83f-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="8e83f-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="8e83f-212">[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="8e83f-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="8e83f-213">[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="8e83f-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="8e83f-214">[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="8e83f-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="8e83f-215">[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="8e83f-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="8e83f-216">[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="8e83f-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="8e83f-217">[Dokumentacja platformy Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="8e83f-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="8e83f-218">[SQL Database]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="8e83f-218">[SQL Database]: /documentation/services/sql-database/</span></span>
