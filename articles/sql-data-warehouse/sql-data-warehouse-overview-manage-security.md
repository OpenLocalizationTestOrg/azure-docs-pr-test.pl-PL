---
title: "aaaSecure bazy danych w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Zabezpieczanie bazy danych w usłudze SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Uwierzytelnianie](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

W tym artykule przedstawiono podstawy hello zabezpieczania bazy danych magazynu danych SQL Azure. W szczególności, w tym artykule ułatwiają rozpoczęcie pracy z zasobami ograniczania dostępu, ochrony danych i monitorowania działań w bazie danych.

## <a name="connection-security"></a>Zabezpieczenia połączeń
Zabezpieczenia połączeń odwołuje się toohow ograniczenia i zabezpieczanie bazy danych tooyour połączeń przy użyciu reguł zapory i szyfrowanie połączenia.

Reguły zapory są używane przez oba powitania serwera i hello bazy danych tooreject próby nawiązania połączenia z adresów IP, które nie zostały jawnie białej. tooallow połączenia z aplikacji lub publiczny adres IP komputera klienta, należy najpierw utworzyć regułę zapory poziomu serwera przy użyciu hello portalu Azure, interfejsu API REST lub programu PowerShell. Najlepszym rozwiązaniem należy ograniczyć zakresów adresów IP hello dozwolone za pośrednictwem zapory serwera, jak to możliwe.  tooaccess magazyn danych SQL Azure z komputera lokalnego, upewnij się, że hello zapory w sieci i komputera lokalnego umożliwia komunikację wychodzący na porcie TCP 1433.  Aby uzyskać więcej informacji, zobacz [zapory bazy danych SQL Azure][Azure SQL Database firewall], [procedurę składowaną sp_set_firewall_rule][sp_set_firewall_rule], i [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Domyślnie są szyfrowane tooyour połączeń SQL Data Warehouse.  Modyfikowanie toodisable ustawienia połączenia szyfrowania są ignorowane.

## <a name="authentication"></a>Authentication
Uwierzytelnianie odwołuje się toohow potwierdzenia tożsamości, łącząc toohello bazy danych. Magazyn danych SQL obsługuje obecnie uwierzytelniania programu SQL Server z nazwą użytkownika i hasło, a także usługi Azure Active Directory. 

Po utworzeniu powitania serwera logicznego bazy danych określonego identyfikatora logowania "administratora serwera" przy użyciu nazwy użytkownika i hasła. Te poświadczenia można uwierzytelniać tooany baza danych na tym serwerze jako właściciel bazy danych hello lub "właściciela" przy użyciu uwierzytelniania programu SQL Server.

Jednak najlepszym rozwiązaniem użytkowników w organizacji należy używać tooauthenticate innego konta. Dzięki temu można ograniczać hello uprawnienia przyznane aplikacji toohello i zmniejszyć ryzyko hello złośliwych działań w przypadku ataku polegającego na iniekcji SQL tooa narażony jest kod aplikacji. 

toocreate serwera uwierzytelniony użytkownik SQL, Połącz toohello **wzorca** bazy danych na serwerze z zalogowaniem administrator serwera, a następnie utwórz nowe dane logowania serwera.  Ponadto jest dobrym rozwiązaniem toocreate użytkownika w bazie danych master powitania dla użytkowników usługi Azure SQL Data Warehouse. Tworzenie użytkownika w głównym umożliwia toologin użytkownika, za pomocą takich narzędzi jak SSMS bez podawania nazwy bazy danych.  Umożliwia także toouse hello obiektu explorer tooview wszystkich baz danych na serwerze SQL.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Następnie należy połączyć tooyour **bazy danych magazynu danych SQL** z zalogowaniem administratora serwera i utworzyć użytkownika bazy danych oparte na powitania serwera logowania właśnie utworzony.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Jeśli użytkownik będzie jednak dodatkowe operacje, takie jak tworzenie identyfikatorów logowania lub tworzenia nowych baz danych, również należy toohello toobe przypisane `Loginmanager` i `dbmanager` ról w bazie danych master hello. Aby uzyskać więcej informacji o tych dodatkowych ról i tooa uwierzytelniania bazy danych SQL, zobacz [Zarządzanie bazami danych i logowaniami w bazie danych SQL Azure][Managing databases and logins in Azure SQL Database].  Aby uzyskać więcej informacji o usłudze Azure AD dla usługi SQL Data Warehouse, zobacz [łączenie tooSQL danych magazynu przy użyciu usługi Azure uwierzytelnianie usługi Active Directory][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autoryzacja
Autoryzacji odwołuje się toowhat można wykonać w bazie danych magazynu danych SQL Azure i jest to kontrolowane przez przynależności do ról i uprawnień konta użytkownika. Najlepszym rozwiązaniem należy udzielić hello użytkowników co najmniej niezbędne uprawnienia. Usługa Azure SQL Data Warehouse sprawia, że to łatwe toomanage z rolami T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

konto administratora serwera Hello łączysz się z jest członek roli db_owner, którego urząd toodo żadnych elementów hello bazy danych. Zapisz to konto, aby móc wdrażać uaktualnienia schematów i wykonywać inne operacje zarządzania. Korzystać z bardziej ograniczone uprawnienia tooconnect z bazy danych toohello aplikacji za pomocą hello konta "ApplicationUser" hello najniższych uprawnień wymaganych przez aplikację.

Istnieją sposoby toofurther limit co użytkownik może zrobić z bazy danych SQL Azure:

* Szczegółowe [uprawnienia] [ Permissions] pozwalają kontroli operacje można wykonywać następujące czynności w poszczególnych kolumnach, tabele, widoki, procedury i innych obiektów w bazie danych hello. Użyj szczegółowe uprawnienia toohave hello sterowanie i udzielanie hello minimalne uprawnienia wymagane. system szczegółowe uprawnienia Hello jest nieco skomplikowane i efektywnie wymaga niektórych toouse analizę.
* [Ról bazy danych] [ Database roles] innych niż db_datareader i db_datawriter mogą być używane toocreate słabszy kont zarządzania lub bardziej zaawansowanych kont użytkowników aplikacji. Witaj wbudowanych stałe role bazy danych zapewniają prosty sposób toogrant uprawnienia, ale może spowodować udzielanie więcej uprawnień niż jest to konieczne.
* [Procedury składowane] [ Stored procedures] mogą być używane toolimit hello akcje, które można podjąć w bazie danych hello.

Zarządzanie bazami danych i serwerów logicznych z hello klasycznego portalu Azure lub przy użyciu interfejsu API usługi Azure Resource Manager hello jest kontrolowana przez konto użytkownika portalu przypisań ról. Aby uzyskać więcej informacji na ten temat, zobacz [kontroli dostępu opartej na rolach w portalu Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Szyfrowanie
Azure SQL Data magazynu przezroczysty danych szyfrowania (funkcji TDE) chroni przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania danych w stanie spoczynku.  Podczas szyfrowania bazy danych, skojarzonych kopii zapasowych i plików dzienników transakcji są szyfrowane bez konieczności wprowadzania żadnych zmian tooyour aplikacji. Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych. W bazie danych SQL klucza szyfrowania bazy danych hello jest chroniony za pomocą certyfikatu wbudowanego serwera. certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera bazy danych SQL. Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni. Witaj algorytmów szyfrowania używanych przez usługi SQL Data Warehouse jest AES 256. Ogólny opis funkcji TDE, zobacz [przezroczystego szyfrowania danych][Transparent Data Encryption].

Można zaszyfrować bazy danych przy użyciu hello [Azure Portal] [ Encryption with Portal] lub [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Następne kroki
Aby uzyskać szczegółowe informacje i przykłady dotyczące łączenia tooyour SQL Data Warehouse przy użyciu różnych protokołów, zobacz [połączyć tooSQL hurtowni danych][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

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
