---
title: "Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą protokołu FTP"
description: "Samouczek, który demonstruje sposób tworzenia aplikacji sieci web PHP, która przechowuje dane w MySQL i użycia serwera FTP wdrożenia na platformie Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="f0031-103">Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="f0031-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="f0031-104">Ten samouczek pokazuje, jak utworzyć aplikację sieci web PHP MySQL i wdrażanie za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="f0031-105">Ten samouczek zakłada masz [PHP][install-php], [MySQL][install-mysql], serwer sieci web, a klient FTP zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f0031-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="f0031-106">Instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="f0031-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f0031-107">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f0031-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f0031-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f0031-108">You will learn:</span></span>

* <span data-ttu-id="f0031-109">Jak utworzyć aplikację sieci web i bazy danych MySQL przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f0031-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="f0031-110">Ponieważ PHP jest domyślnie włączona w aplikacji sieci Web, niezbędny jest segmentami do uruchomienia kodu PHP.</span><span class="sxs-lookup"><span data-stu-id="f0031-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="f0031-111">Jak opublikować aplikację na platformie Azure przy użyciu protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="f0031-112">W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="f0031-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f0031-113">Aplikacja będzie hostowana w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f0031-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="f0031-114">Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="f0031-114">A screenshot of the completed application is below:</span></span>

![Witryna sieci Web Azure PHP][running-app]

> [!NOTE]
> <span data-ttu-id="f0031-116">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="f0031-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f0031-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="f0031-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="f0031-118">Tworzenie aplikacji sieci web i Konfigurowanie publikowania FTP</span><span class="sxs-lookup"><span data-stu-id="f0031-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="f0031-119">Wykonaj następujące kroki, aby utworzyć aplikację sieci web i bazy danych MySQL:</span><span class="sxs-lookup"><span data-stu-id="f0031-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f0031-120">Zaloguj się do [portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="f0031-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f0031-121">Kliknij przycisk **+ nowy** ikona u góry po lewej portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f0031-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Utwórz nową witrynę sieci Web Azure][new-website]
3. <span data-ttu-id="f0031-123">W polu wyszukiwania wpisz **aplikacja sieci Web i MySQL** i wybierz polecenie **aplikacja sieci Web i MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f0031-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Utwórz niestandardowe witryny sieci Web][custom-create]
4. <span data-ttu-id="f0031-125">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f0031-125">Click **Create**.</span></span> <span data-ttu-id="f0031-126">Wprowadź nazwę usługi aplikacji unikatowy, poprawną nazwę grupy zasobów i nowy plan usługi.</span><span class="sxs-lookup"><span data-stu-id="f0031-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Nazwa grupy zasobów zestawu][resource-group]
5. <span data-ttu-id="f0031-128">Wprowadź wartości dla nowej bazy danych, w tym wyrażenie zgody na postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="f0031-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
6. <span data-ttu-id="f0031-130">Po utworzeniu aplikacji sieci web, pojawi się nowy blok usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0031-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="f0031-131">Polecenie **ustawienia** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="f0031-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Konfigurowanie poświadczeń wdrożenia][set-deployment-credentials]
8. <span data-ttu-id="f0031-133">Aby włączyć publikacji FTP, podaj nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f0031-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f0031-134">Zapisz poświadczenia i zanotuj nazwę użytkownika i hasło, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="f0031-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Tworzenie poświadczeń publikowania][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f0031-136">Tworzenie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="f0031-136">Build and test your app locally</span></span>
<span data-ttu-id="f0031-137">Aplikacja rejestracji jest prostą aplikację PHP, która służy do rejestrowania zdarzenia podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="f0031-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="f0031-138">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="f0031-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f0031-139">Informacje rejestracyjne są przechowywane w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0031-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f0031-140">Aplikacja zawiera dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="f0031-140">The app consists of two files:</span></span>

* <span data-ttu-id="f0031-141">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="f0031-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="f0031-142">**createtable.php**: tworzy tabelę MySQL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0031-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="f0031-143">Ten plik zostanie użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="f0031-143">This file will only be used once.</span></span>

<span data-ttu-id="f0031-144">Aby skompilować i uruchomić aplikację lokalnie, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="f0031-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="f0031-145">Należy pamiętać, że tych krokach przyjęto założenie, PHP, MySQL i serwera sieci web na komputerze lokalnym, a włączono [PDO rozszerzenia dla programu MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="f0031-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f0031-146">Utwórz bazę danych MySQL o nazwie `registration`.</span><span class="sxs-lookup"><span data-stu-id="f0031-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="f0031-147">Można to zrobić, w wierszu polecenia MySQL za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f0031-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="f0031-148">W katalogu głównym serwera sieci web, Utwórz folder o nazwie `registration` i utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.</span><span class="sxs-lookup"><span data-stu-id="f0031-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="f0031-149">Otwórz `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="f0031-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="f0031-150">Ten kod będzie używane do tworzenia `registration_tbl` w tabeli `registration` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0031-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="f0031-151">Musisz zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f0031-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="f0031-152">Otwórz przeglądarkę sieci web i przejdź do [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="f0031-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="f0031-153">Spowoduje to utworzenie `registration_tbl` tabeli w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f0031-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="f0031-154">Otwórz **index.php** plik w edytorze tekstów lub IDE i dodać podstawowe kodu HTML i CSS strony (kodu PHP zostaną dodane w kolejnych krokach).</span><span class="sxs-lookup"><span data-stu-id="f0031-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="f0031-155">W tagach PHP należy dodać kodu PHP do łączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="f0031-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="f0031-156">Ponownie, należy zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f0031-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="f0031-157">Następujący kod połączenia bazy danych Dodaj kod dla wstawiania informacje rejestracyjne w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f0031-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="f0031-158">Na koniec po powyższym kodzie należy dodać kodu do pobierania danych z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0031-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="f0031-159">Możesz teraz przejść do [http://localhost/registration/index.php] [ localhost-index] do testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0031-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="f0031-160">Pobierz informacje o połączeniu FTP i MySQL</span><span class="sxs-lookup"><span data-stu-id="f0031-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="f0031-161">Do połączenia z bazą danych MySQL, działającej w aplikacji sieci Web, sieci będą potrzebne informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="f0031-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="f0031-162">Aby uzyskać informacje o połączeniu MySQL, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f0031-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f0031-163">Z usługi aplikacji bloku aplikacja sieci web, kliknij łącze grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="f0031-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Wybierz grupę zasobów][select-resourcegroup]
2. <span data-ttu-id="f0031-165">Z grupy zasobów kliknij bazę danych:</span><span class="sxs-lookup"><span data-stu-id="f0031-165">From your resource group, click the database:</span></span>
   
    ![Wybierz bazę danych][select-database]
3. <span data-ttu-id="f0031-167">Z bazy danych podsumowania, wybierz **ustawienia** > **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f0031-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Wybieranie właściwości][select-properties]
4. <span data-ttu-id="f0031-169">Zanotuj wartości `Database`, `Host`, `User Id`, i `Password`.</span><span class="sxs-lookup"><span data-stu-id="f0031-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Uwaga Właściwości][note-properties]
5. <span data-ttu-id="f0031-171">Z aplikacji sieci web, kliknij przycisk **pobieranie profilu publikowania** łącze w prawym dolnym rogu strony:</span><span class="sxs-lookup"><span data-stu-id="f0031-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Pobieranie profilu publikowania][download-publish-profile]
6. <span data-ttu-id="f0031-173">Otwórz `.publishsettings` plik w edytorze XML.</span><span class="sxs-lookup"><span data-stu-id="f0031-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="f0031-174">Znajdź `<publishProfile >` element z `publishMethod="FTP"` podobny do poniższego:</span><span class="sxs-lookup"><span data-stu-id="f0031-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="f0031-175">Zwróć uwagę na `publishUrl`, `userName`, i `userPWD` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="f0031-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f0031-176">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0031-176">Publish your app</span></span>
<span data-ttu-id="f0031-177">Po przetestowaniu aplikacji lokalnie, można opublikować aplikację sieci web za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="f0031-178">Jednak najpierw musisz zaktualizować informacje o połączeniu bazy danych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0031-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="f0031-179">Korzystając z bazy danych informacji połączenia uzyskanymi wcześniej (w **informacje o połączeniu FTP i pobrać MySQL** sekcji), zaktualizuj następujące informacje w **zarówno** `createdatabase.php` i `index.php` plików z odpowiednimi wartościami:</span><span class="sxs-lookup"><span data-stu-id="f0031-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="f0031-180">Teraz można przystąpić do publikowania aplikacji za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="f0031-181">Otwórz klienta FTP wyboru.</span><span class="sxs-lookup"><span data-stu-id="f0031-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="f0031-182">Wprowadź *częścią nazwy hosta* z `publishUrl` atrybutu opisanymi powyżej do klienta FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="f0031-183">Wprowadź `userName` i `userPWD` atrybuty wymienione powyżej bez zmian do klienta FTP.</span><span class="sxs-lookup"><span data-stu-id="f0031-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="f0031-184">Nawiąż połączenie.</span><span class="sxs-lookup"><span data-stu-id="f0031-184">Establish a connection.</span></span>

<span data-ttu-id="f0031-185">Po nawiązaniu połączenia można przekazywanie i pobieranie plików zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f0031-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="f0031-186">Pamiętaj, że przekazujesz pliki do katalogu głównego, który jest `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="f0031-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="f0031-187">Po przekazaniu zarówno `index.php` i `createtable.php`, przejdź do **http://[site name].azurewebsites.net/createtable.php** do utworzenia tabeli MySQL dla aplikacji, a następnie wyszukaj **http://[site name]. azurewebsites.NET/index.php** aby rozpocząć korzystanie z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0031-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0031-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0031-188">Next steps</span></span>
<span data-ttu-id="f0031-189">Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f0031-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

