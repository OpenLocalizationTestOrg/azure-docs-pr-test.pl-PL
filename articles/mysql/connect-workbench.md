---
title: "Połącz tooAzure bazy danych dla programu MySQL z MySQL Workbench | Dokumentacja firmy Microsoft"
description: "Tego przewodnika Szybki Start zawiera toouse kroki hello MySQL Workbench tooconnect i zapytań dane z bazy danych Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: Użyj MySQL Workbench danych tooconnect i zapytań
Ta opcja szybkiego startu przedstawia sposób tooconnect tooan Azure bazy danych MySQL używania hello aplikacja MySQL Workbench. 

## <a name="prerequisites"></a>Wymagania wstępne
Ta opcja szybkiego startu używa zasobów hello utworzone w jednym z tych wskazówek jako punktu wyjścia:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Zainstaluj narzędzia Workbench MySQL
Pobierz i zainstaluj MySQL Workbench na komputerze z [hello MySQL witryny sieci Web](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz hello połączenia potrzebnych tooconnect toohello bazy danych platformy Azure dla programu MySQL. Należy hello serwera w pełni kwalifikowaną nazwę i poświadczenia logowania.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

2. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby** i wyszukaj powitania serwera po utworzeniu, takich jak **myserver4demo**.

3. Kliknij nazwę serwera hello.

4. Wybierz powitania serwera **właściwości** strony. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**.

 ![Bazy danych platformy Azure dla nazwy serwera MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Jeśli użytkownik zapomni swoje informacje logowania serwera, przejdź toohello **omówienie** strony nazwę logowania administratora serwera hello tooview i w razie potrzeby zresetowania hasła hello.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Połącz serwer toohello przy użyciu narzędzia MySQL Workbench 
za pomocą hello graficznego interfejsu użytkownika narzędzia MySQL Workbench serwer MySQL tooAzure tooconnect:

1.  Uruchom program hello MySQL Workbench aplikacji na komputerze. 

2.  W **instalacji nowego połączenia** okna dialogowego wprowadź następujące informacje na powitania hello **parametry** karty:

    ![konfigurowanie nowego połączenia](./media/connect-workbench/2-setup-new-connection.png)

    | **Ustawienie** | **Sugerowana wartość** | **Opis pola** |
    |---|---|---|
    |   Nazwa połączenia | Połączenie demonstracyjne | Podaj etykietę dla tego połączenia. |
    | Metoda połączenia | Standardowa (TCP/IP) | Metoda Standardowa (TCP/IP) jest wystarczająca. |
    | Nazwa hosta | *nazwa serwera* | Określ wartość hello nazwy serwera, który został użyty podczas hello Azure bazy danych dla programu MySQL wcześniej utworzony. Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj hello pełną nazwę domeny (\*. mysql.database.azure.com) jak pokazano w przykładzie hello. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz nazwę serwera.  |
    | Port | 3306 | Należy zawsze używać portu 3306 podczas łączenia tooAzure bazy danych dla programu MySQL. |
    | Nazwa użytkownika |  *nazwa logowania administratora serwera* | Wpisz powitania serwera admin logowania użytkownika dostarczana, gdy dla programu MySQL utworzony wcześniej hello bazy danych Azure. Przykładowa nazwa użytkownika to myadmin@myserver4demo. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz hello nazwy użytkownika. Hello format jest  *username@servername* .
    | Hasło | Twoje hasło | Kliknij przycisk **magazynu w magazynie...**  przycisk toosave hello hasła. |

3.   Kliknij przycisk **Testuj połączenie** tootest, jeśli wszystkie parametry są poprawnie skonfigurowane. 

4.   Kliknij przycisk **OK** toosave hello połączenia. 

5.   W hello lista **połączeń MySQL**, kliknij odpowiedni serwer tooyour hello kafelków i poczekaj, aż hello toobe połączenie nawiązane.

6.   Otwiera nową kartę SQL za pomocą edytora puste można wpisać zapytań.

    > [!NOTE]
    > Domyślnie zabezpieczeń połączenia SSL jest wymagany i wymuszane MySQL serwera bazy danych Azure. Zwykle nie jest dodatkowa konfiguracja certyfikatów SSL wymagane dla serwera tooyour tooconnect MySQL Workbench. Aby uzyskać więcej informacji dotyczących protokołu SSL, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md).  Toodisable protokołu SSL, należy odwiedzić hello portalu Azure i przycisk hello połączenia zabezpieczeń strony toodisable hello Wymuszanie protokołu SSL połączenia przełącznika.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Utwórz tabelę, wstawiania danych, odczytywanie danych, aktualizowanie danych i usuwanie danych
1. Skopiuj i Wklej hello przykładowy kod SQL w puste tooillustrate kartę SQL przykładowych danych.

    Ten kod tworzy pustą bazę danych o nazwie quickstartdb, a następnie tworzy Przykładowa tabela o nazwie spisu. Wstawia niektórych wierszy następnie odczytuje hello wierszy. Zmienia hello danych za pomocą instrukcji update i odczytuje Witaj ponownie wierszy. Na koniec go usuwa wiersz i odczytuje wierszy hello ponownie.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    Hello zrzut ekranu przedstawia przykład hello kod SQL w danych wyjściowych SQL Workbench i hello, po jego uruchomieniu.
    
    ![Kod SQL próbki toorun karcie SQL Workbench MySQL](media/connect-workbench/3-workbench-sql-tab.png)

2. toorun hello przykładowy kod SQL, kliknij przycisk hello rozjaśnienie ikonę w pasku narzędzi hello hello **pliku SQL** kartę.
3. Zwróć uwagę, hello trzech wyników z kartami w hello **Siatka wyników** sekcji w środku hello hello strony. 
4. Powiadomienie hello **dane wyjściowe** listy u dołu hello hello strony. zostanie wyświetlony stan Hello każdego polecenia. 

Teraz połączyły tooAzure bazy danych dla programu MySQL przy użyciu narzędzia MySQL Workbench i wykonano zapytanie danych przy użyciu języka SQL hello.

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
