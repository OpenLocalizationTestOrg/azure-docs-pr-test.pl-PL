---
title: "Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą usługi Git"
description: "Samouczek, który demonstruje sposób tworzenia aplikacji sieci web PHP, która przechowuje dane w MySQL i używania wdrożenia usługi Git do platformy Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="be1e4-103">Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą usługi Git</span><span class="sxs-lookup"><span data-stu-id="be1e4-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="be1e4-104">W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web PHP MySQL i jak wdrożyć ją [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="be1e4-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="be1e4-105">Użyjesz [PHP][install-php], narzędzie wiersza polecenia MySQL (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="be1e4-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="be1e4-106">Instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="be1e4-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="be1e4-107">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="be1e4-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="be1e4-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="be1e4-108">You will learn:</span></span>

* <span data-ttu-id="be1e4-109">Jak utworzyć aplikację sieci web i bazy danych MySQL przy użyciu [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="be1e4-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="be1e4-110">Ponieważ PHP jest włączona w [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) domyślnie segmentami jest wymagana do uruchamiania kodu PHP.</span><span class="sxs-lookup"><span data-stu-id="be1e4-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="be1e4-111">Jak opublikować i ponownie opublikować aplikację na platformie Azure przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="be1e4-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="be1e4-112">Jak włączyć rozszerzenie Composer można zautomatyzować Composer zadań w każdym `git push`.</span><span class="sxs-lookup"><span data-stu-id="be1e4-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="be1e4-113">W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="be1e4-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="be1e4-114">Aplikacja będzie hostowana w aplikacjach sieci Web.</span><span class="sxs-lookup"><span data-stu-id="be1e4-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="be1e4-115">Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="be1e4-115">A screenshot of the completed application is below:</span></span>

![Witryny sieci web w usłudze Azure PHP][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="be1e4-117">Konfigurowanie środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="be1e4-117">Set up the development environment</span></span>
<span data-ttu-id="be1e4-118">Ten samouczek zakłada masz [PHP][install-php], narzędzie wiersza polecenia MySQL (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="be1e4-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="be1e4-119">Tworzenie aplikacji sieci web i skonfigurować publikowanie w usłudze Git</span><span class="sxs-lookup"><span data-stu-id="be1e4-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="be1e4-120">Wykonaj następujące kroki, aby utworzyć aplikację sieci web i bazy danych MySQL:</span><span class="sxs-lookup"><span data-stu-id="be1e4-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="be1e4-121">Zaloguj się do [portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="be1e4-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="be1e4-122">Kliknij przycisk **nowy** ikony.</span><span class="sxs-lookup"><span data-stu-id="be1e4-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="be1e4-123">Kliknij przycisk **Zobacz wszystkie** obok **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="be1e4-124">Kliknij przycisk **sieci Web i mobilność**, następnie **aplikacja sieci Web i MySQL**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="be1e4-125">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="be1e4-126">Wprowadź prawidłową nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1e4-126">Enter a valid name for your resource group.</span></span>
   
    ![Nazwa grupy zasobów zestawu][resource-group]
6. <span data-ttu-id="be1e4-128">Wprowadź wartości dla nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="be1e4-128">Enter values for your new web app.</span></span>
   
    ![Tworzenie aplikacji sieci Web][new-web-app]
7. <span data-ttu-id="be1e4-130">Wprowadź wartości dla nowej bazy danych, w tym wyrażenie zgody na postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="be1e4-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
8. <span data-ttu-id="be1e4-132">Po utworzeniu aplikacji sieci web, pojawi się nowy blok aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="be1e4-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="be1e4-133">W **ustawienia** kliknij **ciągłe wdrażanie**, następnie kliknij polecenie *Skonfiguruj wymagane ustawienia*.</span><span class="sxs-lookup"><span data-stu-id="be1e4-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Konfigurowanie publikowania Git][setup-publishing]
10. <span data-ttu-id="be1e4-135">Wybierz **lokalnego repozytorium Git** źródła.</span><span class="sxs-lookup"><span data-stu-id="be1e4-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Konfigurowanie repozytorium Git][setup-repository]
11. <span data-ttu-id="be1e4-137">Aby włączyć publikowanie w usłudze Git, podaj nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="be1e4-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="be1e4-138">Zanotuj nazwę użytkownika i hasło, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="be1e4-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="be1e4-139">(Jeśli w repozytorium Git przed, ten krok zostanie pominięty).</span><span class="sxs-lookup"><span data-stu-id="be1e4-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Tworzenie poświadczeń publikowania][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="be1e4-141">Pobierz informacje o połączeniu zdalnym MySQL</span><span class="sxs-lookup"><span data-stu-id="be1e4-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="be1e4-142">Do połączenia z bazą danych MySQL, działającej w aplikacji sieci Web, sieci będą potrzebne informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="be1e4-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="be1e4-143">Aby uzyskać informacje o połączeniu MySQL, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="be1e4-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="be1e4-144">Z grupy zasobów kliknij bazę danych:</span><span class="sxs-lookup"><span data-stu-id="be1e4-144">From your resource group, click the database:</span></span>
   
    ![Wybierz bazę danych][select-database]
2. <span data-ttu-id="be1e4-146">Z bazy danych **ustawienia**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Wybieranie właściwości][select-properties]
3. <span data-ttu-id="be1e4-148">Zanotuj wartości `Database`, `Host`, `User Id`, i `Password`.</span><span class="sxs-lookup"><span data-stu-id="be1e4-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Uwaga Właściwości][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="be1e4-150">Tworzenie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="be1e4-150">Build and test your app locally</span></span>
<span data-ttu-id="be1e4-151">Teraz, po utworzeniu aplikacji sieci web, możesz utworzyć aplikację lokalnie, a następnie wdrożyć ją po zakończeniu testowania.</span><span class="sxs-lookup"><span data-stu-id="be1e4-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="be1e4-152">Aplikacja rejestracji jest prostą aplikację PHP, która służy do rejestrowania zdarzenia podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="be1e4-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="be1e4-153">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="be1e4-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="be1e4-154">Informacje rejestracyjne są przechowywane w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="be1e4-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="be1e4-155">Aplikacja składa się z jednego pliku (skopiuj i Wklej kod dostępne poniżej):</span><span class="sxs-lookup"><span data-stu-id="be1e4-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="be1e4-156">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="be1e4-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="be1e4-157">Aby skompilować i uruchomić aplikację lokalnie, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="be1e4-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="be1e4-158">Należy pamiętać, że tych krokach przyjęto założenie, PHP i MySQL narzędzia wiersza polecenia (część MySQL) na komputerze lokalnym, a włączono [PDO rozszerzenia dla programu MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="be1e4-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="be1e4-159">Połącz z serwerem zdalnym MySQL, przy użyciu wartości dla `Data Source`, `User Id`, `Password`, i `Database` , który został wcześniej pobrany:</span><span class="sxs-lookup"><span data-stu-id="be1e4-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="be1e4-160">Pojawi się wiersz polecenia MySQL:</span><span class="sxs-lookup"><span data-stu-id="be1e4-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="be1e4-161">Wklej poniżej `CREATE TABLE` polecenie, aby utworzyć `registration_tbl` tabeli w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="be1e4-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="be1e4-162">W folderze głównym folderu lokalnego aplikacji Utwórz **index.php** pliku.</span><span class="sxs-lookup"><span data-stu-id="be1e4-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="be1e4-163">Otwórz **index.php** plik w edytorze tekstów lub IDE i Dodaj następujący kod, a następnie ukończ niezbędne zmiany oznaczonych `//TODO:` komentarze.</span><span class="sxs-lookup"><span data-stu-id="be1e4-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="be1e4-164">W terminalu przejdź do folderu aplikacji i wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="be1e4-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="be1e4-165">Możesz teraz przejść do **http://localhost: 8000 /** do testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be1e4-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="be1e4-166">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="be1e4-166">Publish your app</span></span>
<span data-ttu-id="be1e4-167">Po przetestowaniu aplikacji lokalnie, można opublikować aplikacje sieci Web przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="be1e4-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="be1e4-168">Zostanie zainicjowania lokalnego repozytorium Git i Opublikuj aplikację.</span><span class="sxs-lookup"><span data-stu-id="be1e4-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="be1e4-169">Są to te same kroki wyświetlana w portalu Azure na końcu się Git publikowania powyższej sekcji Tworzenie aplikacji sieci web i zestawu.</span><span class="sxs-lookup"><span data-stu-id="be1e4-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="be1e4-170">(Opcjonalnie)  Jeśli zostały zapomniane lub adres URL zdalnego repostitory Git zagubione, przejdź do właściwości aplikacji sieci web w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="be1e4-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="be1e4-171">Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), przejdź do katalogu głównego aplikacji i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="be1e4-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="be1e4-172">Pojawi się monit o podanie hasła utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="be1e4-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Początkowa wypychanych na platformie Azure za pomocą narzędzia Git][git-initial-push]
3. <span data-ttu-id="be1e4-174">Przejdź do **http://[site name].azurewebsites.net/index.php** aby rozpocząć korzystanie z aplikacji (te informacje będą przechowywane na pulpicie nawigacyjnym konta):</span><span class="sxs-lookup"><span data-stu-id="be1e4-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

<span data-ttu-id="be1e4-176">Po opublikowaniu aplikacji, można rozpocząć wprowadzania zmian i publikowanie ich przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="be1e4-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="be1e4-177">Publikowanie zmian w aplikacji</span><span class="sxs-lookup"><span data-stu-id="be1e4-177">Publish changes to your app</span></span>
<span data-ttu-id="be1e4-178">Aby opublikować zmian w aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="be1e4-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="be1e4-179">Wprowadzanie zmian do aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="be1e4-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="be1e4-180">Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), przejdź do katalogu głównego aplikacji i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="be1e4-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="be1e4-181">Pojawi się monit o podanie hasła utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="be1e4-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Wypychanie zmiany witryny na platformie Azure za pomocą narzędzia Git][git-change-push]
3. <span data-ttu-id="be1e4-183">Przejdź do **http://[site name].azurewebsites.net/index.php** do aplikacji i wszelkie zmiany wprowadzone w temacie:</span><span class="sxs-lookup"><span data-stu-id="be1e4-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

> [!NOTE]
> <span data-ttu-id="be1e4-185">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="be1e4-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="be1e4-186">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="be1e4-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="be1e4-187">Automatyzowanie Composer rozszerzenie Composer</span><span class="sxs-lookup"><span data-stu-id="be1e4-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="be1e4-188">Domyślnie proces wdrażania narzędzia git w usłudze App Service nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP.</span><span class="sxs-lookup"><span data-stu-id="be1e4-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="be1e4-189">Można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer.</span><span class="sxs-lookup"><span data-stu-id="be1e4-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="be1e4-190">W przypadku programu PHP sieci web bloku aplikacji w [portalu Azure][management-portal], kliknij przycisk **narzędzia** > **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Ustawienia rozszerzenie Composer][composer-extension-settings]
2. <span data-ttu-id="be1e4-192">Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.</span><span class="sxs-lookup"><span data-stu-id="be1e4-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Dodaj rozszerzenie Composer][composer-extension-add]
3. <span data-ttu-id="be1e4-194">Kliknij przycisk **OK** zaakceptować postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="be1e4-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="be1e4-195">Kliknij przycisk **OK** ponownie, aby dodać rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="be1e4-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="be1e4-196">**Zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer.</span><span class="sxs-lookup"><span data-stu-id="be1e4-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="be1e4-197">![Widok rozszerzenie Composer][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="be1e4-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="be1e4-198">Teraz, wykonywać `git add`, `git commit`, i `git push` , takich jak w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="be1e4-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="be1e4-199">Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.</span><span class="sxs-lookup"><span data-stu-id="be1e4-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Powodzenie rozszerzenie Composer][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="be1e4-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be1e4-201">Next steps</span></span>
<span data-ttu-id="be1e4-202">Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="be1e4-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
