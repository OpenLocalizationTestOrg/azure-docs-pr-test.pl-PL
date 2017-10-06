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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą protokołu FTP
Ten samouczek pokazuje, jak aplikacji sieci web toocreate PHP-MySQL i jak toodeploy za pomocą protokołu FTP. Ten samouczek zakłada masz [PHP][install-php], [MySQL][install-mysql], serwer sieci web, a klient FTP zainstalowany na tym komputerze. Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux. Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.

Dowiesz się:

* Jak toocreate aplikacji sieci web i bazy danych MySQL bazy danych przy użyciu hello portalu Azure. Ponieważ PHP jest domyślnie włączona w aplikacji sieci Web, specjalne nie oznacza to wymagana toorun kodzie PHP.
* Jak toopublish swoją aplikację tooAzure przy użyciu usługi FTP.

W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP. Aplikacja Hello będzie obsługiwana w aplikacji sieci Web. Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Witryna sieci Web Azure PHP][running-app]

> [!NOTE]
> Jeśli chcesz korzystać z usługi Azure App Service przed utworzeniem konta tooget Przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Tworzenie aplikacji sieci web i Konfigurowanie publikowania FTP
Wykonaj te kroki toocreate aplikacji sieci web i bazy danych MySQL:

1. Toohello logowania [Azure Portal][management-portal].
2. Kliknij przycisk hello **+ nowy** ikony na górze hello rogu hello portalu Azure.
   
    ![Utwórz nową witrynę sieci Web Azure][new-website]
3. W polu wyszukiwania wpisz tekst hello **aplikacja sieci Web i MySQL** i wybierz polecenie **aplikacja sieci Web i MySQL**.
   
    ![Utwórz niestandardowe witryny sieci Web][custom-create]
4. Kliknij przycisk **Utwórz**. Wprowadź nazwę usługi aplikacji unikatowy, poprawną nazwę grupy zasobów hello i nowy plan usługi.
   
    ![Nazwa grupy zasobów zestawu][resource-group]
5. Wprowadź wartości dla nowej bazy danych, w tym uzgodnienia toohello postanowienia prawne.
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
6. Podczas tworzenia aplikacji sieci web hello pojawi się nowy blok usługi aplikacji hello.
7. Polecenie **ustawienia** > **poświadczenia wdrażania**. 
   
    ![Konfigurowanie poświadczeń wdrożenia][set-deployment-credentials]
8. tooenable publikacji FTP, należy podać nazwę użytkownika i hasło. Zapisz poświadczenia hello i zanotuj hello nazwę użytkownika i hasło, które można utworzyć.
   
    ![Tworzenie poświadczeń publikowania][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Tworzenie i testowanie aplikacji lokalnie
Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail. Informacje o poprzednim dokonującymi są wyświetlane w tabeli. Informacje rejestracyjne są przechowywane w bazie danych MySQL. Aplikacja Hello składa się z dwóch plików:

* **index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.
* **createtable.php**: tworzy tablicę MySQL hello aplikacji hello. Ten plik zostanie użyte tylko raz.

toobuild i hello Uruchom aplikację lokalnie, wykonaj poniższe kroki hello. Należy pamiętać, że w tych krokach przyjęto założenie, PHP, MySQL i serwera sieci web na komputerze lokalnym i że włączono hello [PDO rozszerzenia dla programu MySQL][pdo-mysql].

1. Utwórz bazę danych MySQL o nazwie `registration`. Można to zrobić z wiersza polecenia MySQL hello za pomocą tego polecenia:
   
        mysql> create database registration;
2. W katalogu głównym serwera sieci web, Utwórz folder o nazwie `registration` i utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.
3. Otwórz hello `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod hello. Ten kod będzie używany toocreate hello `registration_tbl` tabeli w hello `registration` bazy danych.
   
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
   > Konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
   > 
   > 
4. Otwórz przeglądarkę sieci web i przeglądanie za[http://localhost/registration/createtable.php][localhost-createtable]. Spowoduje to utworzenie hello `registration_tbl` tabeli w bazie danych hello.
5. Otwórz hello **index.php** plik w edytorze tekstów lub IDE i Dodaj hello podstawowy kod HTML i CSS dla strony hello (hello kodu PHP zostaną dodane w kolejnych krokach).
   
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
6. W tagach PHP hello należy dodać kodu PHP podłączania toohello bazy danych.
   
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
   > Ponownie, konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
   > 
   > 
7. Następujący kod połączenia bazy danych hello Dodaj kod do wstawiania informacji o rejestracji do hello bazy danych.
   
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
8. Na koniec po powyższym kodzie hello, należy dodać kodu do pobierania danych z bazy danych hello.
   
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

Użytkownik może przeglądać zbyt[http://localhost/registration/index.php] [ localhost-index] tootest hello aplikacji.

## <a name="get-mysql-and-ftp-connection-information"></a>Pobierz informacje o połączeniu FTP i MySQL
tooconnect toohello baza danych MySQL działającej w aplikacji sieci Web, z będzie konieczne hello informacje o połączeniu. tooget MySQL informacje dotyczące połączenia, wykonaj następujące kroki:

1. Z usługi aplikacji hello bloku aplikacja sieci web kliknij łącze grupę zasobów hello:
   
    ![Wybierz grupę zasobów][select-resourcegroup]
2. Z grupy zasobów kliknij przycisk hello bazy danych:
   
    ![Wybierz bazę danych][select-database]
3. Z bazy danych hello podsumowania, wybierz **ustawienia** > **właściwości**.
   
    ![Wybieranie właściwości][select-properties]
4. Zanotuj wartości hello `Database`, `Host`, `User Id`, i `Password`.
   
    ![Uwaga Właściwości][note-properties]
5. Z aplikacji sieci web, kliknij przycisk hello **pobieranie profilu publikowania** łącze na powitania prawym dolnym rogu strony hello:
   
    ![Pobieranie profilu publikowania][download-publish-profile]
6. Otwórz hello `.publishsettings` plik w edytorze XML. 
7. Znajdź hello `<publishProfile >` element z `publishMethod="FTP"` wygląda podobnie toothis:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Zwróć uwagę na powitania `publishUrl`, `userName`, i `userPWD` atrybutów.

## <a name="publish-your-app"></a>Publikowanie aplikacji
Po przetestowaniu aplikacji lokalnie, można opublikować tooyour aplikacji sieci web za pomocą protokołu FTP. Jednak należy najpierw tooupdate hello bazy danych informacje o połączeniu w aplikacji hello. Przy użyciu połączenia bazy danych hello uzyskanymi wcześniej (w hello **informacje o połączeniu FTP i pobrać MySQL** sekcji), aktualizacja hello następujących informacji w **zarówno** hello `createdatabase.php` i `index.php` pliki z hello odpowiednie wartości:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Teraz możesz przygotować toopublish aplikację za pomocą protokołu FTP.

1. Otwórz klienta FTP wyboru.
2. Wprowadź hello *częścią nazwy hosta* z hello `publishUrl` atrybutu opisanymi powyżej do klienta FTP.
3. Wprowadź hello `userName` i `userPWD` atrybuty wymienione powyżej bez zmian do klienta FTP.
4. Nawiąż połączenie.

Po nawiązaniu połączenia będzie tooupload może być i pobierania plików. Pamiętaj, że przekazujesz toohello katalog główny plików, który jest `/site/wwwroot`.

Po przekazaniu zarówno `index.php` i `createtable.php`, Przeglądaj zbyt**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL tabeli dla aplikacji hello, a następnie przejdź zbyt**nazwę http://[site ].azurewebsites.net/index.php** toobegin przy użyciu aplikacji hello.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

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

