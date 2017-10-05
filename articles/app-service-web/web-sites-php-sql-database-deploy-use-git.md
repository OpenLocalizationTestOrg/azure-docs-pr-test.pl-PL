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
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a>Tworzenie aplikacji sieci web PHP-SQL i wdrożyć w usłudze Azure App Service przy użyciu narzędzia Git
Ten samouczek pokazuje, jak utworzyć aplikację sieci web PHP w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) które nawiązuje połączenie z bazą danych SQL Azure i sposobu wdrażania przy użyciu narzędzia Git. Ten samouczek zakłada masz [PHP][install-php], [programu SQL Server Express][install-SQLExpress], [Drivers firmy Microsoft dla programu SQL Server dla PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), i [Git] [ install-git] zainstalowany na tym komputerze. Po ukończeniu tego przewodnika, będziesz mieć aplikację sieci web PHP SQL działających na platformie Azure.

> [!NOTE]
> Można zainstalować i skonfigurować PHP, programu SQL Server Express i Drivers firmy Microsoft dla programu SQL Server dla PHP za pomocą [Instalatora platformy sieci Web firmy Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Dowiesz się:

* Jak utworzyć aplikację sieci web platformy Azure i bazy danych SQL za pomocą [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Ponieważ PHP jest domyślnie włączona w aplikacji usługi sieci Web aplikacji, niezbędny jest segmentami do uruchomienia kodu PHP.
* Jak opublikować i ponownie opublikować aplikację na platformie Azure przy użyciu narzędzia Git.

W ramach tego samouczka, utworzysz prosty rejestracji aplikacji sieci web w języku PHP. Aplikacja będzie obsługiwana w witrynie sieci Web platformy Azure. Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:

![Witryna sieci Web Azure PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git
Wykonaj następujące kroki, aby utworzyć aplikację sieci web platformy Azure i bazy danych SQL:

1. Zaloguj się do [Azure Portal](https://portal.azure.com/).
2. Otwórz w portalu Azure Marketplace, klikając przycisk **nowy** ikona u góry po lewej pulpitu nawigacyjnego, kliknij pozycję **Zaznacz wszystko** obok Marketplace i wybierając **sieci Web i mobilność**.
3. W witrynie Marketplace, wybierz **sieci Web i mobilność**.
4. Kliknij przycisk **aplikacja sieci Web i SQL** ikony.
5. Po przeczytaniu opisu aplikacji sieci Web + SQL aplikacji, wybierz **Utwórz**.
6. Kliknij na każdej części (**grupy zasobów**, **aplikacji sieci Web**, **bazy danych**, i **subskrypcji**) i wprowadź lub wybierz wartości dla pól wymaganych :
   
   * Wprowadź nazwę adresu URL wybranych przez użytkownika    
   * Skonfiguruj poświadczenia serwera bazy danych
   * Wybierz region najbliższego
     
     ![Konfigurowanie aplikacji](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Po zakończeniu definiowania aplikacji sieci web, kliknij przycisk **Utwórz**.
   
    Po utworzeniu aplikacji sieci web, **powiadomienia** przycisk będzie flash zielona **Powodzenie** i otwórz bloku grupy zasobów, aby wyświetlić zarówno aplikacji sieci web i bazy danych SQL w grupie.
8. Kliknij ikonę aplikacji sieci web w bloku grupy zasobów, aby otworzyć blok aplikacji sieci web.
   
    ![Grupa zasobów aplikacji w sieci Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. W **ustawienia** kliknij **ciągłe wdrażanie** > **Skonfiguruj wymagane ustawienia**. Wybierz **lokalnego repozytorium Git** i kliknij przycisk **OK**.
   
    ![gdzie znajduje się kod źródłowy](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Jeśli nie zdefiniowano repozytorium Git przed, należy podać nazwę użytkownika i hasło. Aby to zrobić, kliknij przycisk **ustawienia** > **poświadczenia wdrażania** w bloku aplikacja sieci web.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. W **ustawienia** kliknij **właściwości** wyświetlić zdalnego adresu URL usługi Git należy użyć do wdrożenia aplikacji PHP później.

## <a name="get-sql-database-connection-information"></a>Pobierz informacje dotyczące połączenia bazy danych SQL
Do nawiązania połączenia połączonej z aplikacji sieci web użytkownika spowoduje wystąpienie bazy danych SQL wymagane informacje dotyczące połączenia, która została określona podczas tworzenia bazy danych. Aby uzyskać informacje dotyczące połączenia bazy danych SQL, wykonaj następujące kroki:

1. W bloku grupy zasobów kliknij ikonę bazy danych SQL.
2. W bloku bazy danych SQL, kliknij przycisk **ustawienia** > **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**. 
   
    ![Wyświetl właściwości bazy danych](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Z **PHP** sekcji wynikowy okna dialogowego, zanotuj wartości `Server`, `SQL Database`, i `User Name`. Te wartości będzie używana później podczas publikowania aplikacji sieci web PHP w usłudze Azure App Service.

## <a name="build-and-test-your-application-locally"></a>Kompilowanie i testowanie aplikacji lokalnie
Aplikacja rejestracji jest prostą aplikację PHP, która służy do rejestrowania zdarzenia podając adres nazwę i adres e-mail. Informacje o poprzednim dokonującymi są wyświetlane w tabeli. Informacje rejestracyjne są przechowywane w wystąpieniu bazy danych SQL. Aplikacja składa się z dwóch plików (skopiuj i Wklej kod dostępne poniżej):

* **index.php**: Wyświetla formularz rejestracji i tabelę zawierającą informacje rejestrującego.
* **createtable.php**: tworzy w tabeli bazy danych SQL dla aplikacji. Ten plik zostanie użyte tylko raz.

Aby uruchomić aplikację lokalnie, wykonaj poniższe kroki. Należy pamiętać, że tych krokach przyjęto założenie, PHP i SQL Server Express na komputerze lokalnym, a włączono [PDO rozszerzenia dla programu SQL Server][pdo-sqlsrv].

1. Utwórz bazę danych programu SQL Server o nazwie `registration`. Można to zrobić z `sqlcmd` wiersza polecenia przy użyciu następujących poleceń:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. W katalogu głównym aplikacji, należy utworzyć dwa pliki w nim — jedną o nazwie `createtable.php` i jedną o nazwie `index.php`.
3. Otwórz `createtable.php` plik w edytorze tekstów lub IDE, a następnie dodaj poniższy kod. Ten kod będzie używane do tworzenia `registration_tbl` w tabeli `registration` bazy danych.
   
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
   
    Należy pamiętać, że będzie konieczne zaktualizowanie wartości <code>$user</code> i <code>$pwd</code> z lokalnym nazwa użytkownika serwera SQL i hasło.
4. W terminalu w katalogu głównym aplikacji, wpisz następujące polecenie:
   
        php -S localhost:8000
5. Otwórz przeglądarkę sieci web i przejdź do **http://localhost:8000/createtable.php**. Spowoduje to utworzenie `registration_tbl` tabeli w bazie danych.
6. Otwórz **index.php** plik w edytorze tekstów lub IDE i dodać podstawowe kodu HTML i CSS strony (kodu PHP zostaną dodane w kolejnych krokach).
   
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
7. W tagach PHP należy dodać kodu PHP do łączenia z bazą danych.
   
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
   
    Ponownie, należy zaktualizować wartości <code>$user</code> i <code>$pwd</code> z lokalna MySQL nazwa użytkownika i hasło.
8. Następujący kod połączenia bazy danych Dodaj kod dla wstawiania informacje rejestracyjne w bazie danych.
   
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
9. Na koniec po powyższym kodzie należy dodać kodu do pobierania danych z bazy danych.
   
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

Możesz teraz przejść do **http://localhost:8000/index.php** do testowania aplikacji.

## <a name="publish-your-application"></a>Publikowanie aplikacji
Po przetestowaniu aplikacji lokalnie, można opublikować aplikacji usługi sieci Web aplikacji przy użyciu narzędzia Git. Jednak najpierw musisz zaktualizować informacje o połączeniu bazy danych w aplikacji. Korzystając z bazy danych informacji połączenia uzyskanymi wcześniej (w **informacje o połączeniu pobrać bazy danych SQL** sekcji), zaktualizuj następujące informacje w **zarówno** `createdatabase.php` i `index.php` plików z odpowiednimi wartościami:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> W <code>$host</code>, wartość serwera musi być poprzedzony przez <code>tcp:</code>.
> 
> 

Teraz można przystąpić do ustawiania publikowania w usłudze Git i Opublikuj aplikację.

> [!NOTE]
> Są to te same kroki wymienione na końcu **tworzenie aplikacji sieci web platformy Azure i skonfigurować publikowanie w usłudze Git** powyższej sekcji.
> 
> 

1. Otwórz GitBash (lub terminal, jeśli Git znajduje się w sieci `PATH`), przejdź do katalogu głównego aplikacji ( **rejestracji** katalogu), i uruchom następujące polecenia:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Pojawi się monit o podanie hasła utworzonego wcześniej.
2. Przejdź do **name].azurewebsites.net/createtable.php aplikacji http://[web** można utworzyć tabeli bazy danych SQL dla aplikacji.
3. Przejdź do **name].azurewebsites.net/index.php aplikacji http://[web** aby rozpocząć korzystanie z aplikacji.

Po opublikowaniu aplikacji, można rozpocząć wprowadzania zmian i publikowanie ich przy użyciu narzędzia Git. 

## <a name="publish-changes-to-your-application"></a>Publikowanie zmian w aplikacji
Aby opublikować zmian w aplikacji, wykonaj następujące kroki:

1. Wprowadzanie zmian w aplikacji lokalnie.
2. Otwórz GitBash (lub terminal, it Git jest w Twojej `PATH`), przejdź do katalogu głównego aplikacji i uruchom następujące polecenia:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Pojawi się monit o podanie hasła utworzonego wcześniej.
3. Przejdź do **name].azurewebsites.net/index.php aplikacji http://[web** aby zobaczyć zmiany.

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

