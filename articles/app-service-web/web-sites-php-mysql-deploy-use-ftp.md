---
title: "aaaCreate MySQL PHP sieci web aplikacji w usłudze Azure App Service i wdrażanie za pomocą protokołu FTP"
description: "Samouczek, który demonstruje sposób toocreate PHP sieci web aplikacji, która przechowuje dane w MySQL i użyj tooAzure wdrożenia FTP."
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
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="e6fb2-103">Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="e6fb2-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="e6fb2-104">Ten samouczek pokazuje, jak aplikacji sieci web toocreate PHP-MySQL i jak toodeploy za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="e6fb2-105">Ten samouczek zakłada masz [PHP][install-php], [MySQL][install-mysql], serwer sieci web, a klient FTP zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="e6fb2-106">Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="e6fb2-107">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="e6fb2-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-108">You will learn:</span></span>

* <span data-ttu-id="e6fb2-109">Jak toocreate aplikacji sieci web i bazy danych MySQL bazy danych przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="e6fb2-110">Ponieważ PHP jest domyślnie włączona w aplikacji sieci Web, specjalne nie oznacza to wymagana toorun kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="e6fb2-111">Jak toopublish swoją aplikację tooAzure przy użyciu usługi FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="e6fb2-112">W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="e6fb2-113">Aplikacja Hello będzie obsługiwana w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="e6fb2-114">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-114">A screenshot of hello completed application is below:</span></span>

![Witryna sieci Web Azure PHP][running-app]

> [!NOTE]
> <span data-ttu-id="e6fb2-116">Jeśli chcesz korzystać z usługi Azure App Service przed utworzeniem konta tooget Przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e6fb2-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="e6fb2-118">Tworzenie aplikacji sieci web i Konfigurowanie publikowania FTP</span><span class="sxs-lookup"><span data-stu-id="e6fb2-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="e6fb2-119">Wykonaj te kroki toocreate aplikacji sieci web i bazy danych MySQL:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="e6fb2-120">Toohello logowania [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="e6fb2-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="e6fb2-121">Kliknij przycisk hello **+ nowy** ikony na górze hello rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Utwórz nową witrynę sieci Web Azure][new-website]
3. <span data-ttu-id="e6fb2-123">W polu wyszukiwania wpisz tekst hello **aplikacja sieci Web i MySQL** i wybierz polecenie **aplikacja sieci Web i MySQL**.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Utwórz niestandardowe witryny sieci Web][custom-create]
4. <span data-ttu-id="e6fb2-125">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-125">Click **Create**.</span></span> <span data-ttu-id="e6fb2-126">Wprowadź nazwę usługi aplikacji unikatowy, poprawną nazwę grupy zasobów hello i nowy plan usługi.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Nazwa grupy zasobów zestawu][resource-group]
5. <span data-ttu-id="e6fb2-128">Wprowadź wartości dla nowej bazy danych, w tym uzgodnienia toohello postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
6. <span data-ttu-id="e6fb2-130">Podczas tworzenia aplikacji sieci web hello pojawi się nowy blok usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="e6fb2-131">Polecenie **ustawienia** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Konfigurowanie poświadczeń wdrożenia][set-deployment-credentials]
8. <span data-ttu-id="e6fb2-133">tooenable publikacji FTP, należy podać nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="e6fb2-134">Zapisz poświadczenia hello i zanotuj hello nazwę użytkownika i hasło, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Tworzenie poświadczeń publikowania][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="e6fb2-136">Tworzenie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="e6fb2-136">Build and test your app locally</span></span>
<span data-ttu-id="e6fb2-137">Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="e6fb2-138">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="e6fb2-139">Informacje rejestracyjne są przechowywane w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="e6fb2-140">Aplikacja Hello składa się z dwóch plików:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-140">hello app consists of two files:</span></span>

* <span data-ttu-id="e6fb2-141">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="e6fb2-142">**createtable.php**: tworzy tablicę MySQL hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="e6fb2-143">Ten plik zostanie użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-143">This file will only be used once.</span></span>

<span data-ttu-id="e6fb2-144">toobuild i hello Uruchom aplikację lokalnie, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="e6fb2-145">Należy pamiętać, że w tych krokach przyjęto założenie, PHP, MySQL i serwera sieci web na komputerze lokalnym i że włączono hello [PDO rozszerzenia dla programu MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="e6fb2-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="e6fb2-146">Utwórz bazę danych MySQL o nazwie `registration`.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="e6fb2-147">Można to zrobić z wiersza polecenia MySQL hello za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="e6fb2-148">W katalogu głównym serwera sieci web, Utwórz folder o nazwie `registration` i utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="e6fb2-149">Otwórz hello `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="e6fb2-150">Ten kod będzie używany toocreate hello `registration_tbl` tabeli w hello `registration` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="e6fb2-151">Konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="e6fb2-152">Otwórz przeglądarkę sieci web i przeglądanie za[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="e6fb2-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="e6fb2-153">Spowoduje to utworzenie hello `registration_tbl` tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="e6fb2-154">Otwórz hello **index.php** plik w edytorze tekstów lub IDE i Dodaj hello podstawowy kod HTML i CSS dla strony hello (hello kodu PHP zostaną dodane w kolejnych krokach).</span><span class="sxs-lookup"><span data-stu-id="e6fb2-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="e6fb2-155">W tagach PHP hello należy dodać kodu PHP podłączania toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="e6fb2-156">Ponownie, konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="e6fb2-157">Następujący kod połączenia bazy danych hello Dodaj kod do wstawiania informacji o rejestracji do hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="e6fb2-158">Na koniec po powyższym kodzie hello, należy dodać kodu do pobierania danych z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="e6fb2-159">Użytkownik może przeglądać zbyt[http://localhost/registration/index.php] [ localhost-index] tootest hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="e6fb2-160">Pobierz informacje o połączeniu FTP i MySQL</span><span class="sxs-lookup"><span data-stu-id="e6fb2-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="e6fb2-161">tooconnect toohello baza danych MySQL działającej w aplikacji sieci Web, z będzie konieczne hello informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="e6fb2-162">tooget MySQL informacje dotyczące połączenia, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="e6fb2-163">Z usługi aplikacji hello bloku aplikacja sieci web kliknij łącze grupę zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Wybierz grupę zasobów][select-resourcegroup]
2. <span data-ttu-id="e6fb2-165">Z grupy zasobów kliknij przycisk hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-165">From your resource group, click hello database:</span></span>
   
    ![Wybierz bazę danych][select-database]
3. <span data-ttu-id="e6fb2-167">Z bazy danych hello podsumowania, wybierz **ustawienia** > **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Wybieranie właściwości][select-properties]
4. <span data-ttu-id="e6fb2-169">Zanotuj wartości hello `Database`, `Host`, `User Id`, i `Password`.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Uwaga Właściwości][note-properties]
5. <span data-ttu-id="e6fb2-171">Z aplikacji sieci web, kliknij przycisk hello **pobieranie profilu publikowania** łącze na powitania prawym dolnym rogu strony hello:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Pobieranie profilu publikowania][download-publish-profile]
6. <span data-ttu-id="e6fb2-173">Otwórz hello `.publishsettings` plik w edytorze XML.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="e6fb2-174">Znajdź hello `<publishProfile >` element z `publishMethod="FTP"` wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="e6fb2-175">Zwróć uwagę na powitania `publishUrl`, `userName`, i `userPWD` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="e6fb2-176">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e6fb2-176">Publish your app</span></span>
<span data-ttu-id="e6fb2-177">Po przetestowaniu aplikacji lokalnie, można opublikować tooyour aplikacji sieci web za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="e6fb2-178">Jednak należy najpierw tooupdate hello bazy danych informacje o połączeniu w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="e6fb2-179">Przy użyciu połączenia bazy danych hello uzyskanymi wcześniej (w hello **informacje o połączeniu FTP i pobrać MySQL** sekcji), aktualizacja hello następujących informacji w **zarówno** hello `createdatabase.php` i `index.php` pliki z hello odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="e6fb2-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="e6fb2-180">Teraz możesz przygotować toopublish aplikację za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="e6fb2-181">Otwórz klienta FTP wyboru.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="e6fb2-182">Wprowadź hello *częścią nazwy hosta* z hello `publishUrl` atrybutu opisanymi powyżej do klienta FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="e6fb2-183">Wprowadź hello `userName` i `userPWD` atrybuty wymienione powyżej bez zmian do klienta FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="e6fb2-184">Nawiąż połączenie.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-184">Establish a connection.</span></span>

<span data-ttu-id="e6fb2-185">Po nawiązaniu połączenia będzie tooupload może być i pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="e6fb2-186">Pamiętaj, że przekazujesz toohello katalog główny plików, który jest `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="e6fb2-187">Po przekazaniu zarówno `index.php` i `createtable.php`, Przeglądaj zbyt**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL tabeli dla aplikacji hello, a następnie przejdź zbyt**nazwę http://[site ].azurewebsites.net/index.php** toobegin przy użyciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e6fb2-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6fb2-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6fb2-188">Next steps</span></span>
<span data-ttu-id="e6fb2-189">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e6fb2-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

