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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Tworzenie aplikacji sieci Web PHP-MySQL w usłudze Azure App Service i wdrażanie jej za pomocą protokołu FTP
Ten samouczek pokazuje, jak utworzyć aplikację sieci web PHP MySQL i wdrażanie za pomocą protokołu FTP. Ten samouczek zakłada masz [PHP][install-php], [MySQL][install-mysql], serwer sieci web, a klient FTP zainstalowany na tym komputerze. Instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, w tym systemu Windows, Mac i Linux. Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP/MySQL działające na platformie Azure.

Dowiesz się:

* Jak utworzyć aplikację sieci web i bazy danych MySQL przy użyciu portalu Azure. Ponieważ PHP jest domyślnie włączona w aplikacji sieci Web, niezbędny jest segmentami do uruchomienia kodu PHP.
* Jak opublikować aplikację na platformie Azure przy użyciu protokołu FTP.

W ramach tego samouczka, utworzysz aplikację sieci web rejestracji proste w kodzie PHP. Aplikacja będzie hostowana w aplikacji sieci Web. Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:

![Witryna sieci Web Azure PHP][running-app]

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Tworzenie aplikacji sieci web i Konfigurowanie publikowania FTP
Wykonaj następujące kroki, aby utworzyć aplikację sieci web i bazy danych MySQL:

1. Zaloguj się do [portalu Azure][management-portal].
2. Kliknij przycisk **+ nowy** ikona u góry po lewej portalu Azure.
   
    ![Utwórz nową witrynę sieci Web Azure][new-website]
3. W polu wyszukiwania wpisz **aplikacja sieci Web i MySQL** i wybierz polecenie **aplikacja sieci Web i MySQL**.
   
    ![Utwórz niestandardowe witryny sieci Web][custom-create]
4. Kliknij przycisk **Utwórz**. Wprowadź nazwę usługi aplikacji unikatowy, poprawną nazwę grupy zasobów i nowy plan usługi.
   
    ![Nazwa grupy zasobów zestawu][resource-group]
5. Wprowadź wartości dla nowej bazy danych, w tym wyrażenie zgody na postanowienia prawne.
   
    ![Utwórz nową bazę danych MySQL][new-mysql-db]
6. Po utworzeniu aplikacji sieci web, pojawi się nowy blok usługi aplikacji.
7. Polecenie **ustawienia** > **poświadczenia wdrażania**. 
   
    ![Konfigurowanie poświadczeń wdrożenia][set-deployment-credentials]
8. Aby włączyć publikacji FTP, podaj nazwę użytkownika i hasło. Zapisz poświadczenia i zanotuj nazwę użytkownika i hasło, które można utworzyć.
   
    ![Tworzenie poświadczeń publikowania][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Tworzenie i testowanie aplikacji lokalnie
Aplikacja rejestracji jest prostą aplikację PHP, która służy do rejestrowania zdarzenia podając adres nazwę i adres e-mail. Informacje o poprzednim dokonującymi są wyświetlane w tabeli. Informacje rejestracyjne są przechowywane w bazie danych MySQL. Aplikacja zawiera dwa pliki:

* **index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.
* **createtable.php**: tworzy tabelę MySQL dla aplikacji. Ten plik zostanie użyte tylko raz.

Aby skompilować i uruchomić aplikację lokalnie, wykonaj poniższe kroki. Należy pamiętać, że tych krokach przyjęto założenie, PHP, MySQL i serwera sieci web na komputerze lokalnym, a włączono [PDO rozszerzenia dla programu MySQL][pdo-mysql].

1. Utwórz bazę danych MySQL o nazwie `registration`. Można to zrobić, w wierszu polecenia MySQL za pomocą tego polecenia:
   
        mysql> create database registration;
2. W katalogu głównym serwera sieci web, Utwórz folder o nazwie `registration` i utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.
3. Otwórz `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod. Ten kod będzie używane do tworzenia `registration_tbl` w tabeli `registration` bazy danych.
   
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
   > Musisz zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
   > 
   > 
4. Otwórz przeglądarkę sieci web i przejdź do [http://localhost/registration/createtable.php][localhost-createtable]. Spowoduje to utworzenie `registration_tbl` tabeli w bazie danych.
5. Otwórz **index.php** plik w edytorze tekstów lub IDE i dodać podstawowe kodu HTML i CSS strony (kodu PHP zostaną dodane w kolejnych krokach).
   
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
6. W tagach PHP należy dodać kodu PHP do łączenia z bazą danych.
   
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
   > Ponownie, należy zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
   > 
   > 
7. Następujący kod połączenia bazy danych Dodaj kod dla wstawiania informacje rejestracyjne w bazie danych.
   
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
8. Na koniec po powyższym kodzie należy dodać kodu do pobierania danych z bazy danych.
   
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

Możesz teraz przejść do [http://localhost/registration/index.php] [ localhost-index] do testowania aplikacji.

## <a name="get-mysql-and-ftp-connection-information"></a>Pobierz informacje o połączeniu FTP i MySQL
Do połączenia z bazą danych MySQL, działającej w aplikacji sieci Web, sieci będą potrzebne informacje o połączeniu. Aby uzyskać informacje o połączeniu MySQL, wykonaj następujące kroki:

1. Z usługi aplikacji bloku aplikacja sieci web, kliknij łącze grupy zasobów:
   
    ![Wybierz grupę zasobów][select-resourcegroup]
2. Z grupy zasobów kliknij bazę danych:
   
    ![Wybierz bazę danych][select-database]
3. Z bazy danych podsumowania, wybierz **ustawienia** > **właściwości**.
   
    ![Wybieranie właściwości][select-properties]
4. Zanotuj wartości `Database`, `Host`, `User Id`, i `Password`.
   
    ![Uwaga Właściwości][note-properties]
5. Z aplikacji sieci web, kliknij przycisk **pobieranie profilu publikowania** łącze w prawym dolnym rogu strony:
   
    ![Pobieranie profilu publikowania][download-publish-profile]
6. Otwórz `.publishsettings` plik w edytorze XML. 
7. Znajdź `<publishProfile >` element z `publishMethod="FTP"` podobny do poniższego:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Zwróć uwagę na `publishUrl`, `userName`, i `userPWD` atrybutów.

## <a name="publish-your-app"></a>Publikowanie aplikacji
Po przetestowaniu aplikacji lokalnie, można opublikować aplikację sieci web za pomocą protokołu FTP. Jednak najpierw musisz zaktualizować informacje o połączeniu bazy danych w aplikacji. Korzystając z bazy danych informacji połączenia uzyskanymi wcześniej (w **informacje o połączeniu FTP i pobrać MySQL** sekcji), zaktualizuj następujące informacje w **zarówno** `createdatabase.php` i `index.php` plików z odpowiednimi wartościami:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Teraz można przystąpić do publikowania aplikacji za pomocą protokołu FTP.

1. Otwórz klienta FTP wyboru.
2. Wprowadź *częścią nazwy hosta* z `publishUrl` atrybutu opisanymi powyżej do klienta FTP.
3. Wprowadź `userName` i `userPWD` atrybuty wymienione powyżej bez zmian do klienta FTP.
4. Nawiąż połączenie.

Po nawiązaniu połączenia można przekazywanie i pobieranie plików zgodnie z potrzebami. Pamiętaj, że przekazujesz pliki do katalogu głównego, który jest `/site/wwwroot`.

Po przekazaniu zarówno `index.php` i `createtable.php`, przejdź do **http://[site name].azurewebsites.net/createtable.php** do utworzenia tabeli MySQL dla aplikacji, a następnie wyszukaj **http://[site name]. azurewebsites.NET/index.php** aby rozpocząć korzystanie z aplikacji.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).

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

