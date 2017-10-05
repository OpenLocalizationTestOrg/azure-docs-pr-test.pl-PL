---
title: "Zabezpieczanie bazy danych w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące zabezpieczenia bazy danych w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Zabezpieczanie bazy danych w usłudze SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Uwierzytelnianie](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

W tym artykule przedstawiono podstawowe informacje o zabezpieczaniu bazy danych magazynu danych SQL Azure. W szczególności, w tym artykule ułatwiają rozpoczęcie pracy z zasobami ograniczania dostępu, ochrony danych i monitorowania działań w bazie danych.

## <a name="connection-security"></a>Zabezpieczenia połączeń
Zabezpieczenia połączeń dotyczą sposobu ograniczania i zabezpieczania połączeń z bazą danych przy użyciu reguł zapory i szyfrowania połączeń.

Reguły zapory są używane zarówno przez serwer, jak i przez bazę danych do odrzucania prób połączenia z adresów IP, które nie zostały jawnie wymienione na liście dozwolonych hostów. Umożliwia nawiązywanie połączeń z aplikacji lub publiczny adres IP komputera klienta, należy najpierw utworzyć regułę zapory poziomu serwera przy użyciu portalu Azure, interfejsu API REST lub programu PowerShell. Najlepszym rozwiązaniem jest maksymalne ograniczenie zakresu adresów IP przepuszczanych przez zaporę serwera.  Aby uzyskać dostęp do usługi Azure SQL Data Warehouse z komputera lokalnego, upewnij się, że zapory w sieci i komputera lokalnego umożliwia komunikację wychodzący na porcie TCP 1433.  Aby uzyskać więcej informacji, zobacz [zapory bazy danych SQL Azure][Azure SQL Database firewall], [procedurę składowaną sp_set_firewall_rule][sp_set_firewall_rule], i [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Domyślnie są szyfrowane połączenia z usługą SQL Data Warehouse.  Modyfikowanie ustawień połączenia umożliwia wyłączenie szyfrowania są ignorowane.

## <a name="authentication"></a>Authentication
Uwierzytelnianie to sposób potwierdzenia tożsamości podczas nawiązywania połączenia z bazą danych. Magazyn danych SQL obsługuje obecnie uwierzytelniania programu SQL Server z nazwą użytkownika i hasło, a także usługi Azure Active Directory. 

Po utworzeniu serwera logicznego bazy danych należy określić nazwę logowania „server admin” przy użyciu nazwy użytkownika i hasła. Przy użyciu tych poświadczeń, można uwierzytelniać na dowolnym bazy danych na tym serwerze jako właściciel bazy danych lub "właściciela" przy użyciu uwierzytelniania programu SQL Server.

Jednak najlepszym rozwiązaniem użytkowników w organizacji należy używać innego konta do uwierzytelniania. W ten sposób można ograniczyć uprawnienia do aplikacji i zmniejszyć ryzyko złośliwych działań w przypadku, gdy kod aplikacji jest narażony na atak iniekcji kodu SQL. 

Aby utworzyć serwer uwierzytelniony użytkownik SQL, połącz się z **wzorca** bazy danych na serwerze z zalogowaniem administrator serwera, a następnie utwórz nowe dane logowania serwera.  Ponadto jest dobrym rozwiązaniem jest utworzenie użytkownika w bazie danych master dla użytkowników usługi Azure SQL Data Warehouse. Tworzenie użytkownika w głównym umożliwia użytkownikom logowanie za pomocą takich narzędzi jak SSMS bez podawania nazwy bazy danych.  Umożliwia także użycie Eksplorator obiektów do wyświetlania wszystkich baz danych na serwerze SQL.

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Następnie połączyć się z **bazy danych magazynu danych SQL** z zalogowaniem administratora serwera i utworzyć użytkownika bazy danych oparte na nowo utworzoną logowanie do serwera.

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Jeśli użytkownik będzie jednak dodatkowe operacje, takie jak tworzenie identyfikatorów logowania lub tworzenia nowych baz danych, zostanie muszą być przypisani do `Loginmanager` i `dbmanager` ról w bazie danych master. Aby uzyskać więcej informacji o tych dodatkowych ról i uwierzytelniania w bazie danych SQL, zobacz [Zarządzanie bazami danych i logowaniami w bazie danych SQL Azure][Managing databases and logins in Azure SQL Database].  Aby uzyskać więcej informacji o usłudze Azure AD dla usługi SQL Data Warehouse, zobacz [łączenie z SQL danych magazynu przy użyciu Azure uwierzytelnianie usługi Active Directory][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autoryzacja
Autoryzacji odwołuje się do co można zrobić w bazie danych magazynu danych SQL Azure, a jest to kontrolowane przez członkostwo w rolach konta użytkownika i uprawnienia. Zalecanym najlepszym rozwiązaniem jest przyznanie użytkownikom minimalnych niezbędnych uprawnień. Usługa Azure SQL Data Warehouse ułatwia to zarządzanie za pomocą ról w T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

Konto administratora serwera, za pomocą którego nawiązujesz połączenie, jest członkiem roli db_owner, która ma uprawnienia do wykonywania wszystkich funkcji w bazie danych. Zapisz to konto, aby móc wdrażać uaktualnienia schematów i wykonywać inne operacje zarządzania. Używaj konta „ApplicationUser” z bardziej ograniczonymi uprawnienia do nawiązywania połączenia pomiędzy swoją aplikacją a bazą danych aplikacji, korzystając z minimalnych uprawnień wymaganych przez aplikację.

Istnieją następujące sposoby dalszego ograniczenia operacji wykonywanych przez użytkownika w usłudze Azure SQL Database:

* Szczegółowe [uprawnienia] [ Permissions] pozwalają kontroli operacje można wykonywać następujące czynności w poszczególnych kolumnach, tabele, widoki, procedury i innych obiektów w bazie danych. Umożliwia szczegółowe uprawnienia większości kontrolę i udzielanie minimalne uprawnienia wymagane. System szczegółowe uprawnienia jest dość złożone i wymaga niektórych badania efektywnie korzystać.
* [Ról bazy danych] [ Database roles] innych niż db_datareader i db_datawriter może służyć do tworzenia bardziej zaawansowanych kont użytkowników aplikacji lub słabszy kont zarządzania. Role wbudowane stałej bazy danych z łatwością udzielić uprawnień, ale może spowodować udzielanie więcej uprawnień niż jest to konieczne.
* [Procedury składowane] [ Stored procedures] pozwala ograniczyć akcje, które można podjąć w bazie danych.

Zarządzanie bazami danych i serwerami logicznymi z klasycznego portalu Azure lub za pomocą interfejsu API usługi Azure Resource Manager jest kontrolowane przez przypisania ról do konta użytkownika portalu. Aby uzyskać więcej informacji na ten temat, zobacz [kontroli dostępu opartej na rolach w portalu Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Szyfrowanie
Azure SQL Data magazynu przezroczysty danych szyfrowania (funkcji TDE) chroni przed zagrożeniem złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania danych w stanie spoczynku.  Podczas szyfrowania bazy danych, skojarzonych kopii zapasowych i plików dzienników transakcji są szyfrowane bez konieczności wprowadzania jakichkolwiek zmian w aplikacji. Funkcji TDE szyfruje magazyn całej bazy danych przy użyciu klucza symetrycznego o nazwie klucza szyfrowania bazy danych. Baza danych SQL klucza szyfrowania bazy danych jest chroniona za pomocą certyfikatu wbudowanego serwera. Certyfikat serwera wbudowanych jest unikatowy dla każdego serwera bazy danych SQL. Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni. Algorytm szyfrowania używany przez usługi SQL Data Warehouse jest AES 256. Ogólny opis funkcji TDE, zobacz [przezroczystego szyfrowania danych][Transparent Data Encryption].

Można zaszyfrować przy użyciu bazy danych [Azure Portal] [ Encryption with Portal] lub [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Następne kroki
Aby uzyskać szczegółowe informacje i przykłady dotyczące łączenia się z usługą SQL Data Warehouse przy użyciu różnych protokołów, zobacz [nawiązywanie połączenia z usługi SQL Data Warehouse][Connect to SQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
