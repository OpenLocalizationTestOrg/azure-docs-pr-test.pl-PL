---
title: "aaaCreate PHP SQL sieci web aplikacji i wdrażania tooAzure App Service przy użyciu narzędzia Git"
description: "Samouczek, który demonstruje sposób toocreate PHP sieci web aplikacji, która przechowuje dane w bazie danych SQL Azure i użyć tooAzure wdrożenia Git usługi aplikacji."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="d873d-103">Tworzenie aplikacji sieci web PHP-SQL i wdrażanie tooAzure App Service przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="d873d-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="d873d-104">Ten samouczek pokazuje, jak toocreate PHP sieci web aplikacji w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) łączące tooAzure bazy danych SQL i w jaki sposób toodeploy go przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="d873d-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="d873d-105">Ten samouczek zakłada masz [PHP][install-php], [programu SQL Server Express][install-SQLExpress], hello [Drivers firmy Microsoft dla programu SQL Server dla PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d873d-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="d873d-106">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP SQL działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d873d-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d873d-107">Można zainstalować i skonfigurować PHP, programu SQL Server Express i hello Drivers firmy Microsoft dla programu SQL Server dla programów PHP i przy użyciu hello [Instalatora platformy sieci Web firmy Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d873d-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="d873d-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="d873d-108">You will learn:</span></span>

* <span data-ttu-id="d873d-109">Jak toocreate Azure sieci web, aplikacji i bazy danych SQL przy użyciu hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="d873d-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d873d-110">Ponieważ PHP jest domyślnie włączona w aplikacji usługi sieci Web aplikacji, specjalne nie oznacza to wymagana toorun kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="d873d-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="d873d-111">Jak toopublish i opublikuj go ponownie z tooAzure aplikacji przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="d873d-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="d873d-112">W ramach tego samouczka, utworzysz prosty rejestracji aplikacji sieci web w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="d873d-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="d873d-113">Aplikacja Hello będzie obsługiwana w witrynie sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d873d-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="d873d-114">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="d873d-114">A screenshot of hello completed application is below:</span></span>

![Witryna sieci Web Azure PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d873d-116">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="d873d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d873d-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="d873d-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="d873d-118">Tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git</span><span class="sxs-lookup"><span data-stu-id="d873d-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="d873d-119">Wykonaj te kroki toocreate aplikacji sieci web platformy Azure i bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="d873d-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="d873d-120">Zaloguj się za toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d873d-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d873d-121">Otwórz hello Azure Marketplace, klikając hello **nowy** ikony na górze hello pozostałych hello pulpitu nawigacyjnego, kliknij pozycję **Zaznacz wszystko** dalej tooMarketplace i wybierając **sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="d873d-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="d873d-122">Hello Marketplace, wybierz **sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="d873d-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="d873d-123">Kliknij przycisk hello **aplikacja sieci Web i SQL** ikony.</span><span class="sxs-lookup"><span data-stu-id="d873d-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="d873d-124">Po przeczytaniu opisu hello hello aplikacja sieci Web i aplikacji SQL, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d873d-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="d873d-125">Kliknij na każdej części (**grupy zasobów**, **aplikacji sieci Web**, **bazy danych**, i **subskrypcji**) i wprowadź lub wybierz wartości hello wymagane pola:</span><span class="sxs-lookup"><span data-stu-id="d873d-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="d873d-126">Wprowadź nazwę adresu URL wybranych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="d873d-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="d873d-127">Skonfiguruj poświadczenia serwera bazy danych</span><span class="sxs-lookup"><span data-stu-id="d873d-127">Configure database server credentials</span></span>
   * <span data-ttu-id="d873d-128">Witaj wybierz region najbliższy tooyou</span><span class="sxs-lookup"><span data-stu-id="d873d-128">Select hello region closest tooyou</span></span>
     
     ![Konfigurowanie aplikacji](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="d873d-130">Po zakończeniu definiowania hello aplikacji sieci web, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d873d-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="d873d-131">Podczas tworzenia aplikacji sieci web hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i hello zarówno hello sieci web i aplikacji hello bazy danych SQL w grupie hello tooshow Otwórz bloku grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d873d-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="d873d-132">Kliknij ikonę aplikacji sieci web hello w bloku hello zasobów grupy bloku tooopen hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d873d-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Grupa zasobów aplikacji w sieci Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="d873d-134">W **ustawienia** kliknij **ciągłe wdrażanie** > **Skonfiguruj wymagane ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="d873d-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="d873d-135">Wybierz **lokalnego repozytorium Git** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d873d-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![gdzie znajduje się kod źródłowy](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="d873d-137">Jeśli nie zdefiniowano repozytorium Git przed, należy podać nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d873d-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="d873d-138">toodo tego, kliknij **ustawienia** > **poświadczenia wdrażania** w bloku aplikacja sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="d873d-139">W **ustawienia** kliknij **właściwości** toosee hello Git zdalnego adresu URL należy toouse toodeploy aplikację PHP później.</span><span class="sxs-lookup"><span data-stu-id="d873d-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="d873d-140">Pobierz informacje dotyczące połączenia bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="d873d-140">Get SQL Database connection information</span></span>
<span data-ttu-id="d873d-141">wystąpienie bazy danych SQL toohello tooconnect, który jest połączony tooyour aplikacji sieci web, użytkownika będzie konieczne hello informacje dotyczące połączenia, określony podczas tworzenia hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d873d-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="d873d-142">Witaj tooget informacje dotyczące połączenia bazy danych SQL, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d873d-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="d873d-143">W bloku grupy zasobów powitania kliknij ikonę hello SQL database.</span><span class="sxs-lookup"><span data-stu-id="d873d-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="d873d-144">W bloku hello SQL database, kliknij **ustawienia** > **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="d873d-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Wyświetl właściwości bazy danych](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="d873d-146">Z hello **PHP** sekcji hello wynikowy okna dialogowego, zanotuj wartości hello `Server`, `SQL Database`, i `User Name`.</span><span class="sxs-lookup"><span data-stu-id="d873d-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="d873d-147">Użyj tych wartości później podczas publikowania tooAzure aplikacji programu PHP sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d873d-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="d873d-148">Kompilowanie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="d873d-148">Build and test your application locally</span></span>
<span data-ttu-id="d873d-149">Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="d873d-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="d873d-150">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d873d-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="d873d-151">Informacje rejestracyjne są przechowywane w wystąpieniu bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d873d-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="d873d-152">Aplikacja Hello składa się z dwóch plików (skopiuj i Wklej kod dostępne poniżej):</span><span class="sxs-lookup"><span data-stu-id="d873d-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="d873d-153">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="d873d-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="d873d-154">**createtable.php**: tworzy hello tabeli bazy danych SQL dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="d873d-155">Ten plik zostanie użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="d873d-155">This file will only be used once.</span></span>

<span data-ttu-id="d873d-156">toorun hello aplikację lokalnie, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="d873d-157">Należy pamiętać, że w tych krokach przyjęto założenie, masz PHP i SQL Server Express konfigurowanie na komputerze lokalnym i że włączono hello [PDO rozszerzenia dla programu SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="d873d-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="d873d-158">Utwórz bazę danych programu SQL Server o nazwie `registration`.</span><span class="sxs-lookup"><span data-stu-id="d873d-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="d873d-159">Można to zrobić z hello `sqlcmd` wiersza polecenia przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="d873d-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="d873d-160">W katalogu głównym aplikacji, należy utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.</span><span class="sxs-lookup"><span data-stu-id="d873d-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="d873d-161">Otwórz hello `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="d873d-162">Ten kod będzie używany toocreate hello `registration_tbl` tabeli w hello `registration` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d873d-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="d873d-163">Należy pamiętać, że konieczne będzie tooupdate hello wartości <code>$user</code> i <code>$pwd</code> z lokalnym nazwa użytkownika serwera SQL i hasło.</span><span class="sxs-lookup"><span data-stu-id="d873d-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="d873d-164">W terminalu w katalogu głównym hello hello typu aplikacji hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d873d-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="d873d-165">Otwórz przeglądarkę sieci web i przeglądanie za**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="d873d-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="d873d-166">Spowoduje to utworzenie hello `registration_tbl` tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="d873d-167">Otwórz hello **index.php** plik w edytorze tekstów lub IDE i Dodaj hello podstawowy kod HTML i CSS dla strony hello (hello kodu PHP zostaną dodane w kolejnych krokach).</span><span class="sxs-lookup"><span data-stu-id="d873d-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="d873d-168">W tagach PHP hello należy dodać kodu PHP podłączania toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d873d-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="d873d-169">Ponownie, konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d873d-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="d873d-170">Następujący kod połączenia bazy danych hello Dodaj kod do wstawiania informacji o rejestracji do hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d873d-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="d873d-171">Na koniec po powyższym kodzie hello, należy dodać kodu do pobierania danych z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="d873d-172">Użytkownik może przeglądać zbyt**http://localhost:8000/index.php** tootest hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d873d-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="d873d-173">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d873d-173">Publish your application</span></span>
<span data-ttu-id="d873d-174">Po przetestowaniu aplikacji lokalnie, można publikować aplikacje sieci Web usługi tooApp przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="d873d-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="d873d-175">Jednak należy najpierw tooupdate hello bazy danych informacje o połączeniu w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="d873d-176">Przy użyciu połączenia bazy danych hello uzyskanymi wcześniej (w hello **informacje o połączeniu pobrać bazy danych SQL** sekcji), aktualizacja hello następujących informacji w **zarówno** hello `createdatabase.php` i `index.php` pliki z hello odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="d873d-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="d873d-177">W hello <code>$host</code>, wartość powitania serwera musi poprzedzać z <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="d873d-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="d873d-178">Teraz są gotowe tooset się publikowanie w usłudze Git i publikowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="d873d-179">Są to te same czynności wymienionych na końcu hello hello hello **tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git** powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d873d-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="d873d-180">Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), zmień katalog główny toohello katalogów aplikacji (hello **rejestracji** katalogu), i hello uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d873d-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="d873d-181">Pojawi się monit o hasło hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d873d-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="d873d-182">Przeglądaj zbyt**name].azurewebsites.net/createtable.php aplikacji http://[web** tabeli bazy danych SQL hello toocreate dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="d873d-183">Przeglądaj zbyt**name].azurewebsites.net/index.php aplikacji http://[web** toobegin przy użyciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d873d-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="d873d-184">Po opublikowaniu aplikacji, możesz rozpocząć tworzenie tooit zmian i użyć Git toopublish je.</span><span class="sxs-lookup"><span data-stu-id="d873d-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="d873d-185">Publikowanie aplikacji tooyour zmiany</span><span class="sxs-lookup"><span data-stu-id="d873d-185">Publish changes tooyour application</span></span>
<span data-ttu-id="d873d-186">toopublish zmiany tooapplication, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d873d-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="d873d-187">Zmiany tooyour aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d873d-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="d873d-188">Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), a następnie zmień katalogi toohello katalogu aplikacji i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d873d-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="d873d-189">Pojawi się monit o hasło hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d873d-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="d873d-190">Przeglądaj zbyt**name].azurewebsites.net/index.php aplikacji http://[web** toosee zmiany.</span><span class="sxs-lookup"><span data-stu-id="d873d-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d873d-191">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="d873d-191">What's changed</span></span>
* <span data-ttu-id="d873d-192">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d873d-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

