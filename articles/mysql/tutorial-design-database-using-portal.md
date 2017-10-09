---
title: aaaDesign pierwszy Azure bazy danych dla bazy danych MySQL - portalu Azure | Dokumentacja firmy Microsoft
description: "Ten samouczek wyjaśnia sposób toocreate i zarządzanie bazą danych Azure MySQL serwera i bazy danych przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL
Bazy danych platformy Azure dla programu MySQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności baz danych MySQL w chmurze hello. Przy użyciu hello portalu Azure, można łatwo zarządzać serwerem i projektowanie bazy danych.

W tym samouczku użyjesz hello toolearn portalu Azure, jak do:

> [!div class="checklist"]
> * Utwórz bazę danych systemu Azure dla programu MySQL
> * Konfigurowanie zapory serwera hello
> * Użyj mysql narzędzia wiersza polecenia toocreate bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

## <a name="sign-in-toohello-azure-portal"></a>Zaloguj się toohello portalu Azure
Otwórz przeglądarkę sieci web Ulubione, a następnie odwiedź hello [portalu Microsoft Azure](https://portal.azure.com/). Wprowadź toosign Twoje poświadczenia w portalu toohello. Widok domyślny Hello jest pulpit nawigacyjny usługi.

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Serwer usługi Azure Database for MySQL jest tworzony za pomocą zdefiniowanego zestawu [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md). Serwer Hello jest tworzony w [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Przejdź za**baz danych** > **bazy danych Azure dla programu MySQL**. Jeśli nie można znaleźć serwera MySQL w obszarze **baz danych** kategorii, kliknij przycisk **zobaczyć wszystkie** tooshow wszystkie dostępne usługi bazy danych. Możesz także wpisać **bazy danych Azure dla programu MySQL** w tooquickly pole wyszukiwania hello znaleźć hello usługi.
![TooMySQL Nawigacja 2-1](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Kliknij przycisk **bazy danych Azure dla programu MySQL** Kafelek, a następnie kliknij przycisk **Utwórz**.

W naszym przykładzie wypełnić hello Azure bazy danych MySQL formularza z hello następujących informacji:

| **Ustawienie** | **Sugerowana wartość** | **Opis pola** |
|---|---|---|
| *Nazwa serwera* | myserver4demo  | Nazwa serwera ma toobe globalnie unikatowe. |
| *Subskrypcja* | mysubscription | Wybierz subskrypcję z listy rozwijanej hello. |
| *Grupa zasobów* | myresourcegroup | Utwórz grupę zasobów lub wybierz istniejącą. |
| *Identyfikator logowania administratora serwera* | myadmin | Konfiguracja nazwy konta administratora. |
| *Hasło* |  | Ustaw silne hasło do konta administratora. |
| *Potwierdź hasło* |  | Potwierdź hasło konta administratora hello. |
| *Lokalizacja* |  | Wybierz dostępny region. |
| *Wersja* | 5.7 | Wybierz hello najnowszej wersji. |
| *Konfigurowanie wydajności* | Podstawowe, 50 obliczeniowe jednostki, 50 GB  | Wybierz pozycje **Warstwa cenowa**, **Jednostki obliczeniowe** i **Magazyn (GB)**, a następnie kliknij przycisk **OK**. |
| *TooDashboard numeru PIN* | Zaznacz | Zalecane toocheck to pole, więc może zajść łatwo później na powitania serwera |
Następnie kliknij pozycję **Utwórz**. Minucie lub dwóch nowej bazy danych Azure MySQL serwera jest uruchomiona w chmurze hello. Możesz kliknąć **powiadomienia** przycisk na proces wdrażania hello hello narzędzi toomonitor.

## <a name="configure-firewall"></a>Konfigurowanie zapory
Azure bazy danych dla programu MySQL są chronione przez zaporę. Domyślnie wszystkie połączenia toohello serwera i hello bazy danych wewnątrz powitania serwera są odrzucane. Przed utworzeniem połączenia tooAzure bazy danych MySQL na powitania po raz pierwszy, skonfiguruj adres IP w sieci publicznej hello zapory tooadd powitania klienta na komputerze (lub zakres adresów IP).

1. Kliknij nowo utworzonego serwera, a następnie kliknij przycisk **zabezpieczenia połączeń**.
   ![Zabezpieczenia połączeń 3-1](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Możesz **dodać Moje IP**, lub skonfigurować reguły zapory w tym miejscu. Należy pamiętać, tooclick **zapisać** po utworzeniu reguły hello.
Teraz możesz połączyć toohello serwera za pomocą narzędzia wiersza polecenia mysql lub MySQL Workbench graficznego interfejsu użytkownika.

> [!TIP]
> Azure bazy danych MySQL serwera komunikuje się za pośrednictwem portu 3306. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 3306 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie można połączyć serwer MySQL tooAzure, chyba że dział IT otwiera port 3306.

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu
W pełni kwalifikowana hello GET **nazwy serwera** i **nazwę logowania administratora serwera** bazy danych Azure, aby serwer MySQL z hello portalu Azure. Możesz użyć hello pełną nazwę tooconnect tooyour serwera za pomocą narzędzia wiersza polecenia mysql. 

1. W [portalu Azure](https://portal.azure.com/), kliknij przycisk **wszystkie zasoby** z menu po lewej stronie powitania, nazwa typu hello i wyszukaj bazy danych Azure, aby serwer MySQL. Wybierz hello — szczegóły hello tooview nazwy serwera.

2. W obszarze hello ustawienia kliknij pozycję **właściwości**. Należy zanotować **nazwy serwera** i **nazwę logowania administratora serwera**. Możesz kliknąć pozycję hello Kopiuj przycisku Dalej tooeach pola toocopy toohello Schowka.
   ![właściwości serwera 4-2](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

W tym przykładzie nazwa serwera hello jest *myserver4demo.mysql.database.azure.com*, i jest identyfikator logowania administratora serwera hello  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Połącz serwer toohello przy użyciu mysql
Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour połączenia bazy danych platformy Azure dla serwera MySQL. Z hello powłoki chmury Azure w przeglądarce hello lub własnego komputera przy użyciu narzędzia mysql zainstalowane lokalnie, można uruchomić narzędzie wiersza polecenia hello mysql. toolaunch hello powłoki chmury Azure, kliknij przycisk hello `Try It` przycisk blokiem kodu w tym artykule, lub odwiedź hello portalu Azure i kliknij przycisk hello `>_` ikonę w górnym prawym narzędzi hello. 

Wpisz tooconnect polecenie hello:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Tworzenie pustej bazy danych
Po wyświetleniu serwera połączonych toohello utworzyć toowork pustą bazę danych, z.
```sql
CREATE DATABASE mysampledb;
```

W wierszu hello Uruchom hello następujące polecenia tooswitch połączenia toothis nowo utworzone w bazie danych:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Tworzenie tabel w bazie danych hello
Teraz, gdy wiesz, jak tooconnect toohello Azure bazy danych dla bazy danych MySQL, firma Microsoft może przejść przez jak toocomplete niektóre podstawowe zadania.

Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych. Teraz utworzyć tabelę, która przechowuje informacje dotyczące spisu.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Ładowanie danych do tabel hello
Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego. W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Zapytania i Aktualizuj hello dane w tabelach hello
Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello.
```sql
SELECT * FROM inventory;
```

Należy również zaktualizować hello dane w tabelach hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Przywracanie bazy danych tooa poprzedniego punktu w czasie
Wyobraź sobie przypadkowo usunięto tabelę ważne bazy danych i nie można łatwo odzyskać hello danych. Bazy danych platformy Azure dla programu MySQL pozwala toorestore powitania serwera tooa punktu w czasie, tworząc kopię hello baz danych do nowego serwera. Można użyć tego nowego serwera toorecover usunięte dane. Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.

1. W portalu Azure hello Znajdź bazy danych Azure dla programu MySQL. Na powitania **omówienie** kliknij przycisk **przywrócić** na powitania narzędzi. zostanie otwarta strona przywracania Hello.

   ![10-1 przywracania bazy danych](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Wypełnianie hello **przywrócić** formularza hello wymagane informacje.
   
   ![Formularz przywracania 10-2](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Punkt przywracania**: Wybierz w momencie, które mają toorestore, w czasie hello na liście. Upewnij się, że tooconvert tooUTC Twojego lokalną strefę czasową.
   - **Przywracanie serwera toonew**: Podaj nową nazwę serwera ma toorestore do.
   - **Lokalizacja**: hello region jest taki sam jak powitania serwera źródłowego i nie można zmienić.
   - **Warstwa cenowa**: hello warstwa cenowa jest hello identyczny powitania serwera źródłowego i nie można zmienić.
   
3. Kliknij przycisk **OK** toorestore hello serwera zbyt[tooa punktu przywracania w czasie](./howto-restore-server-portal.md) przed hello tabeli został usunięty. Przywracanie serwera tworzy nową kopię powitania serwera, począwszy od hello punktu w czasie, które określisz. 

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyjesz hello toolearned portalu Azure, jak do:

> [!div class="checklist"]
> * Utwórz bazę danych systemu Azure dla programu MySQL
> * Konfigurowanie zapory serwera hello
> * Użyj mysql narzędzia wiersza polecenia toocreate bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

> [!div class="nextstepaction"]
> [Jak tooconnect tooAzure aplikacji bazy danych MySQL](./howto-connection-string.md)
