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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Tworzenie aplikacji sieci web PHP-SQL i wdrażanie tooAzure App Service przy użyciu narzędzia Git
Ten samouczek pokazuje, jak toocreate PHP sieci web aplikacji w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) łączące tooAzure bazy danych SQL i w jaki sposób toodeploy go przy użyciu narzędzia Git. Ten samouczek zakłada masz [PHP][install-php], [programu SQL Server Express][install-SQLExpress], hello [Drivers firmy Microsoft dla programu SQL Server dla PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), i [Git] [ install-git] zainstalowany na tym komputerze. Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP SQL działających na platformie Azure.

> [!NOTE]
> Można zainstalować i skonfigurować PHP, programu SQL Server Express i hello Drivers firmy Microsoft dla programu SQL Server dla programów PHP i przy użyciu hello [Instalatora platformy sieci Web firmy Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Dowiesz się:

* Jak toocreate Azure sieci web, aplikacji i bazy danych SQL przy użyciu hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Ponieważ PHP jest domyślnie włączona w aplikacji usługi sieci Web aplikacji, specjalne nie oznacza to wymagana toorun kodzie PHP.
* Jak toopublish i opublikuj go ponownie z tooAzure aplikacji przy użyciu narzędzia Git.

W ramach tego samouczka, utworzysz prosty rejestracji aplikacji sieci web w języku PHP. Aplikacja Hello będzie obsługiwana w witrynie sieci Web platformy Azure. Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Witryna sieci Web Azure PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git
Wykonaj te kroki toocreate aplikacji sieci web platformy Azure i bazy danych SQL:

1. Zaloguj się za toohello [Azure Portal](https://portal.azure.com/).
2. Otwórz hello Azure Marketplace, klikając hello **nowy** ikony na górze hello pozostałych hello pulpitu nawigacyjnego, kliknij pozycję **Zaznacz wszystko** dalej tooMarketplace i wybierając **sieci Web i mobilność**.
3. Hello Marketplace, wybierz **sieci Web i mobilność**.
4. Kliknij przycisk hello **aplikacja sieci Web i SQL** ikony.
5. Po przeczytaniu opisu hello hello aplikacja sieci Web i aplikacji SQL, wybierz **Utwórz**.
6. Kliknij na każdej części (**grupy zasobów**, **aplikacji sieci Web**, **bazy danych**, i **subskrypcji**) i wprowadź lub wybierz wartości hello wymagane pola:
   
   * Wprowadź nazwę adresu URL wybranych przez użytkownika    
   * Skonfiguruj poświadczenia serwera bazy danych
   * Witaj wybierz region najbliższy tooyou
     
     ![Konfigurowanie aplikacji](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Po zakończeniu definiowania hello aplikacji sieci web, kliknij przycisk **Utwórz**.
   
    Podczas tworzenia aplikacji sieci web hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i hello zarówno hello sieci web i aplikacji hello bazy danych SQL w grupie hello tooshow Otwórz bloku grupy zasobów.
8. Kliknij ikonę aplikacji sieci web hello w bloku hello zasobów grupy bloku tooopen hello aplikacji sieci web.
   
    ![Grupa zasobów aplikacji w sieci Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. W **ustawienia** kliknij **ciągłe wdrażanie** > **Skonfiguruj wymagane ustawienia**. Wybierz **lokalnego repozytorium Git** i kliknij przycisk **OK**.
   
    ![gdzie znajduje się kod źródłowy](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Jeśli nie zdefiniowano repozytorium Git przed, należy podać nazwę użytkownika i hasło. toodo tego, kliknij **ustawienia** > **poświadczenia wdrażania** w bloku aplikacja sieci web hello.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. W **ustawienia** kliknij **właściwości** toosee hello Git zdalnego adresu URL należy toouse toodeploy aplikację PHP później.

## <a name="get-sql-database-connection-information"></a>Pobierz informacje dotyczące połączenia bazy danych SQL
wystąpienie bazy danych SQL toohello tooconnect, który jest połączony tooyour aplikacji sieci web, użytkownika będzie konieczne hello informacje dotyczące połączenia, określony podczas tworzenia hello bazy danych. Witaj tooget informacje dotyczące połączenia bazy danych SQL, wykonaj następujące kroki:

1. W bloku grupy zasobów powitania kliknij ikonę hello SQL database.
2. W bloku hello SQL database, kliknij **ustawienia** > **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**. 
   
    ![Wyświetl właściwości bazy danych](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Z hello **PHP** sekcji hello wynikowy okna dialogowego, zanotuj wartości hello `Server`, `SQL Database`, i `User Name`. Użyj tych wartości później podczas publikowania tooAzure aplikacji programu PHP sieci web usługi aplikacji.

## <a name="build-and-test-your-application-locally"></a>Kompilowanie i testowanie aplikacji lokalnie
Rejestracja aplikacji Hello jest prostą aplikację PHP, która pozwala tooregister zdarzenia, podając adres nazwę i adres e-mail. Informacje o poprzednim dokonującymi są wyświetlane w tabeli. Informacje rejestracyjne są przechowywane w wystąpieniu bazy danych SQL. Aplikacja Hello składa się z dwóch plików (skopiuj i Wklej kod dostępne poniżej):

* **index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.
* **createtable.php**: tworzy hello tabeli bazy danych SQL dla aplikacji hello. Ten plik zostanie użyte tylko raz.

toorun hello aplikację lokalnie, wykonaj poniższe kroki hello. Należy pamiętać, że w tych krokach przyjęto założenie, masz PHP i SQL Server Express konfigurowanie na komputerze lokalnym i że włączono hello [PDO rozszerzenia dla programu SQL Server][pdo-sqlsrv].

1. Utwórz bazę danych programu SQL Server o nazwie `registration`. Można to zrobić z hello `sqlcmd` wiersza polecenia przy użyciu następujących poleceń:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. W katalogu głównym aplikacji, należy utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.
3. Otwórz hello `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod hello. Ten kod będzie używany toocreate hello `registration_tbl` tabeli w hello `registration` bazy danych.
   
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
   
    Należy pamiętać, że konieczne będzie tooupdate hello wartości <code>$user</code> i <code>$pwd</code> z lokalnym nazwa użytkownika serwera SQL i hasło.
4. W terminalu w katalogu głównym hello hello typu aplikacji hello następujące polecenie:
   
        php -S localhost:8000
5. Otwórz przeglądarkę sieci web i przeglądanie za**http://localhost:8000/createtable.php**. Spowoduje to utworzenie hello `registration_tbl` tabeli w bazie danych hello.
6. Otwórz hello **index.php** plik w edytorze tekstów lub IDE i Dodaj hello podstawowy kod HTML i CSS dla strony hello (hello kodu PHP zostaną dodane w kolejnych krokach).
   
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
7. W tagach PHP hello należy dodać kodu PHP podłączania toohello bazy danych.
   
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
   
    Ponownie, konieczne będzie wartości hello tooupdate <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
8. Następujący kod połączenia bazy danych hello Dodaj kod do wstawiania informacji o rejestracji do hello bazy danych.
   
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
9. Na koniec po powyższym kodzie hello, należy dodać kodu do pobierania danych z bazy danych hello.
   
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

Użytkownik może przeglądać zbyt**http://localhost:8000/index.php** tootest hello aplikacji.

## <a name="publish-your-application"></a>Publikowanie aplikacji
Po przetestowaniu aplikacji lokalnie, można publikować aplikacje sieci Web usługi tooApp przy użyciu narzędzia Git. Jednak należy najpierw tooupdate hello bazy danych informacje o połączeniu w aplikacji hello. Przy użyciu połączenia bazy danych hello uzyskanymi wcześniej (w hello **informacje o połączeniu pobrać bazy danych SQL** sekcji), aktualizacja hello następujących informacji w **zarówno** hello `createdatabase.php` i `index.php` pliki z hello odpowiednie wartości:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> W hello <code>$host</code>, wartość powitania serwera musi poprzedzać z <code>tcp:</code>.
> 
> 

Teraz są gotowe tooset się publikowanie w usłudze Git i publikowanie aplikacji hello.

> [!NOTE]
> Są to te same czynności wymienionych na końcu hello hello hello **tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git** powyższej sekcji.
> 
> 

1. Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), zmień katalog główny toohello katalogów aplikacji (hello **rejestracji** katalogu), i hello uruchom następujące polecenia:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Pojawi się monit o hasło hello, utworzony wcześniej.
2. Przeglądaj zbyt**name].azurewebsites.net/createtable.php aplikacji http://[web** tabeli bazy danych SQL hello toocreate dla aplikacji hello.
3. Przeglądaj zbyt**name].azurewebsites.net/index.php aplikacji http://[web** toobegin przy użyciu aplikacji hello.

Po opublikowaniu aplikacji, możesz rozpocząć tworzenie tooit zmian i użyć Git toopublish je. 

## <a name="publish-changes-tooyour-application"></a>Publikowanie aplikacji tooyour zmiany
toopublish zmiany tooapplication, wykonaj następujące kroki:

1. Zmiany tooyour aplikacji lokalnie.
2. Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), a następnie zmień katalogi toohello katalogu aplikacji i uruchom następujące polecenia hello:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Pojawi się monit o hasło hello, utworzony wcześniej.
3. Przeglądaj zbyt**name].azurewebsites.net/index.php aplikacji http://[web** toosee zmiany.

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

