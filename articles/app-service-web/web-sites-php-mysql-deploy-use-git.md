---
title: "aaaCreate MySQL PHP sieci web aplikacji w usłudze Azure App Service i wdrażanie przy użyciu narzędzia Git"
description: "Samouczek, który demonstruje sposób toocreate PHP sieci web aplikacji, która przechowuje dane w MySQL i użyj tooAzure wdrożenia Git."
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="0ed3f-103">Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą usługi Git</span><span class="sxs-lookup"><span data-stu-id="0ed3f-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="0ed3f-104">Ten samouczek pokazuje, jak aplikacji sieci web toocreate PHP-MySQL i jak toodeploy on zbyt[usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="0ed3f-105">Użyjesz [PHP][install-php], hello MySQL narzędzia wiersza polecenia (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="0ed3f-106">Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="0ed3f-107">Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="0ed3f-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-108">You will learn:</span></span>

* <span data-ttu-id="0ed3f-109">Jak toocreate aplikacji sieci web i bazy danych MySQL bazy danych przy użyciu hello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="0ed3f-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="0ed3f-110">Ponieważ PHP jest włączona w [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) domyślnie segmentami jest wymagana toorun kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="0ed3f-111">Jak toopublish i opublikuj go ponownie z tooAzure aplikacji przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="0ed3f-112">Jak tooenable hello Composer rozszerzenia tooautomate Composer zadań w każdym `git push`.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="0ed3f-113">W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="0ed3f-114">Aplikacja Hello będzie obsługiwana w aplikacjach sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="0ed3f-115">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-115">A screenshot of hello completed application is below:</span></span>

![Witryny sieci web w usłudze Azure PHP][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="0ed3f-117">Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="0ed3f-117">Set up hello development environment</span></span>
<span data-ttu-id="0ed3f-118">Ten samouczek zakłada masz [PHP][install-php], hello MySQL narzędzia wiersza polecenia (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="0ed3f-119">Tworzenie aplikacji sieci web i skonfigurować publikowanie w usłudze Git</span><span class="sxs-lookup"><span data-stu-id="0ed3f-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="0ed3f-120">Wykonaj te kroki toocreate aplikacji sieci web i bazy danych MySQL:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="0ed3f-121">Toohello logowania [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="0ed3f-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="0ed3f-122">Kliknij przycisk hello **nowy** ikony.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="0ed3f-123">Kliknij przycisk **Zobacz wszystkie** dalej zbyt**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="0ed3f-124">Kliknij przycisk **sieci Web i mobilność**, następnie **aplikacja sieci Web i MySQL**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="0ed3f-125">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="0ed3f-126">Wprowadź prawidłową nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-126">Enter a valid name for your resource group.</span></span>
   
    ![Nazwa grupy zasobów zestawu][resource-group]
6. <span data-ttu-id="0ed3f-128">Wprowadź wartości dla nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-128">Enter values for your new web app.</span></span>
   
    ![Tworzenie aplikacji sieci Web][new-web-app]
7. <span data-ttu-id="0ed3f-130">Wprowadź wartości dla nowej bazy danych, w tym uzgodnienia toohello postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
8. <span data-ttu-id="0ed3f-132">Podczas tworzenia aplikacji sieci web hello zobaczysz hello nowego bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="0ed3f-133">W **ustawienia** kliknij **ciągłe wdrażanie**, następnie kliknij polecenie *Skonfiguruj wymagane ustawienia*.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Konfigurowanie publikowania Git][setup-publishing]
10. <span data-ttu-id="0ed3f-135">Wybierz **lokalnego repozytorium Git** hello źródła.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Konfigurowanie repozytorium Git][setup-repository]
11. <span data-ttu-id="0ed3f-137">tooenable Git publikowania, musisz podać nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="0ed3f-138">Zanotuj hello nazwę użytkownika i hasło, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="0ed3f-139">(Jeśli w repozytorium Git przed, ten krok zostanie pominięty).</span><span class="sxs-lookup"><span data-stu-id="0ed3f-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Tworzenie poświadczeń publikowania][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="0ed3f-141">Pobierz informacje o połączeniu zdalnym MySQL</span><span class="sxs-lookup"><span data-stu-id="0ed3f-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="0ed3f-142">tooconnect toohello baza danych MySQL działającej w aplikacji sieci Web, z będzie konieczne hello informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="0ed3f-143">tooget MySQL informacje dotyczące połączenia, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="0ed3f-144">Z grupy zasobów kliknij przycisk hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-144">From your resource group, click hello database:</span></span>
   
    ![Wybierz bazę danych][select-database]
2. <span data-ttu-id="0ed3f-146">Z bazy danych hello **ustawienia**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Wybieranie właściwości][select-properties]
3. <span data-ttu-id="0ed3f-148">Zanotuj wartości hello `Database`, `Host`, `User Id`, i `Password`.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Uwaga Właściwości][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="0ed3f-150">Tworzenie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="0ed3f-150">Build and test your app locally</span></span>
<span data-ttu-id="0ed3f-151">Teraz, po utworzeniu aplikacji sieci web, możesz utworzyć aplikację lokalnie, a następnie wdrożyć ją po zakończeniu testowania.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="0ed3f-152">Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="0ed3f-153">Informacje o poprzednim dokonującymi są wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="0ed3f-154">Informacje rejestracyjne są przechowywane w bazie danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="0ed3f-155">Aplikacja Hello składa się z jednego pliku (skopiuj i Wklej kod dostępne poniżej):</span><span class="sxs-lookup"><span data-stu-id="0ed3f-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="0ed3f-156">**index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="0ed3f-157">toobuild i hello Uruchom aplikację lokalnie, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="0ed3f-158">Należy pamiętać, że tych krokach przyjęto założenie hello PHP i MySQL narzędzia wiersza polecenia (część MySQL) na komputerze lokalnym i włączono hello [PDO rozszerzenia dla programu MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="0ed3f-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="0ed3f-159">Połącz toohello MySQL serwera zdalnego, za pomocą wartości hello `Data Source`, `User Id`, `Password`, i `Database` , który został wcześniej pobrany:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="0ed3f-160">pojawi się wiersz polecenia MySQL Hello:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="0ed3f-161">Wklej w następujących hello `CREATE TABLE` hello toocreate polecenia `registration_tbl` tabeli w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="0ed3f-162">W głównym folderze lokalnym aplikacji hello utworzyć **index.php** pliku.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="0ed3f-163">Otwórz hello **index.php** plik w edytorze tekstów lub IDE, a następnie dodać hello następującego kodu i oznaczone pełną hello niezbędne zmiany `//TODO:` komentarze.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="0ed3f-164">W terminalu Przejdź tooyour aplikacji folderu i typ hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="0ed3f-165">Użytkownik może przeglądać zbyt**http://localhost: 8000 /** tootest hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="0ed3f-166">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ed3f-166">Publish your app</span></span>
<span data-ttu-id="0ed3f-167">Po przetestowaniu aplikacji lokalnie, można publikować aplikacje tooWeb przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="0ed3f-168">Zostanie zainicjowania lokalnego repozytorium Git i publikowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="0ed3f-169">Te są hello same kroki opisane w hello portalu Azure na końcu hello hello tworzenie aplikacji sieci web i zestaw się Git publikowania powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="0ed3f-170">(Opcjonalnie)  Jeśli zostały zapomniane lub adres URL zdalnego repostitory Git zagubione, przejdź toohello właściwości aplikacji sieci web na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="0ed3f-171">Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), a następnie zmień katalogi toohello katalogu aplikacji i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="0ed3f-172">Pojawi się monit o hasło hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Początkowa tooAzure wypychanych za pomocą narzędzia Git][git-initial-push]
3. <span data-ttu-id="0ed3f-174">Przeglądaj zbyt**http://[site name].azurewebsites.net/index.php** toobegin przy użyciu aplikacji hello (te informacje będą przechowywane na pulpicie nawigacyjnym konta):</span><span class="sxs-lookup"><span data-stu-id="0ed3f-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

<span data-ttu-id="0ed3f-176">Po opublikowaniu aplikacji, możesz rozpocząć tworzenie tooit zmian i użyć Git toopublish je.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="0ed3f-177">Publikowanie aplikacji tooyour zmiany</span><span class="sxs-lookup"><span data-stu-id="0ed3f-177">Publish changes tooyour app</span></span>
<span data-ttu-id="0ed3f-178">toopublish zmiany tooyour aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="0ed3f-179">Wprowadź zmiany tooyour lokalnie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="0ed3f-180">Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), a następnie zmień katalogi toohello katalogu głównego aplikacji i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="0ed3f-181">Pojawi się monit o hasło hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Wypychanie lokacji zmienia się tooAzure za pomocą narzędzia Git][git-change-push]
3. <span data-ttu-id="0ed3f-183">Przeglądaj zbyt**http://[site name].azurewebsites.net/index.php** toosee aplikacji oraz wszelkie zmiany wprowadzone:</span><span class="sxs-lookup"><span data-stu-id="0ed3f-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

> [!NOTE]
> <span data-ttu-id="0ed3f-185">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0ed3f-186">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="0ed3f-187">Automatyzowanie Composer z hello rozszerzenie Composer</span><span class="sxs-lookup"><span data-stu-id="0ed3f-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="0ed3f-188">Domyślnie program hello procesu wdrażania narzędzia git w usłudze App Service nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="0ed3f-189">Można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer hello.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="0ed3f-190">W przypadku programu PHP sieci web bloku aplikacji w hello [portalu Azure][management-portal], kliknij przycisk **narzędzia** > **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Ustawienia rozszerzenie Composer][composer-extension-settings]
2. <span data-ttu-id="0ed3f-192">Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Dodaj rozszerzenie Composer][composer-extension-add]
3. <span data-ttu-id="0ed3f-194">Kliknij przycisk **OK** tooaccept postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="0ed3f-195">Kliknij przycisk **OK** ponownie tooadd hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="0ed3f-196">Witaj **zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer hello.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="0ed3f-197">![Widok rozszerzenie Composer][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="0ed3f-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="0ed3f-198">Teraz, wykonywać `git add`, `git commit`, i `git push` podobnie jak w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="0ed3f-199">Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.</span><span class="sxs-lookup"><span data-stu-id="0ed3f-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Powodzenie rozszerzenie Composer][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="0ed3f-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ed3f-201">Next steps</span></span>
<span data-ttu-id="0ed3f-202">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0ed3f-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
