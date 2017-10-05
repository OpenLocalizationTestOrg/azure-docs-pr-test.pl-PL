---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak projektować pod kątem PostgreSQL pierwszą bazę danych Azure przy użyciu portalu Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a>Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu portalu Azure

Azure Database for PostgreSQL to usługa zarządzana, która umożliwia uruchamianie i skalowanie w chmurze baz danych PostgreSQL o wysokiej dostępności, a także zarządzanie nimi. Przy użyciu portalu Azure, można łatwo zarządzać serwerem i projektowanie bazy danych.

W tym samouczku, użyj portalu Azure Aby dowiedzieć się, jak:
> [!div class="checklist"]
> * Tworzenie serwera usługi Azure Database for PostgreSQL
> * Konfigurowanie zapory serwera
> * Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

## <a name="prerequisites"></a>Wymagania wstępne
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="log-in-to-the-azure-portal"></a>Logowanie do witryny Azure Portal
Zaloguj się do witryny [Azure Portal](https://portal.azure.com).

## <a name="create-an-azure-database-for-postgresql"></a>Tworzenie serwera usługi Azure Database for PostgreSQL

Serwer usługi Azure Database for PostgreSQL jest tworzony ze zdefiniowanym zestawem [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md). Serwer jest tworzony w ramach [grupy zasobów Azure](../azure-resource-manager/resource-group-overview.md).

Wykonaj następujące kroki, aby utworzyć serwer usługi Azure Database for PostgreSQL:
1.  Kliknij przycisk **+ nowy** znaleziono przycisku w lewym górnym rogu portalu Azure.
2.  Na stronie **Nowy** wybierz pozycję **Bazy danych**, a następnie na stronie **Bazy danych** wybierz pozycję **Azure Database for PostgreSQL**.
 ![Usługa Azure Database for PostgreSQL — tworzenie bazy danych](./media/tutorial-design-database-using-azure-portal/1-create-database.png)

3.  Wypełnij formularz informacjami o szczegółach nowego serwera w sposób pokazany na wcześniejszej ilustracji, używając następujących informacji:
    - Nazwa serwera: **mypgserver-20170401** (nazwa serwera jest mapowana na nazwę DNS i dlatego musi być globalnie unikatowa) 
    - Subskrypcja: jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w ramach której istnieje zasób lub będą za niego naliczane opłaty.
    - Grupa zasobów: **myresourcegroup**
    - Wybrane przez Ciebie login i hasło administratora serwera
    - Lokalizacja
    - Wersja PostgreSQL

  > [!IMPORTANT]
  > Login i hasło administratora serwera określone w tym miejscu będą wymagane do logowania do serwera i jego baz danych w późniejszej części tego przewodnika Szybki start. Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.

4.  Kliknij pozycję **Warstwa cenowa**, aby określić warstwę usługi i poziom wydajności dla nowej bazy danych. W tym przewodniku Szybki start wybierz warstwę **Podstawowa**, **50 jednostek obliczeniowych** i **50 GB** dołączonej pamięci.
 ![Usługa Azure Database for PostgreSQL — wybór warstwy usług](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)
5.  Kliknij przycisk **OK**.
6.  Kliknij przycisk **Utwórz**, aby aprowizować serwer. Aprowizacja zajmuje kilka minut.

  > [!TIP]
  > Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, aby łatwo śledzić wdrożenia.

7.  Na pasku narzędzi kliknij pozycję **Powiadomienia**, aby monitorować proces wdrażania.
 ![Usługa Azure Database for PostgreSQL — patrz Powiadomienia](./media/tutorial-design-database-using-azure-portal/3-notifications.png)
   
  Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze. Baza danych [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) to domyślna baza danych przeznaczona do użycia dla użytkowników oraz na potrzeby narzędzi i aplikacji innych firm. 

## <a name="configure-a-server-level-firewall-rule"></a>Konfigurowanie reguły zapory na poziomie serwera

Usługa Azure Database for PostgreSQL tworzy zaporę na poziomie serwera. Ta zapora uniemożliwia zewnętrznym aplikacjom i narzędziom łączenie się z serwerem i wszelkimi bazami danych na tym serwerze, chyba że zostanie utworzona reguła zapory otwierająca zaporę dla konkretnych adresów IP. 

1.  Po zakończeniu wdrożenia kliknij pozycję **Wszystkie zasoby** w menu po lewej stronie i wpisz nazwę **mypgserver-20170401**, aby wyszukać nowo utworzony serwer. Kliknij nazwę serwera wyświetlaną w wynikach wyszukiwania. Zostanie otwarta strona **Przegląd**, która zawiera dalsze opcje konfiguracji.
 
 ![Azure Database for PostgreSQL — wyszukiwanie serwera ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  W bloku serwera wybierz opcję **Zabezpieczenia połączeń**. 
3.  Kliknij w polu tekstowym w obszarze **Nazwa reguły** i dodaj nową regułę zapory, aby na liście dozwolonych umieścić zakres adresów IP służących do łączności. W tym samouczku umożliwia Zezwalaj na wszystkie adresy IP, wpisując w **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** i **końcowemu adresowi IP = 255.255.255.255** , a następnie kliknij przycisk **Zapisz** . Możesz ustawić regułę zapory uwzględniającą zakres adresów IP, aby mieć możliwość nawiązywania połączeń z Twojej sieci.
 
 ![Usługa Azure Database for PostgreSQL — tworzenie reguły zapory](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  Kliknij przycisk **Zapisz**, a następnie kliknij przycisk **X**, aby zamknąć stronę **Zabezpieczenia połączeń**.

  > [!NOTE]
  > Serwer Azure PostgreSQL komunikuje się przez port 5432. Jeśli próbujesz nawiązać połączenie z sieci firmowej, ruch wychodzący na porcie 5432 może być zablokowany przez zaporę sieciową. Jeśli zachodzi taka sytuacja, nie będzie można nawiązać połączenia z serwerem usługi Azure SQL Database, chyba że dział IT otworzy port 5432.
  >


## <a name="get-the-connection-information"></a>Pobieranie informacji o połączeniu

Podczas tworzenia serwera usługi Azure Database for PostgreSQL, domyślnie jest także tworzona baza danych **postgres**. Aby nawiązać połączenie z serwerem bazy danych, musisz podać informacje o hoście i poświadczenia dostępu.

1. W menu po lewej stronie w witrynie Azure Portal kliknij pozycję **Wszystkie zasoby** i wyszukaj właśnie utworzony serwer **mypgserver 20170401**.

  ![Azure Database for PostgreSQL — wyszukiwanie serwera ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. Kliknij nazwę serwera **mypgserver 20170401**.
4. Wybierz stronę serwera **Przegląd**. Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**.

 ![Azure Database for PostgreSQL — dane logowania administratora serwera](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a>Nawiązywanie połączenia z bazą danych PostgreSQL w powłoce Cloud Shell za pomocą narzędzia psql

Użyj teraz narzędzia wiersza polecenia psql, aby nawiązać połączenie z serwerem usługi Azure Database for PostgreSQL. 
1. Uruchom powłokę Azure Cloud Shell za pośrednictwem ikony terminala w górnym okienku nawigacji.

   ![Azure Database for PostgreSQL — ikona terminala powłoki Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. Powłoka Azure Cloud Shell zostanie otwarta w przeglądarce, umożliwiając wpisywanie poleceń powłoki bash.

   ![Azure Database for PostgreSQL — znak zachęty powłoki Azure Shell Bash](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. W wierszu polecenia powłoki Cloud Shell nawiąż połączenie z serwerem usługi Azure Database for PostgreSQL za pomocą poleceń psql. Następujący format służy do łączenia z serwerem usługi Azure Database for PostgreSQL przy użyciu narzędzia [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html):
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   Na przykład poniższe polecenie nawiązuje połączenie z domyślną bazą danych o nazwie **postgres** na Twoim serwerze PostgreSQL **mypgserver-20170401.postgres.database.azure.com** za pomocą poświadczeń dostępu. Po wyświetleniu monitu wprowadź hasło administratora serwera.

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a>Utwórz nową bazę danych
Po nawiązaniu połączenia z serwerem utwórz pustą bazę danych za pomocą wiersza polecenia.
```bash
CREATE DATABASE mypgsqldb;
```

W wierszu polecenia wykonaj poniższe polecenie, aby przełączyć połączenie na nowo utworzoną bazę danych **mypgsqldb**.
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a>Tworzenie tabel w bazie danych
Teraz, Znając sposób nawiązywania połączenia z bazą danych Azure dla PostgreSQL możemy przekazywane sposób wykonania zadania podstawowe.

Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych. Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Nowo utworzona tabela na liście tabvles można teraz wyświetlić, wpisując:
```sql
\dt
```

## <a name="load-data-into-the-tables"></a>Ładowanie danych do tabel
Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego. W oknie Otwórz okno wiersza polecenia Uruchom następujące zapytanie do wstawienia niektórych wierszy danych
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Masz teraz dwa wiersze przykładowych danych do tabeli utworzony wcześniej.

## <a name="query-and-update-the-data-in-the-tables"></a>Zapytania i zaktualizować dane w tabelach
Wykonaj następujące zapytanie, aby pobrać informacje z tabeli bazy danych. 
```sql
SELECT * FROM inventory;
```

Możesz również zaktualizować dane w tabelach
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Wiersz jest odpowiednio aktualizowany podczas pobierania danych.
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a>Przywróć dane z wcześniejszego punktu w czasie
Załóżmy, że zostanie przypadkowo usunięte w tej tabeli. Ta sytuacja jest coś, co nie można łatwo odzyskać z. Bazy danych platformy Azure dla PostgreSQL umożliwia wróć do dowolnego punktu na czas (w ostatnim maksymalnie 7 dni (Basic), a 35 dni (standardowe)) i przywrócić tego punktu w czasie na nowy serwer. Możesz użyć tego nowego serwera, aby odzyskać usunięte dane. Poniższe kroki należy przywrócić działanie serwera próbki do punktu przed tabeli został dodany.

1.  W bazie danych Azure PostgreSQL strony serwera, kliknij przycisk **przywrócić** na pasku narzędzi. **Przywrócić** zostanie otwarta strona.
  ![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)
2.  Wypełnianie **przywrócić** formularza z informacjami wymaganymi:

  ![Portal Azure — opcje przywracania formularza](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - **Punkt przywracania**: Wybierz w momencie po serwer został zmieniony
  - **Serwer docelowy**: Podaj nową nazwę serwera mają zostać przywrócone
  - **Lokalizacja**: nie można wybrać region, domyślnie jest taki sam jak serwer źródłowy
  - **Warstwa cenowa**: nie można zmienić tę wartość podczas przywracania serwera. Jest taki sam jak serwer źródłowy. 
3.  Kliknij przycisk **OK** Aby przywrócić serwer do [Przywracanie do punktu w czasie](./howto-restore-server-portal.md) przed tabele został usunięty. Przywracanie serwera do innego punktu w czasie tworzy zduplikowane nowy serwer jako oryginalnego serwera, począwszy od punktu w czasie, możesz określić, pod warunkiem, że w okresie przechowywania dla Twojego [warstwy usług](./concepts-service-tiers.md).

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób użycia portalu Azure i inne narzędzia do:
> [!div class="checklist"]
> * Tworzenie serwera usługi Azure Database for PostgreSQL
> * Konfigurowanie zapory serwera
> * Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) narzędzie do tworzenia bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

Następnie Dowiedz się, jak użyć wiersza polecenia platformy Azure do wykonywania zadań podobne, przejrzyj tego samouczka: [projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure](tutorial-design-database-using-azure-cli.md)
