---
title: "aaaDesign pierwszą bazę danych Azure SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się toodesign pierwszą bazę danych Azure SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>Projektowanie pierwszą bazę danych Azure SQL

Baza danych SQL Azure to relacyjnej bazy danych — jako a usługa (DBaaS) w hello Microsoft Cloud ("Azure"). Z tego samouczka, dowiesz się, jak toouse hello portalu Azure i [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) do: 

> [!div class="checklist"]
> * Utwórz bazę danych w hello portalu Azure
> * Skonfiguruj regułę zapory poziomu serwera w hello portalu Azure
> * Połączenie bazy danych toohello z SSMS
> * Tworzenie tabel z SSMS
> * Danych ładowania zbiorczego, za pomocą narzędzia BCP
> * Zapytanie danych z narzędzia SSMS
> * Przywróć poprzednie tooa bazy danych hello [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore) w hello portalu Azure

Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka, upewnij się, że została zainstalowana:
- Witaj najnowsza wersja [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- Witaj najnowsza wersja [BCP i SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database"></a>Utwórz pustą bazę danych SQL

Baza danych Azure SQL jest tworzona ze zdefiniowanym zestawem [zasobów obliczeniowych i przechowywania](sql-database-service-tiers.md). Witaj baza danych została utworzona w ramach [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) i [serwera logicznego bazy danych SQL Azure](sql-database-features.md). 

Wykonaj te kroki toocreate pustej bazy danych SQL. 

1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

2. Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazy danych SQL** z hello **baz danych** strony. 

   ![Tworzenie bazy danych puste](./media/sql-database-design-first-database/create-empty-database.png)

3. Wypełnianie hello bazy danych SQL formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:   

   | Ustawienie       | Sugerowana wartość | Opis | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nazwa bazy danych** | mySampleDatabase | Prawidłowe nazwy baz danych opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych). | 
   | **Subskrypcja** | Twoja subskrypcja  | Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions). |
   | **Grupa zasobów** | myResourceGroup | Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). |
   | **Wybierz źródło** | Pusta baza danych | Określa, czy można utworzyć pustej bazy danych. |

4. Kliknij przycisk **serwera** toocreate i skonfiguruj nowy serwer dla nowej bazy danych. Wypełnianie hello **nowy formularz serwera** z hello następujących informacji: 

   | Ustawienie       | Sugerowana wartość | Opis | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nazwa serwera** | Dowolna nazwa unikatowa w skali globalnej | Prawidłowe nazwy serwera opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). | 
   | **Identyfikator logowania administratora serwera** | Dowolna prawidłowa nazwa | Prawidłowe nazwy identyfikatorów logowania opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).|
   | **Hasło** | Dowolne prawidłowe hasło | Hasło musi mieć co najmniej 8 znaków i musi zawierać znaki z trzech z następujących kategorii hello: wielkich liter, małych liter, cyfr i znaków innych niż alfanumeryczne. |
   | **Lokalizacja** | Dowolna prawidłowa lokalizacja | Aby uzyskać informacje na temat regionów, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/). |

   ![tworzenie serwera bazy danych](./media//sql-database-design-first-database/create-database-server.png)

5. Kliknij pozycję **Wybierz**.

6. Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych. W tym samouczku, wybierz **20 jednostek Dtu** i **250** GB miejsca do magazynowania.

   ![tworzenie bazy danych s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Kliknij przycisk **Zastosuj**.  

8. Wybierz **sortowania** dla hello pustej bazy danych (w tym samouczku, wartość domyślna używana hello). Aby uzyskać więcej informacji na temat sortowań zobacz [sortowania](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Kliknij przycisk **Utwórz** tooprovision hello w bazie danych. Inicjowanie obsługi administracyjnej ma o toocomplete minutę i pół. 

10. Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor.

   ![powiadomienie](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Tworzenie reguły zapory na poziomie serwera

Hello usługi baza danych SQL tworzy zapory na poziomie hello server — które uniemożliwiają połączenie serwera toohello lub żadnych baz danych na serwerze hello, chyba że tooopen hello zapory dla określonych adresów IP jest tworzona reguła zapory aplikacji zewnętrznych i narzędzia. Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](sql-database-firewall-configure.md) dla adresów IP klienta i włączyć łączność zewnętrzną przez zaporę bazy danych SQL hello tylko adresu IP. 

> [!NOTE]
> Usługa SQL Database nawiązuje komunikację na porcie 1433. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie można połączyć tooyour serwera bazy danych SQL Azure, chyba że dział IT otwiera port 1433.
>

1. Po zakończeniu wdrażania hello, kliknij przycisk **baz danych SQL** z menu po lewej stronie powitania, a następnie kliknij przycisk **mySampleDatabase** na powitania **baz danych SQL** strony. Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji. Skopiuj tę w pełni kwalifikowaną nazwę serwera do użycia w przyszłości.

   > [!IMPORTANT]
   > Należy to pełna nazwa tooconnect tooyour serwera i jego baz danych w kolejnych Szybki Start.
   > 

   ![nazwa serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello. Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server. 

   ![reguła zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi tooadd IP bieżący adres tooa nowej reguły zapory. Reguła zapory może otworzyć port 1433 dla pojedynczego adresu IP lub zakresu adresów IP.

4. Kliknij pozycję **Zapisz**. Dla bieżącego adresu IP otwierania portu 1433 na serwerze logicznym hello tworzona jest reguła zapory poziomu serwera.

   ![ustawianie reguły zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Kliknij przycisk **OK** , a następnie zamknij hello **ustawienia zapory** strony.

Teraz można podłączyć toohello bazy danych programu SQL server i bazy danych przy użyciu programu SQL Server Management Studio lub inne narzędzie do dowolnego z tego adresu IP przy użyciu konta administratora serwera hello utworzone wcześniej.

> [!IMPORTANT]
> Domyślnie dostęp za pośrednictwem zapory bazy danych SQL hello jest włączona dla wszystkich usług platformy Azure. Kliknij przycisk **OFF** na toodisable tej strony dla wszystkich usług platformy Azure.

## <a name="sql-server-connection-information"></a>Informacje o połączeniu z serwerem SQL

Pobierz hello pełni kwalifikowaną nazwę serwera dla serwera bazy danych SQL Azure w hello portalu Azure. Możesz użyć hello pełną nazwę tooconnect tooyour serwera przy użyciu programu SQL Server Management Studio.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 
3. W hello **Essentials** okienka w hello strony portalu systemu Azure dla bazy danych, Znajdź, a następnie skopiuj hello **nazwy serwera**.

   ![informacje o połączeniu](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>Połączenie bazy danych toohello z SSMS

Użyj [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish serwer bazy danych SQL Azure tooyour połączenia.

1. Otwórz program SQL Server Management Studio.

2. W hello **połączyć tooServer** okna dialogowego wprowadź hello następujących informacji:

   | Ustawienie       | Sugerowana wartość | Opis | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Typ serwera | Aparat bazy danych | Ta wartość jest wymagana |
   | Nazwa serwera | Nazwa FQDN serwera Hello | Witaj nazwa powinna być podobny do następującego: **mynewserver20170313.database.windows.net**. |
   | Authentication | Uwierzytelnianie programu SQL Server | Uwierzytelnianie programu SQL jest typ uwierzytelniania tylko hello ma został skonfigurowany w tym samouczku. |
   | Login | konto administratora powitania serwera | To konto hello określone podczas tworzenia powitania serwera. |
   | Hasło | Witaj hasło do konta administratora serwera | Jest to hasło hello określone podczas tworzenia powitania serwera. |

   ![Połącz tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. Kliknij przycisk **opcje** w hello **połączyć tooserver** okno dialogowe. W hello **połączyć toodatabase** wprowadź **mySampleDatabase** tooconnect toothis w bazie danych.

   ![Połącz toodb na serwerze](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Kliknij przycisk **Połącz**. Okno Eksploratora obiektów Hello zostanie otwarty w programie SSMS. 

5. W Eksploratorze obiektów rozwiń **baz danych** , a następnie rozwiń węzeł **mySampleDatabase** tooview hello obiektów hello przykładowej bazy danych.

   ![Obiekty bazy danych](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Tworzenie tabel w bazie danych hello 

Tworzenie schematu bazy danych z czterech tabel, które system zarządzania uczniów uczelni przy użyciu modelu [języka Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):

- Osoby
- Plan
- Dla użytkowników domowych
- System zarządzania uczniów uczelni modelu karty kredytowej

Witaj poniższym diagramie przedstawiono sposób następujące tabele są powiązane tooeach innych. Niektóre z tych tabel odwoływać się do kolumn w innych tabelach. Na przykład hello uczniów tabeli odwołuje hello **PersonId** kolumny hello **osoby** tabeli. Diagram toounderstand hello badań, jak hello tabele w tym samouczku są powiązane tooone innego. Dla omówiono sposób toocreate tabele skuteczne bazy danych, zobacz [tworzenia tabel bazy danych skuteczne](https://msdn.microsoft.com/library/cc505842.aspx). Aby uzyskać informacje dotyczące wybierania typów danych, zobacz [typy danych](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> Można również użyć hello [projektanta tabel w programie SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate i projektowanie tabelach. 

![Relacje między tabelami](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. W Eksploratorze obiektów kliknij prawym przyciskiem myszy pozycję **mySampleDatabase** i kliknij opcję **Nowe zapytanie**. Puste zapytanie zostanie otwarte okno czyli tooyour połączenia bazy danych.

2. W oknie zapytania hello wykonaj hello następującego zapytania toocreate cztery tabel bazy danych: 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Tworzenie tabel](./media/sql-database-design-first-database/create-tables.png)

3. Rozwiń węzeł "tabele" hello w hello programu SQL Server Management Studio obiektu explorer toosee hello tabele, które utworzono.

   ![tabele utworzone w programie ssms](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Ładowanie danych do tabel hello

1. Utwórz folder o nazwie **SampleTableData** pliki do pobrania folderu toostore przykładowych danych bazy danych. 

2. Kliknij prawym przyciskiem myszy hello następujące łącza i zapisać je w hello **SampleTableData** folderu. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Otwórz okno wiersza polecenia i przejdź do folderu SampleTableData toohello.

4. Wykonaj następujące polecenia tooinsert przykładowych danych do tabel hello, zastępując wartości hello hello **ServerName**, **DatabaseName**, **UserName**i **Hasło** hello wartościami dla danego środowiska.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

Teraz załadowano przykładowych danych do tabel hello, utworzony wcześniej.

## <a name="query-data"></a>Zapytania o dane

Wykonanie poniższych informacji tooretrieve zapytania z tabel bazy danych hello hello. Zobacz [Pisanie zapytań SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn więcej informacji na temat Pisanie zapytań SQL. Pierwsza kwerenda Hello łączy wszystkie cztery tabele toofind przez wszystkich studentów hello nauczanych przez "Dominick Pope" które mają wyższe niż 75% stopnia w swojej klasie. Witaj drugiego zapytania wszystkie cztery między tabelami i wyszukuje wszystkich kursów, w których kiedykolwiek zarejestrował "Noe Coleman".

1. W oknie zapytania SQL Server Management Studio wykonaj następujące kwerendy hello:

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. W oknie zapytania SQL Server Management Studio wykonaj następujące zapytanie:

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Przywracanie bazy danych tooa poprzedniego punktu w czasie

Załóżmy, że przypadkowo usunięto tabelę. Jest to coś, co nie można łatwo odzyskać z. Bazy danych SQL Azure pozwala toogo tooany zapasowego punktu w czasie w hello ostatnio zapasowej too35 dni i przywrócić ten punkt w czasie tooa nowej bazy danych. Możesz to toorecover bazy danych usunięte dane. Hello następujące kroki hello przykładowej bazy danych tooa punktu przywracania przed dodaniem hello tabel.

1. Na stronie Baza danych SQL hello bazy danych, kliknij przycisk **przywrócić** na powitania narzędzi. Witaj **przywrócić** zostanie otwarta strona.

   ![Przywracanie](./media/sql-database-design-first-database/restore.png)

2. Wypełnianie hello **przywrócić** formularza hello wymagane informacje:
    * Nazwa bazy danych: podaj nazwę bazy danych 
    * W momencie: Wybierz hello **w momencie** kartę w formularzu przywracania hello 
    * Punkt przywracania: Wybierz godzinę, która występuje przed zmianą hello bazy danych
    * Serwer docelowy: nie można zmienić tę wartość podczas przywracania bazy danych 
    * Elastyczna pula baz danych: Wybierz **None**  
    * Warstwa cenowa: Wybierz **20 jednostek Dtu** i **250 GB** magazynu.

   ![punkt przywracania](./media/sql-database-design-first-database/restore-point.png)

3. Kliknij przycisk **OK** toorestore hello bazy danych za[tooa punktu przywracania w czasie](sql-database-recovery-using-backups.md#point-in-time-restore) przed dodaniem hello tabel. Przywracanie bazy danych tooa innego punktu w czasie tworzy duplikat bazy danych w hello tym samym serwerze co hello oryginalnej bazy danych lub nowszym hello punktu w czasie określisz, tak długo, jak jest w okresie przechowywania powitania dla Twojego [warstwy usług](sql-database-service-tiers.md).

## <a name="next-steps"></a>Następne kroki 
W tym samouczku przedstawiono bazy danych podstawowych zadań takich jak utworzyć bazę danych i tabele, załadować zapytania na danych i przywrócić hello bazy danych tooa wcześniejszego punktu w czasie. W tym samouczku omówiono:
> [!div class="checklist"]
> * Tworzenie bazy danych
> * Konfigurowanie reguł zapory
> * Połączenia bazy danych toohello z [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * Tworzenie tabel
> * Danych ładowania zbiorczego
> * Dane zapytania
> * Przywracanie bazy danych hello tooa poprzedniego punktu w czasie przy użyciu bazy danych SQL [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore) możliwości

Przejdź dalej toolearn samouczka toohello o projektowaniu bazy danych przy użyciu programu Visual Studio i C#.

> [!div class="nextstepaction"]
>[Projekt bazy danych Azure SQL i Połącz z C# i ADO.NET](sql-database-design-first-database-csharp.md)
