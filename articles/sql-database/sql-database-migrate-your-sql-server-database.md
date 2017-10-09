---
title: aaaMigrate bazy danych programu SQL Server tooAzure bazy danych SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się toomigrate tooAzure bazy danych programu SQL Server bazy danych SQL."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Migrowanie tooAzure bazy danych programu SQL Server bazy danych SQL

Przenoszenie programu SQL Server tooAzure bazy danych SQL Database jest procesem trzech części — najpierw przygotować, a następnie wyeksportować, a następnie zaimportuj hello bazy danych. Z tego samouczka dowiesz się, aby:

> [!div class="checklist"]
> * Przygotowanie bazy danych w programie SQL Server do migracji tooAzure bazy danych SQL przy użyciu hello [Asystenta migracji danych](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Witaj bazy danych tooa pliku BACPAC pliku eksportu
> * Importowanie pliku pliku BACPAC hello do bazy danych SQL Azure

Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

- Hello zainstalowana najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). Instalowanie programu SSMS instaluje najnowszą wersję hello SQLPackage, narzędzie wiersza polecenia, które mogą być używane tooautomate szereg zadań związanych z projektowaniem bazy danych. 
- Zainstalowane hello [Asystenta migracji danych](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Zidentyfikowano i mieć toomigrate bazy danych tooa dostępu. Samouczku hello [programu SQL Server 2008 R2 bazy danych AdventureWorks OLTP](https://msftdbprodsamples.codeplex.com/releases/view/59211) w wystąpieniu programu SQL Server 2008 R2 lub nowszej, ale możesz użyć dowolnej bazy danych wybrane. problemy ze zgodnością toofix, użyj [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Przygotowanie do migracji

Wszystko jest gotowe tooprepare do migracji. Wykonaj te kroki hello toouse  **[Asystenta migracji danych](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello gotowości bazy danych, aby tooAzure migracji bazy danych SQL.

1. Otwórz hello **Asystenta migracji danych**. Czy planujesz toomigrate, nie trzeba tooinstall hello na powitania komputera hostującego wystąpienie programu SQL Server, możesz uruchomić DMA na dowolnym komputerze z łączności toohello wystąpienia zawierającego hello bazy danych SQL Server.

     ![Otwórz Asystenta migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. W menu po lewej stronie powitania kliknij **+ nowy** toocreate **oceny** projektu. Wypełnij formularz hello z **Nazwa projektu** (wszystkie pozostałe wartości należy pozostawić wartości domyślne) i kliknij przycisk **Utwórz**. Witaj **opcje** zostanie otwarta strona.

     ![Nowy projekt Asystenta migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Na powitania **opcje** kliknij przycisk **dalej**. Witaj **Wybierz źródła** zostanie otwarta strona.

     ![nowe opcje migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Na powitania **Wybierz źródła** strony, wprowadź nazwę hello zawierających server hello planujesz toomigrate wystąpienia programu SQL Server. Jeśli to konieczne, zmian hello innych wartości na tej stronie. Kliknij przycisk **Połącz**.

     ![nowe źródła wybierz migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. W hello **Dodaj źródła** część hello **Wybierz źródła** zaznacz pola wyboru hello toobe baz danych hello sprawdzane pod kątem zgodności. Kliknij pozycję **Dodaj**.

     ![nowe źródła wybierz migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Kliknij przycisk **Start oceny**.

     ![Nowa ocena rozpoczęcia migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Po ukończeniu oceny hello Pierwsze spojrzenie toosee, jeśli baza danych hello jest wystarczająco zgodne toomigrate. Poszukaj hello zaznaczone zielone koło.

     ![nowe dane migracji wyników oceny zgodne](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Przejrzyj wyniki hello. Witaj **parzystość funkcji programu SQL Server** tooreview wyniki domyślna hello są wyświetlane wyniki. W szczególności Przejrzyj hello informacje nieobsługiwane i częściowo obsługiwane funkcje i hello podane informacje o zalecanych akcji. 

     ![nowe parzystości oceny migracji danych](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Przejrzyj hello **problemy ze zgodnością** , klikając tę opcję w lewym górnym rogu hello. W szczególności Przegląd hello informacji na temat migracji blockers, zmiany zachowania i przestarzałe funkcje dla każdego poziomu zgodności. W przypadku bazy danych hello AdventureWorks2008R2 Przejrzyj zmiany hello wyszukiwania pełnotekstowego tooFull od programu SQL Server 2008 i hello zmiany wprowadzone tooSERVERPROPERTY('LCID') od wersji programu SQL Server 2000. Aby uzyskać więcej informacji na temat tych zmian podano łącza, aby uzyskać więcej informacji. Wiele opcje wyszukiwania i ustawienia wyszukiwania pełnotekstowego zostały zmienione. 

   > [!IMPORTANT] 
   > Po przeprowadzeniu migracji tooAzure Twojej bazy danych SQL Database, można wybrać bazę danych hello toooperate na jego bieżący poziom zgodności (poziom 100 dla bazy danych AdventureWorks2008R2 hello) lub na wyższym poziomie. Aby uzyskać więcej informacji na powitania wpływ i opcje dla działania bazy danych na poziomie zgodności określonego, zobacz [zmienić poziom zgodności bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zobacz też [ALTER DATABASE CONFIGURATION zakres](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) informacji o dodatkowych ustawień na poziomie bazy danych powiązanych toocompatibility poziomów.
   >

10. Opcjonalnie kliknij **Eksportuj raport** toosave hello raportu w formacie JSON.
11. Zamknij hello Asystenta migracji danych.

## <a name="export-toobacpac-file"></a>Eksportuj plik tooBACPAC 

Plik pliku BACPAC to plik ZIP z rozszerzeniem pliku BACPAC zawierające hello metadane i dane z bazy danych programu SQL Server. Plik pliku BACPAC mogą być przechowywane w magazynie obiektów blob platformy Azure lub w magazynie lokalnym archiwizowania lub migracja — takie jak z programu SQL Server tooAzure bazy danych SQL. Dla spójna transakcyjnie toobe eksportu, pamiętaj, że nie zapis działanie ma miejsce podczas eksportowania hello.

Wykonaj te kroki toouse hello SQLPackage narzędzia wiersza polecenia tooexport hello AdventureWorks2008R2 toolocal przestrzeń dyskowa bazy danych.

1. Otwórz wiersz polecenia systemu Windows i zmienić folder tooa katalogu, w którym zostały hello **130** wersji SQLPackage — takie jak **\Microsoft SQL Server\130\DAC\bin C:\Program Files (x86)**.

2. Wykonaj następujące polecenia SQLPackage na powitania wiersza polecenia tooexport hello hello **AdventureWorks2008R2** bazy danych z **localhost** za**AdventureWorks2008R2.bacpac**. Zmienić dowolne z tych wartości jako odpowiednie tooyour środowiska.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage eksportu](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Po zakończeniu wykonywania hello hello wygenerowany pliku BACPAC plik jest przechowywany w katalogu hello, w którym znajduje się sqlpackage hello pliku wykonywalnego. W tym przykładzie \Microsoft SQL Server\130\DAC\bin C:\Program Files (x86). 

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/). Logowania z hello komputera, z którego uruchomiono narzędzie wiersza polecenia SQLPackage hello ułatwia tworzenie hello hello reguły zapory w kroku 5.

## <a name="create-a-sql-server-logical-server"></a>Tworzenie serwera logicznego SQL

A [serwera logicznego SQL server](sql-database-features.md) działa jako centralny punkt administracyjny dla wielu baz danych. Wykonaj następujące kroki toocreate programu SQL server serwera logicznego toocontain hello migracji bazy danych firmy Adventure Works OLTP programu SQL Server. 

1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

2. Typ **programu sql server** okno wyszukiwania hello na powitania **nowy** i wybrać opcję **bazy danych SQL (serwer logiczny)** z hello filtrowane listy.

    ![wybieranie serwera logicznego](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Na powitania **wszystko** kliknij przycisk **programu SQL server (serwer logiczny)** , a następnie kliknij przycisk **Utwórz** na powitania **programu SQL Server (serwer logiczny)** strony .

    ![Tworzenie serwera logicznego](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Wypełnij hello programu SQL server (serwer logiczny) formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:     

   | Ustawienie       | Sugerowana wartość | Opis | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nazwa serwera** | Wprowadź wszelkie globalnie unikatowa nazwa | Prawidłowe nazwy serwera opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). | 
   | **Identyfikator logowania administratora serwera** | Wprowadź wszelkie prawidłową nazwę. | Prawidłowe nazwy identyfikatorów logowania opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych). |
   | **Hasło** | Wprowadź wszelkie prawidłowe hasło. | Hasło musi mieć co najmniej 8 znaków i musi zawierać znaki z trzech z następujących kategorii hello: wielkich liter, małych liter, cyfr i znaków innych niż alfanumeryczne. |
   | **Subskrypcja** | Wybierz subskrypcję | Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions). |
   | **Grupa zasobów** | Wybierz istniejącą grupę zasobów lub Utwórz nową grupę, takich jak **myResourceGroup** |  Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). |
   | **Lokalizacja** | Wprowadź żadnej prawidłowej lokalizacji hello nowego serwera | Aby uzyskać informacje na temat regionów, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/). |

   ![Tworzenie serwera logicznego ukończone formularza](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Kliknij przycisk **Utwórz** serwera logicznego hello tooprovision. Aprowizacja zajmuje kilka minut. 

> [!IMPORTANT]
> Należy pamiętać, swoją nazwę serwera, nazwa logowania administratora serwera i hasło. Te wartości muszą się w dalszej części tego samouczka.
>

## <a name="create-a-server-level-firewall-rule"></a>Tworzenie reguły zapory na poziomie serwera

Tworzy Hello usługi baza danych SQL [zapory na poziomie serwera hello](sql-database-firewall-configure.md) uniemożliwiający połączenie serwera toohello lub żadnych baz danych na serwerze hello, chyba że tooopen hello tworzona jest reguła zapory aplikacji zewnętrznych i narzędzia zapory dla określonych adresów IP. Wykonaj te kroki toocreate regułę zapory poziomu serwera bazy danych SQL dla adresu IP hello hello komputera, z którego uruchomiono narzędzie wiersza polecenia SQLPackage hello. Dzięki temu SQLPackage tooconnect toohello SQL serverDatabase serwera logicznego przez zaporę bazy danych SQL Azure hello. 

1. Kliknij przycisk **wszystkie zasoby** z menu po lewej stronie powitania i kliknij przycisk nowego serwera na powitania **wszystkie zasoby** strony. Strona omówienia powitania serwera otwiera i udostępnia opcje dla dalszego konfiguracji.

     ![Omówienie serwera logicznego](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Kliknij przycisk **zapory** w menu po lewej stronie powitania w obszarze **ustawienia** na stronie Przegląd hello. Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server. 

3. Kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi tooadd hello adres IP komputera hello obecnie używasz a następnie kliknij przycisk **zapisać**. Dla tego adresu IP jest tworzona reguła zapory poziomu serwera.

     ![ustawianie reguły zapory serwera](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Kliknij przycisk **OK**.

Teraz możesz połączyć tooall baz danych, na tym serwerze za pomocą programu SQL Server Management Studio lub inne narzędzie do dowolnego z tego adresu IP przy użyciu konta administratora serwera hello utworzone wcześniej.

> [!NOTE]
> Usługa SQL Database nawiązuje komunikację na porcie 1433. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie można połączyć tooyour serwera bazy danych SQL Azure, chyba że dział IT otwiera port 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Importowanie pliku BACPAC tooAzure pliku bazy danych SQL 

udostępnia najnowsze wersje Hello hello SQLPackage narzędzia wiersza polecenia obsługi tworzenia bazy danych Azure SQL o określonej [warstwę i poziom wydajności usługi](sql-database-service-tiers.md). Aby uzyskać najlepszą wydajność podczas importowania wybierz poziom wydajności i warstwę usługi wysokiej i następnie Skaluj w dół po zaimportowaniu Jeśli hello usługi warstwę i poziom wydajności jest większa niż należy natychmiast.

Wykonaj te kroki Użyj hello SQLPackage narzędzia wiersza polecenia tooimport hello AdventureWorks2008R2 bazy danych tooAzure bazy danych SQL. Podczas korzystania z programu SQL Server Management Studio, dla tego zadania, SQLPackage jest metoda hello preferowane dla większości środowisk produkcyjnych maksymalną elastyczność i najlepszą wydajność. Zobacz [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Wykonaj następujące polecenia SQLPackage na powitania wiersza polecenia tooimport hello hello **AdventureWorks2008R2** bazy danych z serwera logicznego SQL server magazynu lokalnego toohello tego możesz tooa wcześniej utworzonej nowej bazy danych, usługi warstwy **Premium**, a celem usługi **P6**. Zastąp wartości hello w nawiasach ostrych odpowiednie wartości dla serwera logicznego SQL server i określ nazwę nowej bazy danych hello (również Zamień hello nawiasy). Możesz również toochange hello wartości wersji bazy danych i usługi objectgive jako odpowiednie tooyour środowiska. W celu hello tego samouczka hello migrowanych baza danych jest nazywana **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![Importuj sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Serwer logiczny serwer SQL nasłuchuje na porcie 1433. Jeśli próbujesz tooconnect tooa logicznego serwera programu SQL server z w obrębie firmowej zapory, ten port musi być otwarty w hello firmowej zapory dla toosuccessfully można połączyć z usługą.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Połącz przy użyciu programu SQL Server Management Studio (SSMS)

Użyj programu SQL Server Management Studio tooestablish serwer bazy danych SQL Azure tooyour połączenia i zaktualizowane bazy danych o nazwie **myMigratedDatabase** w tym samouczku. Jeśli używasz programu SQL Server Management Studio na innym komputerze, z którego uruchomiono SQLPackage, należy utworzyć regułę zapory dla tego komputera przy użyciu kroków hello w poprzedniej procedurze hello.

1. Otwórz program SQL Server Management Studio.

2. W hello **połączyć tooServer** okna dialogowego wprowadź hello następujących informacji:
   - **Typ serwera**: określ aparat bazy danych
   - **Nazwa serwera**: Wprowadź nazwę FQDN serwera, na przykład **mynewserver20170403.database.windows.net**
   - **Uwierzytelnianie**: określ uwierzytelnianie programu SQL Server
   - **Logowanie**: wprowadź nazwę konta administratora serwera
   - **Hasło**: Wprowadź hello hasło dla konta administratora serwera
 
    ![Uzyskuj dostęp do narzędzia ssms](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Kliknij przycisk **Połącz**. zostanie otwarte okno Eksploratora obiektów Hello. 

4. W Eksploratorze obiektów rozwiń **baz danych** , a następnie rozwiń węzeł **myMigratedDatabase** tooview hello obiektów hello przykładowej bazy danych.

## <a name="change-database-properties"></a>Zmień właściwości bazy danych

Można zmienić warstwy usług hello, poziom wydajności i poziom zgodności przy użyciu programu SQL Server Management Studio. Podczas fazy importowania hello zaleca się importowania tooa wyższej wydajności warstwy bazy danych dla najlepszą wydajność, ale skalowanie w dół zakończone importu hello pieniędzy toosave dopóki nie są gotowe tooactively Użyj hello importowanych bazy danych. Zmiana poziomu zgodności hello może spowodować lepszą wydajność i dostępu toohello najnowsze możliwości hello usługi baza danych SQL Azure. Podczas migracji starszej bazy danych, jej poziom zgodności bazy danych jest zachowywana na poziomie hello najniższa obsługiwana, który jest zgodny z bazą danych hello importowane. Aby uzyskać więcej informacji, zobacz [zwiększona wydajność zapytań ze zgodnością 130 poziom w bazie danych SQL Azure](sql-database-compatibility-level-query-performance-130.md).

1. W Eksploratorze obiektów kliknij prawym przyciskiem myszy **myMigratedDatabase** i kliknij przycisk **nowe zapytanie**. Zostanie otwarte okno kwerendy tooyour połączenia bazy danych.

2. Wykonanie powitania po warstwy usług hello tooset polecenia zbyt**standardowe** i hello zbyt poziomie wydajności**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![Zmiana warstwy usług](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Wykonanie powitania po poziom zgodności bazy danych polecenie toochange hello zbyt**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![Zmień poziom zgodności](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Następne kroki 
W tym samouczku przygotowany, wyeksportowane i zaimportowane bazy danych. Znasz już do:

> [!div class="checklist"]
> * Przygotowanie bazy danych w programie SQL Server do migracji tooAzure bazy danych SQL
> * Witaj bazy danych tooa pliku BACPAC pliku eksportu
> * Importowanie pliku pliku BACPAC hello do bazy danych SQL Azure

Jak przejść dalej toolearn samouczka toohello toosecure bazy danych.

> [!div class="nextstepaction"]
> [Zabezpieczenia bazy danych Azure SQL](sql-database-security-tutorial.md).


