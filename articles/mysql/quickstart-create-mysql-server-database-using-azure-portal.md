---
title: "Szybki start: Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal | Microsoft Docs"
description: "W tym artykule podano instrukcje pozwalające utworzyć przykładowy serwer usługi Azure Database for MySQL za pomocą witryny Azure Portal w czasie około pięciu minut."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: quickstart
ms.date: 11/01/2017
ms.openlocfilehash: f427b23ca4b48da79759584bdcc98c1002c054c1
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2017
---
# <a name="create-an-azure-database-for-mysql-server-by-using-the-azure-portal"></a>Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal
Azure Database for MySQL to usługa zarządzana, która umożliwia uruchamianie i skalowanie w chmurze baz danych MySQL o wysokiej dostępności, a także zarządzanie nimi. W tym przewodniku Szybki start przedstawiono, jak utworzyć serwer usługi Azure Database for MySQL za pomocą witryny Azure Portal w ciągu okołu pięciu minut.  

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).

## <a name="sign-in-to-azure"></a>Logowanie do platformy Azure
Otwórz przeglądarkę internetową, a następnie przejdź do witryny [Azure Portal](https://portal.azure.com/). Wprowadź swoje poświadczenia, aby zalogować się do portalu. Widok domyślny to pulpit nawigacyjny usług.

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Serwer usługi Azure Database for MySQL jest tworzony za pomocą zdefiniowanego zestawu [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md). Serwer jest tworzony w ramach [grupy zasobów Azure](../azure-resource-manager/resource-group-overview.md).

Wykonaj następujące kroki, aby utworzyć serwer usługi Azure Database for MySQL:

1. Wybierz przycisk **Nowy** (+) w lewym górnym rogu portalu.

2. Wybierz pozycję **Bazy danych** > **Azure Database for MySQL**. Możesz również wpisać hasło **MySQL** w polu wyszukiwania, aby znaleźć tę usługę.

    ![Opcja Azure Database for MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

4. Wypełnij formularz informacjami o szczegółach nowego serwera w sposób pokazany na wcześniejszej ilustracji, używając następujących informacji:

    **Ustawienie** | **Sugerowana wartość** | **Opis pola** 
    ---|---|---
    Nazwa serwera | Unikatowa nazwa serwera | Wybierz unikatową nazwę, która identyfikuje serwer usługi Azure Database for MySQL. Przykład: mojserwer4demo. Nazwa domeny *mysql.database.azure.com* jest dołączana do podawanej nazwy serwera. Nazwa serwera może zawierać tylko małe litery, cyfry i znaki łącznika (-). Musi zawierać od 3 do 63 znaków.
    Subskrypcja | Twoja subskrypcja | Wybierz subskrypcję platformy Azure, która ma być używana dla serwera. Jeśli masz wiele subskrypcji, wybierz tę, w ramach której są naliczane opłaty za ten zasób.
    Grupa zasobów | myresourcegroup | Podaj nazwę nowej lub istniejącej grupy zasobów.
    Identyfikator logowania administratora serwera | myadmin | Konto logowania do użycia podczas łączenia z serwerem. Nazwą logowania administratora nie może być **azure_superuser**, **admin**, **administrator**, **root**, **guest** ani **public**.
    Hasło | *Wartość wybrana przez użytkownika* | Podaj nowe hasło dla konta administratora serwera. Musi zawierać od 8 do 128 znaków. Hasło musi zawierać znaki z trzech z następujących kategorii: wielkie litery angielskie, małe litery angielskie, cyfry (0–9) i znaki inne niż alfanumeryczne (!, $, #, % itp.).
    Potwierdź hasło | *Wartość wybrana przez użytkownika*| Potwierdź hasło do konta administratora.
    Lokalizacja | *Region najbliżej Twoich użytkowników*| Wybierz lokalizację najbliżej użytkowników lub innych aplikacji Azure.
    Wersja | *Najnowsza wersja*| Najnowsza wersja, chyba że z konkretnych powodów wymagana jest inna wersja.
    Warstwa cenowa | **Podstawowa**, **50 jednostek obliczeniowych**, **50 GB** | Wybierz warstwę usługi i poziom wydajności nowej bazy danych. Na karcie w górnej części wybierz pozycję **Warstwa Podstawowa**. Wybierz lewy koniec suwaka **Jednostki obliczeniowe**, aby dopasować wartość do najmniejszą dostępnej dla tego przewodnika Szybki start. Wybierz przycisk **OK**, aby zapisać wybraną warstwę cenową. Aby uzyskać więcej informacji, zobacz poniższy zrzut ekranu.
    Przypnij do pulpitu nawigacyjnego | Zaznacz | Zaznacz tę opcję, aby umożliwić łatwe monitorowanie serwera na pierwszej stronie pulpitu nawigacyjnego witryny Azure Portal.

    > [!IMPORTANT]
    > Nazwa logowania i hasło administratora serwera określone w tym miejscu będą wymagane do logowania do serwera i jego baz danych w późniejszej części tego przewodnika Szybki start. Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.
    > 

    ![Witryna Azure Portal — tworzenie serwera MySQL przez podanie w formularzu wymaganych danych wejściowych](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Wybierz pozycję **Utwórz**, aby aprowizować serwer. Aprowizowanie może zająć do 20 minut.
   
5.  Wybierz pozycję **Powiadomienia** (ikonę dzwonka) na pasku narzędzi, aby monitorować proces wdrażania.

## <a name="configure-a-server-level-firewall-rule"></a>Konfigurowanie reguły zapory na poziomie serwera

Usługa Azure Database for MySQL tworzy zaporę na poziomie serwera. Uniemożliwia ona zewnętrznym aplikacjom i narzędziom łączenie się z serwerem i wszelkimi bazami danych na tym serwerze, chyba że zostanie utworzona reguła zapory otwierająca zaporę dla konkretnych adresów IP. 

1.   Po zakończeniu wdrażania odszukaj serwer. Jeśli to konieczne, możesz go wyszukać. Na przykład wybierz pozycję **Wszystkie zasoby** z menu po lewej stronie. Wpisz nazwę serwera (takiego jak przykładowy serwer **myserver4demo**), aby wyszukać nowo utworzony serwer. Wybierz nazwę serwera z listy wyników wyszukiwania. Zostanie otwarta strona **Przegląd**, która zawiera dalsze opcje konfiguracji.

2. Na stronie serwera wybierz pozycję **Zabezpieczenia połączeń**.

3.  W obszarze z nagłówkiem **Reguły zapory** wybierz puste pole tekstowe w kolumnie **Nazwa reguły**, aby rozpocząć tworzenie reguły zapory. 

   ![Zabezpieczenia połączeń — reguły zapory](./media/quickstart-create-mysql-server-database-using-azure-portal/5_firewall-settings.png)

   W tym przewodniku Szybki start zezwolimy na wszystkie adresy IP na serwerze, wypełniając pola w poszczególnych kolumnach następującymi wartościami:

   Nazwa reguły | Początkowy adres IP | Końcowy adres IP 
   ---|---|---
   AllowAllIps |  0.0.0.0 | 255.255.255.255
   
   Zezwalanie na wszystkie adresy IP nie jest bezpieczne. Ten przykład podano dla uproszczenia, ale w rzeczywistym scenariuszu musisz dokładnie znać zakresy adresów IP, które chcesz dodać dla aplikacji i użytkowników. 

4. Na górnym pasku narzędzi strony **Zabezpieczenia połączeń** wybierz pozycję **Zapisz**. Przed kontynuowaniem zaczekaj, aż pojawi się powiadomienie, że aktualizacja została zakończona pomyślnie. 

   > [!NOTE]
   > Połączenia z usługą Azure Database for MySQL korzystają z portu 3306. Jeśli próbujesz nawiązać połączenie z sieci firmowej, ruch wychodzący na porcie 3306 może być zablokowany. W takim przypadku nie będzie można nawiązać połączenia z serwerem, chyba że dział informatyczny otworzy port 3306.
   > 

## <a name="get-the-connection-information"></a>Pobieranie informacji o połączeniu
Aby można było nawiązać połączenie z serwerem bazy danych, potrzebne są pełna nazwa serwera i poświadczenia logowania administratora. Być może te wartości zostały zanotowane wcześniej podczas pracy z artykułem Szybki start. W przeciwnym razie możesz łatwo odnaleźć nazwę serwera i informacje dotyczące logowania na stronie **Przegląd** lub **Właściwości** serwera w witrynie Azure Portal.

Aby je znaleźć, wykonaj następujące czynności: 

1. Otwórz stronę **Przegląd** serwera. Zanotuj wartości **Nazwa serwera** i **Identyfikator logowania administratora serwera**. 

2. Umieszczaj kursor nad poszczególnymi polami, a po prawej stronie tekstu pojawi się ikona kopiowania. Wybierz ikonę kopiowania, aby w razie potrzeby skopiować wartości.

W tym przykładzie nazwa serwera to **myserver4demo.mysql.database.azure.com**, a identyfikator logowania administratora serwera to **myadmin@myserver4demo**.

## <a name="connect-to-mysql-by-using-the-mysql-command-line-tool"></a>Nawiązywanie połączenia z serwerem MySQL za pomocą narzędzia wiersza polecenia mysql
Istnieje wiele aplikacji, za pomocą których można nawiązać połączenie z serwerem usługi Azure Database for MySQL. 

Użyjmy najpierw narzędzia wiersza polecenia [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html), aby zilustrować procedurę nawiązywania połączenia z serwerem. Możesz użyć przeglądarki internetowej i usługi Azure Cloud Shell w opisany sposób bez instalowania żadnego dodatkowego oprogramowania. Jeśli masz zainstalowane lokalnie narzędzie mysql, możesz nawiązać połączenie także lokalnie.

1. Uruchom usługę Azure Cloud Shell za pomocą ikony terminalu (**>_**) w prawej górnej części witryny Azure Portal.

2.  Usługa Azure Cloud Shell zostanie otwarta w przeglądarce, umożliwiając wpisywanie poleceń powłoki Bash.

    ![Wiersz polecenia — przykładowy wiersz polecenia mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. W wierszu polecenia usługi Cloud Shell nawiąż połączenie z serwerem usługi Azure Database for MySQL, wpisując wiersz polecenia mysql.

    Następujący format służy do łączenia z serwerem usługi Azure Database for MySQL przy użyciu narzędzia mysql:

    ```bash
    mysql --host <fully qualified servername> --user <serveradminlogin@servername> -p
    ```

    Na przykład następujące polecenie umożliwia połączenie z przykładowym serwerem:

    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo -p
    ```

    Parametr narzędzia mysql |Sugerowana wartość|Opis
    ---|---|---
    --host | *Nazwa serwera* | Wartość nazwy serwera, która została użyta wcześniej podczas tworzenia serwera usługi Azure Database for MySQL. Przykładowy serwer to **myserver4demo.mysql.database.azure.com**. Użyj w pełni kwalifikowanej nazwy domeny (**\*.mysql.database.azure.com**), tak jak pokazano w przykładzie. Jeśli nie pamiętasz nazwy serwera, postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia. 
    --user | *Nazwa logowania administratora serwera* |Nazwa logowania administratora serwera, którą podano wcześniej podczas tworzenia serwera usługi Azure Database for MySQL. Jeśli nie pamiętasz nazwy użytkownika, postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia. Format to *username@servername*.
    -p | *Zaczekaj, aż zostanie wyświetlony monit* |Wtedy wpisz hasło podane podczas tworzenia serwera. Weź pod uwagę, że wpisywane znaki nie są wyświetlane w wierszu polecenia powłoki Bash. Po wprowadzeniu hasła wybierz klawisz **Enter**.

   Po nawiązaniu połączenia narzędzie mysql wyświetli monit `mysql>` umożliwiający wpisywanie poleceń. 

   Poniżej przedstawiono przykładowe dane wyjściowe polecenia mysql:

    ```bash
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Jeśli konfiguracja zapory nie umożliwia dostępu do adresu IP usługi Azure Cloud Shell, wystąpi następujący błąd:
    >
    > BŁĄD 2003 (28000): Klient o adresie IP 123.456.789.0 nie może uzyskać dostępu do serwera.
    >
    > Aby naprawić błąd, upewnij się, że konfiguracja serwera jest zgodna z krokami opisanymi w sekcji „Konfigurowanie reguły zapory na poziomie serwera” tego artykułu.

4. Aby upewnić się, że połączenie działa, wyświetl stan serwera, wpisując polecenie `status` w wierszu polecenia mysql>.

    ```sql
    status
    ```

   > [!TIP]
   > Aby zapoznać się z dodatkowymi poleceniami, zobacz [MySQL 5.7 Reference Manual - Chapter 4.5.1 (Podręcznik programu MySQL 5.7 — rozdział 4.5.1)](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Utwórz pustą bazę danych, wpisując następujące polecenie w wierszu polecenia **mysql>**:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    Wykonanie polecenia może potrwać kilka chwil. 

    Na serwerze usługi Azure Database for MySQL można utworzyć jedną lub wiele baz danych. Można wybrać opcję utworzenia jednej bazy danych na serwer w celu wykorzystania wszystkich zasobów. Można też utworzyć wiele baz danych, współdzielących zasoby. Nie istnieje limit dotyczący maksymalnej liczby baz danych, które można utworzyć, ale w przypadku wielu baz danych są współdzielone te same zasoby serwera. 

6. Wyświetl bazy danych, wpisując następujące polecenie w wierszu polecenia **mysql>**:

    ```sql
    SHOW DATABASES;
    ```

7.  Wpisz polecenie `\q`, a następnie wybierz klawisz **Enter**, aby zamknąć narzędzie mysql. Po wykonaniu tych czynności możesz zamknąć usługę Azure Cloud Shell.

Nawiązano połączenie z serwerem usługi Azure Database for MySQL i utworzono pustą bazę danych użytkownika. Przejdź do następnej sekcji, w której przedstawiono podobne ćwiczenie. Następne ćwiczenie polega na nawiązaniu połączenia z tym samym serwerem przy użyciu innego popularnego narzędzia — MySQL Workbench.

## <a name="connect-to-the-server-by-using-the-mysql-workbench-gui-tool"></a>Nawiązywanie połączenia z serwerem za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench
Aby nawiązać połączenie z serwerem za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench, wykonaj następujące czynności:

1.  Otwórz aplikację MySQL Workbench na komputerze klienckim. Aplikację MySQL Workbench możesz pobrać i zainstalować [ze strony pobierania aplikacji MySQL Workbench](https://dev.mysql.com/downloads/workbench/).

2. Utwórz nowe połączenie. Kliknij ikonę znaku plus (+) obok nagłówka **Połączenia MySQL**.

3. W oknie dialogowym **Konfigurowanie nowego połączenia** wprowadź informacje dotyczące połączenia serwera na karcie **Parametry**. Wartości zastępcze są wyświetlane jako przykład. Zamień nazwę hosta, nazwę użytkownika i hasło na własne wartości.

    ![Konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    |Ustawienie |Sugerowana wartość|Opis pola|
    |---|---|---|
     Nazwa połączenia | Połączenie demonstracyjne | Etykieta dla tego połączenia. |
    Metoda połączenia | Standardowa (TCP/IP) | Metoda Standardowa (TCP/IP) jest wystarczająca. |
    Nazwa hosta | *Nazwa serwera* | Wartość nazwy serwera, która została użyta podczas tworzenia serwera usługi Azure Database for MySQL. Przykładowy serwer to **myserver4demo.mysql.database.azure.com**. Użyj w pełni kwalifikowanej nazwy domeny (**\*.mysql.database.azure.com**), tak jak pokazano w przykładzie. Jeśli nie pamiętasz nazwy serwera, postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia.|
     Port | 3306 | Port używany podczas łączenia z serwerem usługi Azure Database for MySQL. |
    Nazwa użytkownika |  *Nazwa logowania administratora serwera* | Informacje dotyczące logowania administratora serwera, które podano wcześniej podczas tworzenia serwera usługi Azure Database for MySQL. Przykładowa nazwa użytkownika to **myadmin@myserver4demo**. Jeśli nie pamiętasz nazwy użytkownika, postępuj zgodnie z instrukcjami w poprzedniej sekcji, aby uzyskać informacje dotyczące połączenia. Format to *username@servername*.
    Hasło | *Twoje hasło* | Aby zapisać hasło, wybierz przycisk **Zapisz w magazynie**. |

4. Wybierz pozycję **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały skonfigurowane poprawnie. Następnie wybierz przycisk **OK**, aby zapisać połączenie. 

    > [!NOTE]
    > Na serwerze domyślnie jest wymuszane używanie protokołu SSL. W związku z tym do pomyślnego nawiązania połączenia jest wymagana dodatkowa konfiguracja. Aby uzyskać więcej informacji, zobacz [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL (Konfigurowanie łączności SSL w aplikacji w celu bezpiecznego nawiązywania połączeń z usługą Azure Database for MySQL)](./howto-configure-ssl.md). Aby wyłączyć protokół SSL na czas wykonywania instrukcji w tym przewodniku Szybki start, przejdź do witryny Azure Portal. Wybierz stronę Zabezpieczenia połączeń i kliknij przycisk przełączania **Wymuszaj połączenie SSL** w celu wyłączenia go.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Zasoby, które zostały utworzone w ramach tego przewodnika Szybki start, możesz wyczyścić na dwa sposoby. Możesz usunąć [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) zawierającą wszystkie zasoby w tej grupie. Jeśli chcesz zachować inne zasoby bez zmian, usuń tylko ten jeden zasób serwera.

> [!TIP]
> Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. Jeśli chcesz kontynuować pracę z przewodnikami Szybki start, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start. Jeśli nie planujesz kontynuowania pracy, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w ramach tego przewodnika Szybki start.
>

Aby usunąć całą grupę zasobów łącznie z nowo utworzonym serwerem, wykonaj następujące czynności:

1.  Znajdź grupę zasobów w witrynie Azure Portal. W menu po lewej stronie wybierz pozycję **Grupy zasobów**, a następnie wybierz nazwę grupy zasobów, takiej jak przykładowa grupa **myresourcegroup**.

2.  Na stronie grupy zasobów wybierz pozycję **Usuń**. Następnie wpisz nazwę grupy zasobów, takiej jak przykładowa grupa **myresourcegroup**, w polu tekstowym, aby potwierdzić usunięcie, i wybierz pozycję **Usuń**.

Aby usunąć tylko nowo utworzony serwer, wykonaj następujące czynności:

1.  Znajdź serwer w witrynie Azure Portal, jeśli nie jest jeszcze otwarty. W menu po lewej stronie w witrynie Azure Portal wybierz pozycję **Wszystkie zasoby**. Następnie wyszukaj utworzony serwer.

2.  Na stronie **Przegląd** wybierz pozycję **Usuń**. 

    ![Azure Database for MySQL — usuwanie serwera](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)

3.  Potwierdź nazwę serwera do usunięcia i wyświetl jego bazy danych, których dotyczy ta operacja. W polu tekstowym wpisz nazwę serwera, takiego jak przykładowy serwer **myserver4demo**. Wybierz pozycję **Usuń**.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Projektowanie pierwszej bazy danych usługi Azure Database for MySQL](./tutorial-design-database-using-portal.md)

