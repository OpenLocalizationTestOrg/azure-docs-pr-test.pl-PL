---
title: "Łączenia z bazą danych Azure dla programu MySQL z MySQL Workbench | Dokumentacja firmy Microsoft"
description: "Ta opcja szybkiego startu zawiera czynności w celu MySQL Workbench do nawiązywania połączeń i zapytania na danych z bazy danych platformy Azure dla programu MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a>Bazy danych platformy Azure dla programu MySQL: MySQL Workbench używany do nawiązywania połączeń i zapytania na danych
Ta opcja szybkiego startu pokazuje, jak nawiązać połączenia z bazą danych Azure dla programu MySQL przy użyciu aplikacji MySQL Workbench. 

## <a name="prerequisites"></a>Wymagania wstępne
Ten przewodnik Szybki start jako punktu wyjścia używa zasobów utworzonych w jednym z tych przewodników:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Zainstaluj narzędzia Workbench MySQL
Pobierz i zainstaluj MySQL Workbench na komputerze z [MySQL witryny sieci Web](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
Pobierz informacje o połączeniu potrzebne do nawiązania połączenia z usługą Azure Database for MySQL. Potrzebna jest w pełni kwalifikowana nazwa serwera i poświadczenia logowania.

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).

2. W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj utworzony serwer, taki jak **myserver4demo**.

3. Kliknij nazwę serwera.

4. Wybierz stronę **Właściwości** serwera. Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.

 ![Bazy danych platformy Azure dla nazwy serwera MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Jeśli nie pamiętasz informacji logowania do serwera, przejdź do strony **Przegląd**, aby wyświetlić nazwę logowania administratora serwera oraz w razie konieczności zresetować hasło.

## <a name="connect-to-the-server-using-mysql-workbench"></a>Połącz z serwerem przy użyciu narzędzia MySQL Workbench 
Aby nawiązać połączenie z serwerem usługi Azure MySQL za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench:

1.  Uruchamianie aplikacji MySQL Workbench na komputerze. 

2.  W **instalacji nowego połączenia** okna dialogowego wprowadź następujące informacje **parametry** karty:

    ![konfigurowanie nowego połączenia](./media/connect-workbench/2-setup-new-connection.png)

    | **Ustawienie** | **Sugerowana wartość** | **Opis pola** |
    |---|---|---|
    |   Nazwa połączenia | Połączenie demonstracyjne | Podaj etykietę dla tego połączenia. |
    | Metoda połączenia | Standardowa (TCP/IP) | Metoda Standardowa (TCP/IP) jest wystarczająca. |
    | Nazwa hosta | *nazwa serwera* | Określ wartość nazwy serwera, która została użyta wcześniej podczas tworzenia usługi Azure Database for MySQL. Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj w pełni kwalifikowanej nazwy domeny (\*.mysql.database.azure.com) tak jak pokazano w przykładzie. Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy serwera.  |
    | Port | 3306 | Zawsze używaj portu 3306 podczas łączenia z usługą Azure Database for MySQL. |
    | Nazwa użytkownika |  *nazwa logowania administratora serwera* | Wpisz nazwę logowania administratora serwera, którą podano wcześniej podczas tworzenia usługi Azure Database for MySQL. Przykładowa nazwa użytkownika to myadmin@myserver4demo. Postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia, jeśli nie pamiętasz nazwy użytkownika. Format to *username@servername*.
    | Hasło | Twoje hasło | Kliknij przycisk **magazynu w magazynie...**  przycisk, aby zapisać hasło. |

3.   Kliknij przycisk **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały prawidłowo skonfigurowane. 

4.   Kliknij przycisk **OK** można zapisać połączenia. 

5.   Na liście z **połączeń MySQL**, kliknij odpowiadający serwera i poczekaj, aby ustanowić połączenie.

6.   Otwiera nową kartę SQL za pomocą edytora puste można wpisać zapytań.

    > [!NOTE]
    > Domyślnie zabezpieczeń połączenia SSL jest wymagany i wymuszane MySQL serwera bazy danych Azure. Zwykle dodatkowa konfiguracja, z certyfikatów SSL nie jest wymagane dla środowiska roboczego MySQL, aby połączyć się z serwerem. Aby uzyskać więcej informacji dotyczących protokołu SSL, zobacz [łączności Konfigurowanie protokołu SSL w celu bezpiecznego łączenia z bazą danych Azure dla programu MySQL aplikacji](./howto-configure-ssl.md).  Jeśli potrzebujesz wyłączyć protokół SSL, można znaleźć w portalu Azure, a następnie kliknij przycisk Strona zabezpieczeń połączeń wyłączenie przycisku przełącznika połączenia SSL wymuszania.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Utwórz tabelę, wstawiania danych, odczytywanie danych, aktualizowanie danych i usuwanie danych
1. Skopiuj i wklej przykładowy kod SQL w puste karcie SQL w celu zilustrowania przykładowych danych.

    Ten kod tworzy pustą bazę danych o nazwie quickstartdb, a następnie tworzy Przykładowa tabela o nazwie spisu. Następnie niektóre wiersze do wstawienia odczytuje wiersze. Zmiany danych za pomocą instrukcji update i odczytuje wiersze ponownie. Na koniec go usuwa wiersz i odczytuje wiersze ponownie.
    
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

    Zrzut ekranu przedstawia przykładowy kod SQL w SQL Workbench i dane wyjściowe po uruchomieniu.
    
    ![MySQL Workbench SQL kartę, aby uruchomić przykładowy kod SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. Aby uruchomić przykładowy kod SQL, kliknij przycisk rozjaśnianego ikonę na pasku narzędzi **pliku SQL** kartę.
3. Zwróć uwagę, trzy karty wyników w **Siatka wyników** sekcji środku strony. 
4. Powiadomienie **dane wyjściowe** listy w dolnej części strony. Zostanie wyświetlony stan każdego polecenia. 

Teraz ma połączonej z bazą danych Azure dla programu MySQL przy użyciu narzędzia MySQL Workbench i wykonano zapytanie danych przy użyciu języka SQL.

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./concepts-migrate-import-export.md)
