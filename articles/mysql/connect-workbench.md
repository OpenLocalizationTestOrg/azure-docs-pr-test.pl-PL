---
title: "Nawiązywanie połączeń z usługą Azure Database for MySQL za pomocą aplikacji MySQL Workbench | Microsoft Docs"
description: "Ten przewodnik Szybki start zawiera działania umożliwiające wykorzystanie aplikacji MySQL Workbench do nawiązywania połączeń z danymi usługi Azure Database for MySQL i wykonywania zapytań względem nich."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 09/22/2017
ms.openlocfilehash: 4214b80dc4c5db644d5a05f942907c86f292fe18
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2018
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a>Usługa Azure Database for MySQL: nawiązywanie połączeń z danymi i wykonywanie na nich zapytań przy użyciu aplikacji MySQL Workbench
Ten przewodnik Szybki start przedstawia sposób nawiązywania połączeń z usługą Azure Database for MySQL przy użyciu aplikacji MySQL Workbench. 

## <a name="prerequisites"></a>Wymagania wstępne
Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Instalacja aplikacji MySQL Workbench
Pobierz i zainstaluj aplikację MySQL Workbench na komputerze przy użyciu [witryny internetowej MySQL](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL. Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).

2. W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **myserver4demo**.

3. Kliknij nazwę serwera.

4. Wybierz stronę **Właściwości** serwera, a następnie zanotuj **nazwę serwera** i **nazwę logowania administratora serwera**.

 ![Nazwa serwera usługi Azure Database for MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.

## <a name="connect-to-the-server-by-using-mysql-workbench"></a>Nawiązywanie połączenia z serwerem za pomocą aplikacji MySQL Workbench 
Aby nawiązać połączenie z serwerem usługi Azure MySQL za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench:

1.  Uruchom aplikację MySQL Workbench na swoim komputerze. 

2.  W oknie dialogowym **Setup New Connection** (Konfigurowanie nowego połączenia) wprowadź poniższe informacje na karcie **Parameters** (Parametry):

    ![konfigurowanie nowego połączenia](./media/connect-workbench/2-setup-new-connection.png)

    | **Ustawienie** | **Sugerowana wartość** | **Opis pola** |
    |---|---|---|
    |   Nazwa połączenia | Połączenie demonstracyjne | Podaj etykietę dla tego połączenia. |
    | Metoda połączenia | Standardowa (TCP/IP) | Metoda Standardowa (TCP/IP) jest wystarczająca. |
    | Nazwa hosta | *nazwa serwera* | Określ wartość nazwy serwera, która została użyta wcześniej podczas tworzenia usługi Azure Database for MySQL. Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj w pełni kwalifikowanej nazwy domeny (\*.mysql.database.azure.com) tak jak pokazano w przykładzie. Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy serwera.  |
    | Port | 3306 | Zawsze używaj portu 3306 podczas łączenia z usługą Azure Database for MySQL. |
    | Nazwa użytkownika |  *nazwa logowania administratora serwera* | Wpisz nazwę logowania administratora serwera, którą podano wcześniej podczas tworzenia usługi Azure Database for MySQL. Przykładowa nazwa użytkownika to myadmin@myserver4demo. Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy użytkownika. Format to *username@servername*.
    | Hasło | Twoje hasło | Aby zapisać hasło, kliknij przycisk **Store in Vault...** (Zapisz w magazynie...). |

3.   Kliknij przycisk **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały prawidłowo skonfigurowane. 

4.   Kliknij przycisk **OK**, aby zapisać połączenie. 

5.   Na liście **MySQL Connections** (Połączenia MySQL) kliknij kafelek odpowiadający serwerowi, a następnie poczekaj na ustanowienie połączenia.

        Zostanie otwarta nowa karta SQL z pustym edytorem, w którym można wpisać swoje zapytania.
    
        > [!NOTE]
        > Domyślnie wymagane i wymuszane są zabezpieczenia połączenia SSL serwera Azure Database for MySQL. Mimo że zazwyczaj nawiązanie połączenia aplikacji MySQL Workbench z serwerem nie wymaga dodatkowej konfiguracji przy użyciu certyfikatów SSL, zalecamy powiązanie certyfikatu SSL urzędu certyfikacji z aplikacją MySQL Workbench. Aby uzyskać więcej informacji na temat sposobu ładowania certyfikatu i tworzenia jego powiązania, zobacz [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL (Konfigurowanie łączności SSL w aplikacji w celu bezpiecznego nawiązywania połączeń z usługą Azure Database for MySQL)](./howto-configure-ssl.md).  Jeśli chcesz wyłączyć protokół SSL, przejdź do witryny Azure Portal, kliknij stronę Zabezpieczenia połączeń i kliknij przycisk przełączania Wymuszaj połączenie SSL.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Tworzenie tabeli, wstawianie danych, odczyt danych, aktualizowanie danych, usuwanie danych
1. Skopiuj i wklej przykładowy kod SQL w pustej karcie SQL w celu zilustrowania przykładowych danych.

    Ten kod tworzy pustą bazę danych o nazwie quickstartdb, a następnie tworzy przykładową tabelę o nazwie inventory. Wstawia pewne wiersze, a następnie odczytuje wiersze. Zmienia dane za pomocą instrukcji update i odczytuje wiersze ponownie. Na końcu usuwa wiersz, po czym ponownie odczytuje wiersze.
    
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

    Zrzut ekranu przedstawia przykładowy kod SQL w aplikacji SQL Workbench i dane wyjściowe po jego uruchomieniu.
    
    ![Karta SQL aplikacji MySQL Workbench umożliwia uruchamianie przykładowego kodu SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. Aby uruchomić przykładowy kod SQL, kliknij ikonę pioruna na pasku narzędzi karty **SQL File** (Plik SQL).
3. Zwróć uwagę na trzy karty wyników w sekcji **Result Grid** (Siatka wyników) pośrodku strony. 
4. Zwróć uwagę na listę **Output** (Dane wyjściowe) w dolnej części strony. Zawiera ona stan każdego polecenia. 

Nawiązano połączenie z usługą Azure Database for MySQL przy użyciu aplikacji MySQL Workbench i wykonano zapytanie o dane przy użyciu języka SQL.

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
