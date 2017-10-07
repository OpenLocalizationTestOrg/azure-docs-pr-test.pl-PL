---
title: "aaaAzure SQL logowania i użytkownicy | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o zarządzaniu zabezpieczeń bazy danych SQL, w szczególności jak toomanage bazy danych zabezpieczeń dostępu i logowania do konta głównego na poziomie serwera hello."
keywords: "zabezpieczenia bazy danych sql, zarządzanie zabezpieczeniami bazy danych, zabezpieczenia logowania, zabezpieczenia bazy danych, dostęp do bazy danych"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Kontrolowanie i udzielanie dostępu do bazy danych

Po skonfigurowaniu reguł zapory osoby mogą łączyć z tooa bazy danych SQL jako jedno z kont administratora hello, hello właściciel bazy danych lub jako użytkownika bazy danych w bazie danych hello.  

>  [!NOTE]  
>  Ten temat dotyczy tooAzure programu SQL server i tooboth bazy danych SQL i magazyn danych SQL bazy danych, które są tworzone na powitania serwera Azure SQL. Dla uproszczenia bazy danych SQL jest używany podczas odwoływania się tooboth bazy danych SQL i magazyn danych SQL. 
>

> [!TIP]
> Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Konta z uprawnieniami administracyjnymi bez ograniczeń
Istnieją dwa konta z uprawnieniami administracyjnymi (**Administrator serwera** i **Administrator usługi Active Directory**), które funkcjonują jako administratorzy. tooidentify tych kont administratora serwera SQL, otwórz hello portalu Azure, a następnie przejdź do właściwości toohello programu SQL server.

![Administratorzy serwera SQL](./media/sql-database-manage-logins/sql-admins.png)

- **Administrator serwera**   
Podczas tworzenia serwera Azure SQL musi zostać podany **identyfikator logowania administratora serwera**. Program SQL server tworzy konto jako identyfikatora logowania w bazie danych master hello. To konto używa do połączenia uwierzytelnienia programu SQL Server (nazwy użytkownika i hasła). Może istnieć tylko jedno z tych kont.   
- **Administrator usługi Azure Active Directory**   
Jako konto administratora można również skonfigurować jedno konto usługi Azure Active Directory (indywidualne lub grupy zabezpieczeń). Jest opcjonalne tooconfigure administrator usługi Azure AD, ale musi być skonfigurowany administrator usługi Azure AD, jeśli chcesz, aby toouse usługi Azure AD kont tooconnect tooSQL bazy danych. Aby uzyskać więcej informacji na temat konfigurowania dostępu do usługi Azure Active Directory, zobacz [tooSQL łączenie bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](sql-database-aad-authentication.md) i [SSMS obsługę usługi Azure AD MFA z SQL Bazy danych i usługi SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).
 

Witaj **administratora serwera** i **administratora usługi Azure AD** kont ma następujące cechy hello:
- To jedyne konta hello, które można automatycznie połączyć tooany bazy danych SQL na serwerze hello. (tooconnect tooa użytkownika bazy danych, innych kont musi być właścicielem hello hello bazy danych lub posiadać konto użytkownika w bazie danych użytkownika hello.)
- Te konta, wprowadź użytkownika bazy danych jako hello `dbo` użytkowników i ich ma wszystkie uprawnienia hello w bazach danych użytkownika hello. (hello właściciela bazy danych użytkownika wprowadza również hello bazy danych jako hello `dbo` użytkownika.) 
- Te konta należy wprowadzać hello `master` bazy danych jako hello `dbo` użytkownika i ma ograniczone uprawnienia w głównym. 
- Te konta nie są elementami członkowskimi hello standard programu SQL Server `sysadmin` stałej roli serwera, który nie jest dostępny w bazie danych SQL.  
- Te konta mogą tworzyć, modyfikować i usuwać bazy danych, identyfikatory logowania, użytkowników w bazie master oraz reguły zapory na poziomie serwera.
- Te konta można dodawać i usuwać elementy członkowskie toohello `dbmanager` i `loginmanager` ról.
- Te konta można wyświetlić hello `sys.sql_logins` tabeli systemowej.

### <a name="configuring-hello-firewall"></a>Konfigurowanie zapory hello
Po skonfigurowaniu hello zapory poziomu serwera dla poszczególnych adresów IP lub zakresu hello **administratora serwera SQL** i hello **administratora usługi Azure Active Directory** można połączyć toohello bazy danych master i wszystkie hello bazy danych użytkownika. Witaj początkowej zapory poziomu serwera można skonfigurować za pomocą hello [portalu Azure](sql-database-get-started-portal.md)za pomocą [środowiska PowerShell](sql-database-get-started-powershell.md) lub przy użyciu hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Po nawiązaniu połączenia można również skonfigurować dodatkowe reguły zapory na poziomie serwera za pomocą [języka Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Ścieżka dostępu administratora
Gdy hello zapory poziomu serwera jest prawidłowo skonfigurowany, hello **administratora serwera SQL** i hello **administratora usługi Azure Active Directory** można połączyć za pomocą narzędzi klienta, takich jak SQL Server Management Studio lub SQL Server Data Tools. Tylko hello najnowsze narzędzia Podaj wszystkie hello funkcje i możliwości. Witaj Poniższy diagram przedstawia typową konfigurację dla hello dwa konta administratora.

![Ścieżka dostępu administratora](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Korzystając z otwartego portu zapory poziomu serwera hello, Administratorzy mogą nawiązywać połączenie z tooany bazy danych SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Łączenie tooa bazy danych przy użyciu programu SQL Server Management Studio
Dla przewodnika tworzenia serwera, bazę danych, reguły zapory poziomu serwera oraz przy użyciu programu SQL Server Management Studio tooquery bazy danych, zobacz [Rozpoczynanie pracy z serwerami bazy danych SQL Azure, bazy danych i reguł zapory przy użyciu hello portalu Azure i SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Dodatkowe role administracyjne na poziomie serwera
Ponadto toohello poziomu serwera ról administracyjnych omówionych wcześniej, baza danych SQL zawiera dwa ograniczeniami ról administracyjnych na kontach użytkowników toowhich bazy danych master hello można dodać który udzielić uprawnień tooeither Tworzenie baz danych lub zarządzać nazwy logowania.

### <a name="database-creators"></a>Kreatory bazy danych
Jeden z tych ról administracyjnych jest hello **dbmanager:** roli. Członkowie tej roli mogą tworzyć nowe bazy danych. toouse tej roli, należy utworzyć użytkownika hello `master` bazy danych, a następnie dodaj hello użytkownika toohello **dbmanager:** roli bazy danych. toocreate bazy danych, użytkownik hello musi być użytkownikiem oparte na logowania programu SQL Server, w bazie danych master hello lub zawarte bazy danych użytkowników na podstawie użytkownika usługi Azure Active Directory.

1. Przy użyciu konta administratora, Połącz toohello bazy danych master.
2. Krok opcjonalny: Utwórz dane logowania uwierzytelniania programu SQL Server, przy użyciu hello [utworzyć logowania](https://msdn.microsoft.com/library/ms189751.aspx) instrukcji. Przykładowa instrukcja:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Podczas tworzenia nazwy logowania lub użytkownika zawartej bazy danych należy używać silnego hasła. Aby uzyskać więcej informacji, zobacz artykuł [Silne hasła](https://msdn.microsoft.com/library/ms161962.aspx).
    
   wydajność tooimprove logowania (podmiotów poziomu serwera) są tymczasowo przechowywane na poziomie bazy danych hello. pamięci podręcznej uwierzytelniania hello toorefresh, zobacz [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. W bazie danych master hello, należy utworzyć użytkownika przy użyciu hello [Tworzenie użytkownika](https://msdn.microsoft.com/library/ms173463.aspx) instrukcji. Hello użytkownika może być Azure użytkownika usługi Active Directory authentication zawarte bazy danych (Jeśli skonfigurowano środowisku uwierzytelniania usługi Azure AD), lub użytkownik bazy danych programu SQL Server authentication zawarte lub użytkownika uwierzytelniania programu SQL Server, oparte na SQL Logowanie do uwierzytelniania serwera (utworzonego w poprzednim kroku hello). Przykładowe instrukcje:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Dodaj hello nowego użytkownika, toohello **dbmanager:** roli bazy danych przy użyciu hello [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instrukcji. Przykładowe instrukcje:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > dbmanager: Hello jest roli bazy danych w bazie danych master, dzięki czemu można tylko dodać roli dbmanager: toohello użytkownika bazy danych. Nie można dodać roli toodatabase poziom identyfikatora logowania poziomu serwera.
    
5. W razie potrzeby skonfiguruj tooconnect użytkownika nowe hello zapory reguły tooallow. (hello nowego użytkownika mogą być chronione przez istniejącą regułę zapory).

Teraz hello użytkownika można połączyć z bazy danych master toohello i można tworzyć nowych baz danych. Tworzenie bazy danych hello konta Hello staje się właścicielem hello hello bazy danych.

### <a name="login-managers"></a>Menedżerowie logowania
Hello innych ról administracyjnych jest hello logowania Menedżera ról. Członkowie tej roli można utworzyć nowych nazw logowania w bazie danych master hello. Jeśli chcesz, możesz wykonać hello te same czynności (Utwórz nazwę logowania i użytkownika, a następnie dodaj toohello użytkownika **loginmanager** roli) tooenable użytkownika toocreate nowych nazw logowania hello wzorca. Zazwyczaj logowania nie są niezbędne, jak firma Microsoft zaleca korzystanie użytkowników zawartej bazy danych, uwierzytelnionym na powitania poziom bazy danych zamiast użytkowników oparte na nazwy logowania. Aby uzyskać więcej informacji, zobacz artykuł [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx) (Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych).

## <a name="non-administrator-users"></a>Użytkownicy niebędący administratorami
Ogólnie rzecz biorąc, bez uprawnień administratora konta nie muszą uzyskać dostęp do bazy danych master toohello. Utwórz użytkowników zawartej bazy danych na poziomie hello bazy danych przy użyciu hello [Tworzenie użytkownika (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instrukcji. Hello użytkownika może być Azure użytkownika usługi Active Directory authentication zawarte bazy danych (Jeśli skonfigurowano środowisku uwierzytelniania usługi Azure AD), lub użytkownik bazy danych programu SQL Server authentication zawarte lub użytkownika uwierzytelniania programu SQL Server, oparte na SQL Logowanie do uwierzytelniania serwera (utworzonego w poprzednim kroku hello). Aby uzyskać więcej informacji, zobacz artykuł [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx) (Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych). 

Użytkownicy toocreate połączyć toohello bazy danych i wykonaj instrukcje toohello podobne następujące przykłady:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Początkowo tylko jeden z administratorów hello lub właściciela hello hello bazy danych można tworzyć użytkownicy. tooauthorize dodatkowym użytkownikom toocreate nowi użytkownicy, przyznaj tym hello wybranego użytkownika `ALTER ANY USER` uprawnień przy użyciu instrukcji, takich jak:

```
GRANT ALTER ANY USER tooMary;
```

toogive dodatkowym użytkownikom pełną kontrolę nad hello bazy danych, były członkami hello **db_owner** stałej roli bazy danych przy użyciu hello `ALTER ROLE` instrukcji.

> [!NOTE]
> Witaj najbardziej typowe przyczyny toocreate bazy danych użytkowników użytkowników na podstawie nazwy logowania, jest w przypadku użytkowników uwierzytelniania programu SQL Server, które wymagają toomultiple bazy danych programu access. Oparte na nazwy logowania użytkowników są wiązanej toohello logowania i tylko jedno hasło, którym jest obsługiwany dla tej nazwy logowania. Użytkownicy zawartej bazy danych w poszczególnych bazach danych są poszczególnymi jednostkami i każdy z nich zachowuje własne hasło. Może to prowadzić do mylenia użytkowników zawartej bazy danych, jeśli nie zachowują oni identycznych haseł.

### <a name="configuring-hello-database-level-firewall"></a>Konfigurowanie zapory poziomu bazy danych hello
Najlepszym rozwiązaniem użytkownicy inni niż administrator powinien mieć tylko dostęp za pośrednictwem bazy hello zapory toohello danych, które używają. Zamiast autoryzowanie ich IP adresy poziomu serwera hello zapory i zapewniając im dostępu tooall baz danych, użyj hello [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) zapory poziomu bazy danych hello tooconfigure instrukcji. Witaj zapory poziomu bazy danych nie można skonfigurować przy użyciu portalu hello.

### <a name="non-administrator-access-path"></a>Ścieżka dostępu użytkownika niebędącego administratorem
Gdy hello zapory poziomu bazy danych jest prawidłowo skonfigurowany, hello bazy danych mogą to robić przy użyciu narzędzi klienta, takich jak SQL Server Management Studio lub SQL Server Data Tools. Tylko hello najnowsze narzędzia Podaj wszystkie hello funkcje i możliwości. powitania po diagram przedstawia ścieżki typowe dostęp bez uprawnień administratora.

![Ścieżka dostępu użytkownika niebędącego administratorem](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Grupy i role
Zarządzanie dostępem wydajne używa uprawnienia przypisane role zamiast poszczególnych użytkowników i toogroups. 

- Korzystając z uwierzytelniania usługi Azure Active Directory, umieść użytkowników usługi Azure Active Directory w grupie usługi Azure Active Directory. Utwórz użytkownika zawartej bazy danych dla grupy hello. Umieść co najmniej jeden użytkownik bazy danych do [roli bazy danych](https://msdn.microsoft.com/library/ms189121) , a następnie przypisać [uprawnienia](https://msdn.microsoft.com/library/ms191291.aspx) toohello roli bazy danych.

- Podczas korzystania z uwierzytelniania programu SQL Server, Utwórz użytkowników zawartej bazy danych w bazie danych hello. Umieść co najmniej jeden użytkownik bazy danych do [roli bazy danych](https://msdn.microsoft.com/library/ms189121) , a następnie przypisać [uprawnienia](https://msdn.microsoft.com/library/ms191291.aspx) toohello roli bazy danych.

Witaj ról bazy danych może być wbudowane role hello takich jak **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, i **db_denydatareader**. **db_owner** jest tooonly pełne uprawnienia toogrant często używane w przypadku kilku użytkowników. Hello innych ról stałej bazy danych ułatwiają szybkie uzyskanie proste bazy danych w rozwoju, ale nie są zalecane dla większości produkcyjnych baz danych. Na przykład Witaj **db_datareader** stałej roli bazy danych daje dostęp do odczytu Tabela tooevery hello bazy danych, która jest zazwyczaj więcej niż jest bezwzględnie konieczne. Jest znacznie hello toouse [Utwórz ROLĘ](https://msdn.microsoft.com/library/ms187936.aspx) toocreate instrukcji własne użytkownika ról bazy danych i dokładnie udzielić hello każdej roli co najmniej uprawnienia niezbędne do potrzeb biznesowych hello. Jeśli użytkownik jest członkiem wielu ról, ich agregacji hello uprawnień je wszystkie.

## <a name="permissions"></a>Uprawnienia
Istnieje ponad 100 uprawnień, których można indywidualnie udzielić lub odmówić w usłudze SQL Database. Wiele z tych uprawnień jest zagnieżdżonych. Na przykład Witaj `UPDATE` uprawnień na schemat zawiera hello `UPDATE` uprawnienie dla każdej tabeli w ramach tego schematu. Jak w przypadku większości systemów uprawnień hello odmowa uprawnienia przesłania grant. Z powodu hello zagnieżdżone rodzaj i liczbę hello uprawnień może upłynąć zachować ostrożność podczas badania toodesign tooproperly systemu odpowiednich uprawnień zabezpieczenia bazy danych. Rozpoczynać hello listę uprawnień na [uprawnienia (aparat bazy danych)](https://msdn.microsoft.com/library/ms191291.aspx) i przejrzyj hello [plakat rozmiar grafiki](http://go.microsoft.com/fwlink/?LinkId=229142) hello uprawnień.


### <a name="considerations-and-restrictions"></a>Uwagi i ograniczenia
Podczas zarządzania logowania i użytkowników w bazie danych SQL, należy wziąć pod uwagę następujące hello:

* Musi być połączony toohello **wzorca** bazy danych podczas wykonywania hello `CREATE/ALTER/DROP DATABASE` instrukcje.   
* Witaj toohello odpowiedniego użytkownika bazy danych **administratora serwera** logowania nie może zostać zmieniony lub porzucony. 
* Język domyślny hello hello jest angielski **administratora serwera** logowania.
* Witaj tylko Administratorzy (**administratora serwera** logowania lub administratora usługi Azure AD) i członków hello hello **dbmanager:** roli bazy danych w hello **wzorca** baza danych ma uprawnienie tooexecute hello `CREATE DATABASE` i `DROP DATABASE` instrukcje.
* Musi być połączony toohello bazy danych master, podczas wykonywania hello `CREATE/ALTER/DROP LOGIN` instrukcje. Nie zaleca się jednak używania nazw logowania. Zamiast tego korzystaj z użytkowników zawartej bazy danych.
* tooconnect tooa użytkownika bazy danych, należy podać nazwę hello bazy danych hello w parametrach połączenia hello.
* Tylko hello poziomu serwera podmiotu zabezpieczeń logowania i hello członkami hello **loginmanager** roli bazy danych w hello **wzorca** baza danych ma uprawnienia tooexecute hello `CREATE LOGIN`, `ALTER LOGIN`, i `DROP LOGIN` instrukcje.
* Podczas wykonywania hello `CREATE/ALTER/DROP LOGIN` i `CREATE/ALTER/DROP DATABASE` instrukcje w aplikacji ADO.NET, za pomocą sparametryzowanych poleceń jest niedozwolone. Aby uzyskać więcej informacji, zobacz artykuł [Polecenia i parametry](https://msdn.microsoft.com/library/ms254953.aspx).
* Podczas wykonywania hello `CREATE/ALTER/DROP DATABASE` i `CREATE/ALTER/DROP LOGIN` instrukcje, każdy z tych instrukcji musi być hello tylko instrukcji w partii języka Transact-SQL. W przeciwnym razie wystąpi błąd. Na przykład powitalne następującego języka Transact-SQL sprawdza, czy istnieje hello bazy danych. Jeśli istnieje, `DROP DATABASE` jest nazwana tooremove hello w bazie danych. Ponieważ hello `DROP DATABASE` instrukcja nie jest hello jedyną instrukcją w partii hello, wykonywania hello następujących instrukcji języka Transact-SQL powoduje wystąpienie błędu.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Podczas wykonywania hello `CREATE USER` instrukcji z hello `FOR/FROM LOGIN` opcji, należy ją hello tylko instrukcji w partii języka Transact-SQL.
* Podczas wykonywania hello `ALTER USER` instrukcji z hello `WITH LOGIN` opcji, należy ją hello tylko instrukcji w partii języka Transact-SQL.
* zbyt`CREATE/ALTER/DROP` użytkownika wymaga hello `ALTER ANY USER` uprawnień na powitania bazy danych.
* Gdy hello właściciela roli bazy danych próbuje tooadd lub usuwanie roli bazy danych innej bazy danych użytkownika tooor od tego, może wystąpić hello następujący błąd: **użytkownik lub rola "Name" nie istnieje w tej bazie danych.** Ten błąd występuje, ponieważ hello użytkownika nie jest właścicielem toohello widoczne. tooresolve ten problem, hello właściciela roli hello Udziel `VIEW DEFINITION` uprawnień na powitania użytkownika. 


## <a name="next-steps"></a>Następne kroki

- toolearn więcej informacji na temat reguł zapory, zobacz [zapory bazy danych SQL Azure](sql-database-firewall-configure.md).
- Omówienie wszystkie funkcje zabezpieczeń bazy danych SQL hello, zobacz [Omówienie zabezpieczeń SQL](sql-database-security-overview.md).
- Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](sql-database-security-tutorial.md).
- Aby uzyskać informacje o widokach i procedurach składowanych, zobacz artykuł dotyczący [tworzenia widoków i procedur składowanych](https://msdn.microsoft.com/library/ms365311.aspx)
- Informacje dotyczące udzielania obiekt bazy danych programu access tooa, zobacz [tooa udzielanie dostępu do obiektu bazy danych](https://msdn.microsoft.com/library/ms365327.aspx)
