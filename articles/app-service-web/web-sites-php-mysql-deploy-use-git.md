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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą usługi Git
Ten samouczek pokazuje, jak aplikacji sieci web toocreate PHP-MySQL i jak toodeploy on zbyt[usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) przy użyciu narzędzia Git. Użyjesz [PHP][install-php], hello MySQL narzędzia wiersza polecenia (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze. Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux. Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.

Dowiesz się:

* Jak toocreate aplikacji sieci web i bazy danych MySQL bazy danych przy użyciu hello [Azure Portal][management-portal]. Ponieważ PHP jest włączona w [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) domyślnie segmentami jest wymagana toorun kodzie PHP.
* Jak toopublish i opublikuj go ponownie z tooAzure aplikacji przy użyciu narzędzia Git.
* Jak tooenable hello Composer rozszerzenia tooautomate Composer zadań w każdym `git push`.

W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP. Aplikacja Hello będzie obsługiwana w aplikacjach sieci Web. Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Witryny sieci web w usłudze Azure PHP][running-app]

## <a name="set-up-hello-development-environment"></a>Konfigurowanie środowiska deweloperskiego hello
Ten samouczek zakłada masz [PHP][install-php], hello MySQL narzędzia wiersza polecenia (część [MySQL][install-mysql]), i [Git] [ install-git] zainstalowany na tym komputerze.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Tworzenie aplikacji sieci web i skonfigurować publikowanie w usłudze Git
Wykonaj te kroki toocreate aplikacji sieci web i bazy danych MySQL:

1. Toohello logowania [Azure Portal][management-portal].
2. Kliknij przycisk hello **nowy** ikony.
3. Kliknij przycisk **Zobacz wszystkie** dalej zbyt**Marketplace**. 
4. Kliknij przycisk **sieci Web i mobilność**, następnie **aplikacja sieci Web i MySQL**. Następnie kliknij pozycję **Utwórz**.
5. Wprowadź prawidłową nazwę grupy zasobów.
   
    ![Nazwa grupy zasobów zestawu][resource-group]
6. Wprowadź wartości dla nowej aplikacji sieci web.
   
    ![Tworzenie aplikacji sieci Web][new-web-app]
7. Wprowadź wartości dla nowej bazy danych, w tym uzgodnienia toohello postanowienia prawne.
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
8. Podczas tworzenia aplikacji sieci web hello zobaczysz hello nowego bloku aplikacja sieci web.
9. W **ustawienia** kliknij **ciągłe wdrażanie**, następnie kliknij polecenie *Skonfiguruj wymagane ustawienia*.
   
    ![Konfigurowanie publikowania Git][setup-publishing]
10. Wybierz **lokalnego repozytorium Git** hello źródła.
    
     ![Konfigurowanie repozytorium Git][setup-repository]
11. tooenable Git publikowania, musisz podać nazwę użytkownika i hasło. Zanotuj hello nazwę użytkownika i hasło, które można utworzyć. (Jeśli w repozytorium Git przed, ten krok zostanie pominięty).
    
     ![Tworzenie poświadczeń publikowania][credentials]

## <a name="get-remote-mysql-connection-information"></a>Pobierz informacje o połączeniu zdalnym MySQL
tooconnect toohello baza danych MySQL działającej w aplikacji sieci Web, z będzie konieczne hello informacje o połączeniu. tooget MySQL informacje dotyczące połączenia, wykonaj następujące kroki:

1. Z grupy zasobów kliknij przycisk hello bazy danych:
   
    ![Wybierz bazę danych][select-database]
2. Z bazy danych hello **ustawienia**, wybierz pozycję **właściwości**.
   
    ![Wybieranie właściwości][select-properties]
3. Zanotuj wartości hello `Database`, `Host`, `User Id`, i `Password`.
   
    ![Uwaga Właściwości][note-properties]

## <a name="build-and-test-your-app-locally"></a>Tworzenie i testowanie aplikacji lokalnie
Teraz, po utworzeniu aplikacji sieci web, możesz utworzyć aplikację lokalnie, a następnie wdrożyć ją po zakończeniu testowania.

Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail. Informacje o poprzednim dokonującymi są wyświetlane w tabeli. Informacje rejestracyjne są przechowywane w bazie danych MySQL. Aplikacja Hello składa się z jednego pliku (skopiuj i Wklej kod dostępne poniżej):

* **index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.

toobuild i hello Uruchom aplikację lokalnie, wykonaj poniższe kroki hello. Należy pamiętać, że tych krokach przyjęto założenie hello PHP i MySQL narzędzia wiersza polecenia (część MySQL) na komputerze lokalnym i włączono hello [PDO rozszerzenia dla programu MySQL][pdo-mysql].

1. Połącz toohello MySQL serwera zdalnego, za pomocą wartości hello `Data Source`, `User Id`, `Password`, i `Database` , który został wcześniej pobrany:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. pojawi się wiersz polecenia MySQL Hello:
   
        mysql>
3. Wklej w następujących hello `CREATE TABLE` hello toocreate polecenia `registration_tbl` tabeli w bazie danych:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. W głównym folderze lokalnym aplikacji hello utworzyć **index.php** pliku.
5. Otwórz hello **index.php** plik w edytorze tekstów lub IDE, a następnie dodać hello następującego kodu i oznaczone pełną hello niezbędne zmiany `//TODO:` komentarze.

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

1. W terminalu Przejdź tooyour aplikacji folderu i typ hello następujące polecenie:
   
       php -S localhost:8000

Użytkownik może przeglądać zbyt**http://localhost: 8000 /** tootest hello aplikacji.

## <a name="publish-your-app"></a>Publikowanie aplikacji
Po przetestowaniu aplikacji lokalnie, można publikować aplikacje tooWeb przy użyciu narzędzia Git. Zostanie zainicjowania lokalnego repozytorium Git i publikowanie aplikacji hello.

> [!NOTE]
> Te są hello same kroki opisane w hello portalu Azure na końcu hello hello tworzenie aplikacji sieci web i zestaw się Git publikowania powyższej sekcji.
> 
> 

1. (Opcjonalnie)  Jeśli zostały zapomniane lub adres URL zdalnego repostitory Git zagubione, przejdź toohello właściwości aplikacji sieci web na powitania portalu Azure.
2. Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), a następnie zmień katalogi toohello katalogu aplikacji i uruchom następujące polecenia hello:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Pojawi się monit o hasło hello, utworzony wcześniej.
   
    ![Początkowa tooAzure wypychanych za pomocą narzędzia Git][git-initial-push]
3. Przeglądaj zbyt**http://[site name].azurewebsites.net/index.php** toobegin przy użyciu aplikacji hello (te informacje będą przechowywane na pulpicie nawigacyjnym konta):
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

Po opublikowaniu aplikacji, możesz rozpocząć tworzenie tooit zmian i użyć Git toopublish je.

## <a name="publish-changes-tooyour-app"></a>Publikowanie aplikacji tooyour zmiany
toopublish zmiany tooyour aplikacji, wykonaj następujące kroki:

1. Wprowadź zmiany tooyour lokalnie aplikacji.
2. Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), a następnie zmień katalogi toohello katalogu głównego aplikacji i uruchom następujące polecenia hello:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Pojawi się monit o hasło hello, utworzony wcześniej.
   
    ![Wypychanie lokacji zmienia się tooAzure za pomocą narzędzia Git][git-change-push]
3. Przeglądaj zbyt**http://[site name].azurewebsites.net/index.php** toosee aplikacji oraz wszelkie zmiany wprowadzone:
   
    ![Witryny sieci web w usłudze Azure PHP][running-app]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Automatyzowanie Composer z hello rozszerzenie Composer
Domyślnie program hello procesu wdrażania narzędzia git w usłudze App Service nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP. Można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer hello.

1. W przypadku programu PHP sieci web bloku aplikacji w hello [portalu Azure][management-portal], kliknij przycisk **narzędzia** > **rozszerzenia**.
   
    ![Ustawienia rozszerzenie Composer][composer-extension-settings]
2. Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.
   
    ![Dodaj rozszerzenie Composer][composer-extension-add]
3. Kliknij przycisk **OK** tooaccept postanowienia prawne. Kliknij przycisk **OK** ponownie tooadd hello rozszerzenia.
   
    Witaj **zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer hello.  
    ![Widok rozszerzenie Composer][composer-extension-view]
4. Teraz, wykonywać `git add`, `git commit`, i `git push` podobnie jak w poprzedniej sekcji hello. Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.
   
    ![Powodzenie rozszerzenie Composer][composer-extension-success]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

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
