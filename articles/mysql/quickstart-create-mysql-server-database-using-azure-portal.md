---
title: "Szybki start: Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal | Microsoft Docs"
description: "Ta procedura artykułu możesz przy użyciu hello Azure tooquickly portalu tworzenie przykładowej bazy danych platformy Azure dla serwera MySQL w około pięciu minut."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal
Bazy danych platformy Azure dla programu MySQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności baz danych MySQL w chmurze hello. Ta opcja szybkiego startu pokazuje, jak toocreate Azure bazy danych dla serwera MySQL przy użyciu portalu Azure hello około pięciu minut. 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure
Otwórz przeglądarkę sieci web i przejdź toohello [portalu Microsoft Azure](https://portal.azure.com/). Wprowadź toosign Twoje poświadczenia w portalu toohello. Widok domyślny Hello jest pulpit nawigacyjny usługi.

## <a name="create-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Serwer usługi Azure Database for MySQL jest tworzony za pomocą zdefiniowanego zestawu [zasobów obliczeniowych i przestrzeni dyskowej](./concepts-compute-unit-and-storage.md). Serwer Hello jest tworzony w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).

Wykonaj te kroki toocreate Azure bazy danych serwera MySQL:

1. Kliknij przycisk hello **nowy** przycisk (+) na powitania lewym górnym rogu hello portalu Azure.

2. Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazy danych Azure dla programu MySQL** z hello **baz danych** strony. Możesz także wpisać **MySQL** w hello nowej strony wyszukiwania pole toofind hello usługi.
![Witryna Azure Portal — nowa — baza danych — MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Wypełnianie hello nowego serwera szczegóły formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:

    **Ustawienie** | **Sugerowana wartość** | **Opis pola** 
    ---|---|---
    Nazwa serwera | myserver4demo | Wybierz unikatową nazwę, która identyfikuje serwer usługi Azure Database for MySQL. Nazwa domeny Hello *mysql.database.azure.com* jest nazwą serwera dołączany toohello podanie tooconnect aplikacje do. Nazwa serwera Hello może zawierać tylko małe litery, cyfry i znaki łącznika (-) hello i musi zawierać od 3 do 63 znaków.
    Subskrypcja | Twoja subskrypcja | Witaj subskrypcji platformy Azure mają toouse serwera. Jeśli masz wiele subskrypcji, wybierz subskrypcję odpowiednie hello, w którym zasobów hello jest on rozliczany dla.
    Grupa zasobów | myresourcegroup | Możesz wprowadzić nową nazwę grupy zasobów lub użyć istniejącej nazwy z subskrypcji.
    Identyfikator logowania administratora serwera | myadmin | Podczas łączenia z serwerem toohello, należy własne toouse konta logowania. Nazwa logowania administracyjnego Hello nie może być "azure_superuser", "admin", "administrator", "root", "Gość" lub "public".
    Hasło | *Wartość wybrana przez użytkownika* | Utwórz nowe hasło dla konta administratora serwera hello. Musi zawierać od 8 znaków too128. Hasło musi zawierać znaki z trzech z następujących kategorii hello — wielkie litery, angielskiej wersji językowej małe litery, cyfry (0-9) i znaki inne niż alfanumeryczne (!, $, #, % itp.).
    Potwierdź hasło | *Wartość wybrana przez użytkownika*| Potwierdź hasło konta administratora hello.
    Lokalizacja | *Witaj region najbliższy tooyour użytkowników*| Wybierz lokalizację hello najbliższego tooyour użytkowników lub inne aplikacje platformy Azure.
    Wersja | *Wybierz hello najnowszej wersji.*| Wybierz hello najnowszej wersji, jeśli nie ma określonych wymagań.
    Warstwa cenowa | **Podstawowa**, **50 jednostek obliczeniowych** **50 GB** | Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych. Wybierz **warstwy Basic** karcie hello u góry hello. Kliknij przycisk hello lewego końca hello **obliczeniowe jednostki** suwaka tooadjust hello wartość toohello najmniej kwotę dostępne dla tego przewodnika Szybki Start. Kliknij przycisk **Ok** hello toosave wybór warstwy cenowej. Zobacz hello następującego zrzutu ekranu.
    Toodashboard numeru PIN | Zaznacz | Sprawdź hello **toodashboard numeru Pin** opcji tooallow łatwe monitorowanie serwera na stronie pulpitu nawigacyjnego front hello portalem Azure.

    > [!IMPORTANT]
    > Identyfikator logowania administratora serwera Hello i hasło określone w tym miejscu są wymagane toolog toohello Server i jego baz danych w dalszej części tego przewodnika Szybki Start. Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.
    > 

    ![Portal Azure — tworzenie MySQL, zapewniając hello wymaganych danych wejściowych z formularza](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Kliknij przycisk **Utwórz** tooprovision powitania serwera. Inicjowanie obsługi administracyjnej zajmuje kilka minut, zapasowej minut too20 maksymalna.
   
5.  Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor (ikonę dzwonka).

## <a name="configure-a-server-level-firewall-rule"></a>Konfigurowanie reguły zapory na poziomie serwera

Hello Azure bazy danych dla usługi MySQL tworzy zapory na poziomie serwera hello. Zapora uniemożliwi aplikacji zewnętrznych i narzędzia połączenie toohello serwera i żadnych baz danych na serwerze hello, chyba że tooopen hello zapory dla określonych adresów IP jest tworzona reguła zapory. 

1.  Zlokalizuj serwera po zakończeniu wdrażania hello. W razie potrzeby wyszukaj go. Na przykład kliknij pozycję **wszystkie zasoby** z menu po lewej stronie powitania i wpisz nazwę serwera hello (np. przykład Witaj *myserver4demo*) toosearch dla nowo utworzonego serwera. Kliknij nazwę serwera na liście wyników wyszukiwania hello. Witaj **omówienie** strony dla serwera zostanie otwarty i udostępnia opcje dla dalszej konfiguracji.

2. Na stronie powitania serwera wybierz **zabezpieczenia połączeń**.

3.  W obszarze hello **reguły zapory** nagłówek, kliknij w polu tekstowym puste hello w hello **Nazwa reguły** Tworzenie reguły zapory hello toobegin kolumny. 

    Dla tego przewodnika Szybki Start umożliwia zezwalanie na wszystkie adresy IP na powitania serwera według wypełnianie w polu tekstowym hello w każdej kolumnie hello następujące wartości:

    Nazwa reguły | Początkowy adres IP | Końcowy adres IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Na powitania górnym pasku narzędzi hello **zabezpieczenia połączeń** kliknij przycisk **zapisać**. Poczekaj chwilę, po czym powiadomień hello powiadomienia pokazujący, że aktualizacja zabezpieczeń połączenia zakończyło się pomyślnie przed kontynuowaniem.

    > [!NOTE]
    > TooAzure połączenia bazy danych dla programu MySQL komunikują się za pośrednictwem portu 3306. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 3306 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie będzie możliwe tooconnect tooyour serwera, chyba że dział IT otwiera port 3306.
    > 

## <a name="get-hello-connection-information"></a>Pobierz informacje o połączeniu hello
tooconnect tooyour serwera bazy danych, należy tooremember hello pełny serwer administrator i nazwę poświadczenia logowania. Może mieć zauważyć tych wartości w artykule szybkiego startu hello. W przypadku, gdy nie, łatwo informacje można znaleźć serwera hello nazwy i logowania z serwera hello **omówienie** strony lub hello **właściwości** strony w hello portalu Azure.

1. Otwórz stronę **Przegląd** serwera. Zanotuj hello **nazwy serwera** i **nazwę logowania administratora serwera**. 
    Umieść kursor nad każdego pola i hello kopiowania ikona jest wyświetlana po prawej toohello hello tekstu. Kliknij ikonę kopiowania hello jako wartości hello toocopy potrzebne.

    W tym przykładzie nazwa serwera hello jest *myserver4demo.mysql.database.azure.com*, i jest identyfikator logowania administratora serwera hello  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Połącz przy użyciu narzędzia wiersza polecenia mysql tooMySQL
Istnieje wiele aplikacji można użyć tooyour tooconnect Azure bazy danych dla serwera MySQL. Użyjmy najpierw hello [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) wiersza polecenia narzędzia tooillustrate jak tooconnect toohello serwera.  Korzystanie z przeglądarki internetowej i hello powłoki chmury Azure zgodnie z opisem w tym miejscu bez hello wymagają tooinstall żadnego dodatkowego oprogramowania. Jeśli masz narzędzie mysql hello zainstalowane lokalnie na własnym komputerze mogą łączyć się z nim również.

1. Uruchamianie hello powłoki chmury Azure za pomocą ikony terminali hello (> _) na powitania górnego prawego hello strony sieci web portalu Azure.

2. Witaj powłoki chmury Azure otwiera w przeglądarce, umożliwiając poleceń powłoki bash tootype.

    ![Wiersz polecenia — przykładowy wiersz polecenia mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. W wierszu polecenia powłoki chmury hello połączyć tooyour Azure bazy danych dla serwera MySQL, wpisując hello mysql polecenie w wierszu hello zielony.

    zgodny z formatem Hello jest używane tooconnect tooan Azure bazy danych MySQL serwera za pomocą narzędzia mysql hello:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Na przykład następujące polecenie hello łączy serwer przykład tooour:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    Parametr narzędzia mysql |Sugerowana wartość|Opis
    ---|---|---
    --host | *nazwa serwera* | Określ wartość hello nazwy serwera, który został użyty podczas hello Azure bazy danych dla programu MySQL wcześniej utworzony. Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj hello pełną nazwę domeny (\*. mysql.database.azure.com) jak pokazano w przykładzie hello. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz nazwę serwera. 
    --user | *nazwa logowania administratora serwera* |Wpisz powitania serwera admin logowania użytkownika dostarczana, gdy dla programu MySQL utworzony wcześniej hello bazy danych Azure. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz hello nazwy użytkownika.  Hello format jest  *username@servername* .
    --password | *Zaczekaj, aż zostanie wyświetlony monit* | Zostanie wyświetlony monit zbyt "Wprowadź hasło" po wprowadź polecenie hello. Po wyświetleniu monitu wpisz hello samo hasło podane podczas tworzenia powitania serwera.  Uwaga hello wpisane znaki nie są pokazywane na powitania bash Monituj podczas wpisywania hasła. Naciśnij klawisz enter po wpisana wszystkich tooauthenticate znaków hello i połącz.

   Po nawiązaniu połączenia hello mysql narzędzie wyświetla `mysql>` monitu dla Ciebie tootype poleceń. 

    Przykład danych wyjściowych polecenia mysql:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Jeśli Zapora hello nie jest skonfigurowany adres IP hello tooallow hello powłoki chmury Azure, hello wystąpił następujący błąd:
    >
    > Błąd 2003 (28000): Klient o adresie IP 123.456.789.0 tooaccess powitania serwera nie jest dozwolone.
    >
    > tooresolve hello błąd, upewnij się, że powitania serwera konfiguracji dopasowań hello etapami hello *skonfigurować regułę zapory poziomu serwera* hello artykułu.

4. Widok serwera stanu tooensure hello połączenia będzie działać. Typ `status` na powitania mysql > monit, gdy jest on podłączony.
    ```sql
    status
    ```

   > [!TIP]
   > Aby zapoznać się z dodatkowymi poleceniami, zobacz [MySQL 5.7 Reference Manual - Chapter 4.5.1 (Podręcznik programu MySQL 5.7 — Rozdział 4.5.1)](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Utwórz pustą bazę danych na hello mysql > monitu, wpisując następujące polecenie hello:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    polecenie Hello może potrwać kilka minut toocomplete. 

    Na serwerze usługi Azure Database for MySQL można utworzyć jedną lub wiele baz danych. Opt toocreate pojedynczej bazy danych na serwerze tooutilize wszystkie zasoby hello lub utworzyć wiele baz danych tooshare hello zasobów. Nie jest nie toohello Ogranicz liczbę baz danych, które mogą zostać utworzone, ale wielu baz danych udostępnianie hello te same zasoby serwera. 

6. Listy baz danych hello na powitania mysql > monitu, wpisując następujące polecenie hello:

    ```sql
    SHOW DATABASES;
    ```

7.  Typ `\q` , a następnie naciśnij klawisz ENTER tooquit hello mysql narzędzia. Po wykonaniu tych czynności możesz zamknąć hello powłoki chmury Azure.

Teraz po połączeniu toohello bazy danych platformy Azure dla programu MySQL i utworzyć bazę danych użytkownika. Kontynuować toohello następnej sekcji toorepeat podobne toohello tooconnect wykonywania tego samego serwera przy użyciu innego typowe narzędzia MySQL Workbench.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Połącz przy użyciu narzędzia Workbench MySQL graficznego interfejsu użytkownika hello serwer toohello
za pomocą hello graficznego interfejsu użytkownika narzędzia MySQL Workbench serwer MySQL tooAzure tooconnect:

1.  Uruchom program hello MySQL Workbench aplikacji na komputerze klienckim. Aplikację MySQL Workbench możesz pobrać i zainstalować [stąd](https://dev.mysql.com/downloads/workbench/).

2.  W **instalacji nowego połączenia** okna dialogowego wprowadź hello następujących informacji **parametry** karty:

    ![konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Ustawienie** | **Sugerowana wartość** | **Opis pola** |
    |---|---|---|
    |   Nazwa połączenia | Połączenie demonstracyjne | Podaj etykietę dla tego połączenia. |
    | Metoda połączenia | Standardowa (TCP/IP) | Metoda Standardowa (TCP/IP) jest wystarczająca. |
    | Nazwa hosta | *nazwa serwera* | Określ wartość hello nazwy serwera, który został użyty podczas hello Azure bazy danych dla programu MySQL wcześniej utworzony. Pokazany przykładowy serwer to myserver4demo.mysql.database.azure.com. Użyj hello pełną nazwę domeny (\*. mysql.database.azure.com) jak pokazano w przykładzie hello. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz nazwę serwera.  |
    | Port | 3306 | Należy zawsze używać portu 3306 podczas łączenia tooAzure bazy danych dla programu MySQL. |
    | Nazwa użytkownika |  *nazwa logowania administratora serwera* | Wpisz powitania serwera admin logowania użytkownika dostarczana, gdy dla programu MySQL utworzony wcześniej hello bazy danych Azure. Przykładowa nazwa użytkownika to myadmin@myserver4demo. Wykonaj kroki hello hello poprzedniej sekcji tooget hello informacje dotyczące połączenia, jeśli nie pamiętasz hello nazwy użytkownika. Hello format jest  *username@servername* .
    | Hasło | Twoje hasło | Kliknij przycisk przechowywania w magazynie... przycisk toosave hello hasła. |

    Kliknij przycisk **Testuj połączenie** tootest, jeśli wszystkie parametry są poprawnie skonfigurowane. Kliknij przycisk OK toosave hello połączenie. 

    > [!NOTE]
    > Protokół SSL jest wymuszana, domyślnie na serwerze i wymaga dodatkowej konfiguracji w kolejności tooconnect pomyślnie. Zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md).  Jeśli chcesz toodisable protokołu SSL dla tego przewodnika Szybki Start, odwiedź hello portalu Azure i przycisk hello połączenia zabezpieczeń strony toodisable hello Wymuszanie protokołu SSL połączenia przełącznika.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Oczyszczanie zasobów hello utworzony w szybkiego startu hello przez usunięcie hello [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md), która obejmuje wszystkie zasoby hello w grupie zasobów hello lub usuwając hello jeden serwer zasobów, jeśli chcesz tookeep hello inne zasoby bez zmian.

> [!TIP]
> Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. Jeśli planujesz toocontinue toowork kolejne Przewodniki Szybki Start, czy nie Oczyszczanie hello zasoby utworzone w tym Szybki Start. Jeśli nie planujesz toocontinue, użyj powitania po toodelete kroki wszystkie zasoby utworzone przez tego szybkiego startu w portalu Azure hello.
>

toodelete hello całej grupy zasobów serwera hello nowo utworzone w tym:
1.  Znajdź grupie zasobów w hello portalu Azure. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello grupy zasobów, takich jak naszym przykładzie **myresourcegroup**.
2.  Na stronie grupy zasobów kliknij polecenie **Usuń**. Następnie typu hello Nazwa grupy zasobów, takich jak naszym przykładzie **myresourcegroup**, w hello usunięcia tooconfirm pola tekstowego, a następnie kliknij przycisk **usunąć**.

Lub zamiast tego toodelete hello nowo utworzonego serwera:
1.  Znajdź serwer w hello portalu Azure, jeśli nie masz otwarty. Z menu po lewej stronie powitania w portalu Azure, kliknij przycisk **wszystkie zasoby**, a następnie wyszukaj powitania serwera został utworzony.
2.  Na powitania **omówienie** kliknij przycisk hello **usunąć** przycisk w górnym okienku hello.
![Azure Database for MySQL — usuwanie serwera](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Upewnij się, nazwy serwera hello toodelete, a następnie Pokaż hello baz danych, których dotyczy problem. Wpisz nazwę serwera w polu tekstowym hello, takich jak naszym przykładzie **myserver4demo**, a następnie kliknij przycisk **usunąć**.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Projektowanie pierwszej bazy danych usługi Azure Database for MySQL](./tutorial-design-database-using-portal.md)

