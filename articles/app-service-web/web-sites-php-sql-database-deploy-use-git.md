---
title: "Tworzenie aplikacji sieci web PHP-SQL i wdrożyć w usłudze Azure App Service przy użyciu narzędzia Git"
description: "Samouczek, który demonstruje sposób tworzenia aplikacji sieci web PHP, która przechowuje dane w bazie danych SQL Azure i przy użyciu wdrażania Git w usłudze Azure App Service."
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
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="1ccec-103">Tworzenie aplikacji sieci web PHP-SQL i wdrożyć w usłudze Azure App Service przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="1ccec-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="1ccec-104">Ten samouczek pokazuje, jak utworzyć aplikację sieci web PHP w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) które nawiązuje połączenie z bazą danych SQL Azure i sposobu wdrażania przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="1ccec-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="1ccec-105">Ten samouczek zakłada masz [PHP][install-php], [programu SQL Server Express][install-SQLExpress], [Drivers firmy Microsoft dla programu SQL Server dla PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1ccec-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="1ccec-106">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP SQL działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1ccec-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1ccec-107">Można zainstalować i skonfigurować PHP, programu SQL Server Express i Drivers firmy Microsoft dla programu SQL Server dla PHP za pomocą [Instalatora platformy sieci Web firmy Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ccec-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="1ccec-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="1ccec-108">You will learn:</span></span>

* <span data-ttu-id="1ccec-109">Jak utworzyć aplikację sieci web platformy Azure i bazy danych SQL za pomocą [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="1ccec-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="1ccec-110">Ponieważ PHP jest domyślnie włączona w aplikacji usługi sieci Web aplikacji, niezbędny jest segmentami do uruchomienia kodu PHP.</span><span class="sxs-lookup"><span data-stu-id="1ccec-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="1ccec-111">Jak opublikować i ponownie opublikować aplikację na platformie Azure przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="1ccec-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="1ccec-112">W ramach tego samouczka, utworzysz prosty rejestracji aplikacji sieci web w języku PHP.</span><span class="sxs-lookup"><span data-stu-id="1ccec-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="1ccec-113">Aplikacja będzie obsługiwana w witrynie sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1ccec-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="1ccec-114">Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="1ccec-114">A screenshot of the completed application is below:</span></span>

![Witryna sieci Web Azure PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="1ccec-116">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="1ccec-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1ccec-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="1ccec-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="1ccec-118">Tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git</span><span class="sxs-lookup"><span data-stu-id="1ccec-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="1ccec-119">Wykonaj następujące kroki, aby utworzyć aplikację sieci web platformy Azure i bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="1ccec-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="1ccec-120">Zaloguj się do [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ccec-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ccec-121">Otwórz w portalu Azure Marketplace, klikając przycisk **nowy** ikona u góry po lewej pulpitu nawigacyjnego, kliknij pozycję **Zaznacz wszystko** obok Marketplace i wybierając **sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="1ccec-122">W witrynie Marketplace, wybierz **sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="1ccec-123">Kliknij przycisk **aplikacja sieci Web i SQL** ikony.</span><span class="sxs-lookup"><span data-stu-id="1ccec-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="1ccec-124">Po przeczytaniu opisu aplikacji sieci Web + SQL aplikacji, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="1ccec-125">Kliknij na każdej części (**grupy zasobów**, **aplikacji sieci Web**, **bazy danych**, i **subskrypcji**) i wprowadź lub wybierz wartości dla pól wymaganych :</span><span class="sxs-lookup"><span data-stu-id="1ccec-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="1ccec-126">Wprowadź nazwę adresu URL wybranych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ccec-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="1ccec-127">Skonfiguruj poświadczenia serwera bazy danych</span><span class="sxs-lookup"><span data-stu-id="1ccec-127">Configure database server credentials</span></span>
   * <span data-ttu-id="1ccec-128">Wybierz region najbliższego</span><span class="sxs-lookup"><span data-stu-id="1ccec-128">Select the region closest to you</span></span>
     
     ![Konfigurowanie aplikacji](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="1ccec-130">Po zakończeniu definiowania aplikacji sieci web, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="1ccec-131">Po utworzeniu aplikacji sieci web, **powiadomienia** przycisk będzie flash zielona **Powodzenie** i otwórz bloku grupy zasobów, aby wyświetlić zarówno aplikacji sieci web i bazy danych SQL w grupie.</span><span class="sxs-lookup"><span data-stu-id="1ccec-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="1ccec-132">Kliknij ikonę aplikacji sieci web w bloku grupy zasobów, aby otworzyć blok aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1ccec-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![Grupa zasobów aplikacji w sieci Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="1ccec-134">W **ustawienia** kliknij **ciągłe wdrażanie** > **Skonfiguruj wymagane ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="1ccec-135">Wybierz **lokalnego repozytorium Git** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![gdzie znajduje się kod źródłowy](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="1ccec-137">Jeśli nie zdefiniowano repozytorium Git przed, należy podać nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="1ccec-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="1ccec-138">Aby to zrobić, kliknij przycisk **ustawienia** > **poświadczenia wdrażania** w bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="1ccec-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="1ccec-139">W **ustawienia** kliknij **właściwości** wyświetlić zdalnego adresu URL usługi Git należy użyć do wdrożenia aplikacji PHP później.</span><span class="sxs-lookup"><span data-stu-id="1ccec-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="1ccec-140">Pobierz informacje dotyczące połączenia bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="1ccec-140">Get SQL Database connection information</span></span>
<span data-ttu-id="1ccec-141">Do nawiązania połączenia połączonej z aplikacji sieci web użytkownika spowoduje wystąpienie bazy danych SQL wymagane informacje dotyczące połączenia, która została określona podczas tworzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="1ccec-142">Aby uzyskać informacje dotyczące połączenia bazy danych SQL, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1ccec-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="1ccec-143">W bloku grupy zasobów kliknij ikonę bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1ccec-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="1ccec-144">W bloku bazy danych SQL, kliknij przycisk **ustawienia** > **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Wyświetl właściwości bazy danych](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="1ccec-146">Z **PHP** sekcji wynikowy okna dialogowego, zanotuj wartości `Server`, `SQL Database`, i `User Name`.</span><span class="sxs-lookup"><span data-stu-id="1ccec-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="1ccec-147">Te wartości będzie używana później podczas publikowania aplikacji sieci web PHP w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1ccec-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="1ccec-148">Kompilowanie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="1ccec-148">Build and test your application locally</span></span>
<span data-ttu-id="1ccec-149">Aplikacja rejestracji jest prostą aplikację PHP, która służy do rejestrowania zdarzenia podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1ccec-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="1ccec-150">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1ccec-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="1ccec-151">Informacje rejestracyjne są przechowywane w wystąpieniu bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1ccec-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="1ccec-152">Aplikacja składa się z dwóch plików (skopiuj i Wklej kod dostępne poniżej):</span><span class="sxs-lookup"><span data-stu-id="1ccec-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="1ccec-153">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="1ccec-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="1ccec-154">**createtable.php**: tworzy w tabeli bazy danych SQL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="1ccec-155">Ten plik zostanie użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="1ccec-155">This file will only be used once.</span></span>

<span data-ttu-id="1ccec-156">Aby uruchomić aplikację lokalnie, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="1ccec-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="1ccec-157">Należy pamiętać, że tych krokach przyjęto założenie, PHP i SQL Server Express na komputerze lokalnym, a włączono [PDO rozszerzenia dla programu SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="1ccec-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="1ccec-158">Utwórz bazę danych programu SQL Server o nazwie `registration`.</span><span class="sxs-lookup"><span data-stu-id="1ccec-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="1ccec-159">Można to zrobić z `sqlcmd` wiersza polecenia przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="1ccec-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="1ccec-160">W katalogu głównym aplikacji, należy utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.</span><span class="sxs-lookup"><span data-stu-id="1ccec-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="1ccec-161">Otwórz `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="1ccec-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="1ccec-162">Ten kod będzie używane do tworzenia `registration_tbl` w tabeli `registration` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   
    <span data-ttu-id="1ccec-163">Należy pamiętać, że będzie konieczne zaktualizowanie wartości <code>$user</code> i <code>$pwd</code> z lokalnym nazwa użytkownika serwera SQL i hasło.</span><span class="sxs-lookup"><span data-stu-id="1ccec-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="1ccec-164">W terminalu w katalogu głównym aplikacji, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1ccec-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="1ccec-165">Otwórz przeglądarkę sieci web i przejdź do **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="1ccec-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="1ccec-166">Spowoduje to utworzenie `registration_tbl` tabeli w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="1ccec-167">Otwórz **index.php** plik w edytorze tekstów lub IDE i dodać podstawowe kodu HTML i CSS strony (kodu PHP zostaną dodane w kolejnych krokach).</span><span class="sxs-lookup"><span data-stu-id="1ccec-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="1ccec-168">W tagach PHP należy dodać kodu PHP do łączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="1ccec-169">Ponownie, należy zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="1ccec-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="1ccec-170">Następujący kod połączenia bazy danych Dodaj kod dla wstawiania informacje rejestracyjne w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
9. <span data-ttu-id="1ccec-171">Na koniec po powyższym kodzie należy dodać kodu do pobierania danych z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1ccec-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="1ccec-172">Możesz teraz przejść do **http://localhost:8000/index.php** do testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="1ccec-173">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1ccec-173">Publish your application</span></span>
<span data-ttu-id="1ccec-174">Po przetestowaniu aplikacji lokalnie, można opublikować aplikacji usługi sieci Web aplikacji przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="1ccec-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="1ccec-175">Jednak najpierw musisz zaktualizować informacje o połączeniu bazy danych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="1ccec-176">Korzystając z bazy danych informacji połączenia uzyskanymi wcześniej (w **informacje o połączeniu pobrać bazy danych SQL** sekcji), zaktualizuj następujące informacje w **zarówno** `createdatabase.php` i `index.php` plików z odpowiednimi wartościami:</span><span class="sxs-lookup"><span data-stu-id="1ccec-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="1ccec-177">W <code>$host</code>, wartość serwera musi być poprzedzony przez <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="1ccec-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="1ccec-178">Teraz można przystąpić do ustawiania publikowania w usłudze Git i Opublikuj aplikację.</span><span class="sxs-lookup"><span data-stu-id="1ccec-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="1ccec-179">Są to te same kroki wymienione na końcu **tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git** powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="1ccec-180">Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), przejdź do katalogu głównego aplikacji ( **rejestracji** katalogu), i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ccec-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="1ccec-181">Pojawi się monit o podanie hasła utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1ccec-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="1ccec-182">Przejdź do **name].azurewebsites.net/createtable.php aplikacji http://[web** można utworzyć tabeli bazy danych SQL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="1ccec-183">Przejdź do **name].azurewebsites.net/index.php aplikacji http://[web** aby rozpocząć korzystanie z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ccec-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="1ccec-184">Po opublikowaniu aplikacji, można rozpocząć wprowadzania zmian i publikowanie ich przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="1ccec-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="1ccec-185">Publikowanie zmian w aplikacji</span><span class="sxs-lookup"><span data-stu-id="1ccec-185">Publish changes to your application</span></span>
<span data-ttu-id="1ccec-186">Aby opublikować zmian w aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1ccec-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="1ccec-187">Wprowadzanie zmian w aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="1ccec-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="1ccec-188">Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), przejdź do katalogu głównego aplikacji i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ccec-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="1ccec-189">Pojawi się monit o podanie hasła utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1ccec-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="1ccec-190">Przejdź do **name].azurewebsites.net/index.php aplikacji http://[web** aby zobaczyć zmiany.</span><span class="sxs-lookup"><span data-stu-id="1ccec-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1ccec-191">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="1ccec-191">What's changed</span></span>
* <span data-ttu-id="1ccec-192">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="1ccec-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

