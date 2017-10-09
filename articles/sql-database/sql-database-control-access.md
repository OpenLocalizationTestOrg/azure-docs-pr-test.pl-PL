---
title: "aaaGranting tooAzure dostępu do bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Więcej informacji o przyznanie dostępu tooMicrosoft bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Kontrola dostępu w usłudze Azure SQL Database
tooprovide zabezpieczeń, baza danych SQL kontroluje dostęp przy użyciu reguł zapory ograniczenie łączności za pomocą adresu IP mechanizmów uwierzytelniania wymagające tooprove użytkowników, tożsamości i ograniczanie użytkowników toospecific akcji i dane mechanizmów autoryzacji. 

> [!IMPORTANT]
> Przegląd funkcji zabezpieczeń hello bazy danych SQL, zobacz [Omówienie zabezpieczeń SQL](sql-database-security-overview.md). Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Zapora i reguły zapory
Usługa Microsoft Azure SQL Database udostępnia usługę relacyjnej bazy danych dla platformy Azure i innych aplikacji internetowych. toohelp chronić dane, zapór zapobiec wszystkich serwera bazy danych tooyour dostępu do chwili określenia komputery, które ma uprawnienia. Zapora Hello przyznaje toodatabases dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania. Aby uzyskać więcej informacji, zobacz [Omówienie reguł zapory usługi Azure SQL Database](sql-database-firewall-configure.md)

Witaj usługi baza danych SQL Azure jest dostępna tylko za pośrednictwem portu TCP 1433. tooaccess bazy danych SQL z komputera, sprawdź, czy zapory komputera klienta pozwalają wychodzących komunikacji TCP na porcie TCP 1433. Należy zablokować połączenia przychodzące na porcie TCP 1433, jeśli nie są one wymagane przez inne aplikacje. 

W trakcie procesu połączenia hello połączenia z maszyn wirtualnych platformy Azure są tooa przekierowane na inny adres IP i port unikatowa dla każdej roli procesu roboczego. numer portu Hello jest poza zakresem powitania od 11000 too11999. Aby uzyskać więcej informacji na temat portów TCP, zobacz [porty inne niż 1433 ADO.NET 4.5 i SQL Database2](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Authentication

Usługa SQL Database obsługuje dwa typy uwierzytelniania:

* **Uwierzytelnianie usługi SQL**, które używa nazwy użytkownika i hasła. Po utworzeniu powitania serwera logicznego bazy danych określonego identyfikatora logowania "administratora serwera" przy użyciu nazwy użytkownika i hasła. Przy użyciu tych poświadczeń, można uwierzytelniać tooany baza danych na tym serwerze jako właściciel bazy danych hello lub "właściciela". 
* **Uwierzytelnianie usługi Azure Active Directory**, które korzysta z tożsamości zarządzanej przez usługę Azure Active Directory i jest obsługiwane w przypadku zarządzanych i zintegrowanych domen. Używaj uwierzytelniania usługi Active Directory (zabezpieczeń zintegrowanych), [gdy tylko jest to możliwe](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode). Jeśli chcesz toouse uwierzytelniania usługi Azure Active Directory, należy utworzyć inny administrator serwera o nazwie hello "Administratora usługi Azure AD," zezwala tooadminister usługi Azure AD użytkownicy i grupy. Ten administrator może również wykonywać wszystkie operacje, które może wykonać zwykły administrator serwera. Zobacz [łączenie tooSQL bazy danych przy użyciu usługi Azure uwierzytelnianie usługi Active Directory](sql-database-aad-authentication.md) dla przewodnik toocreate tooenable administratora usługi Azure AD uwierzytelniania usługi Azure Active Directory.

Hello aparatu bazy danych powoduje zamknięcie połączenia, które bezczynnej ponad 30 minut. Witaj połączenia musi logowania ponownie, zanim będzie można go używać. Stale tooSQL aktywnych połączeń bazy danych wymagają ponowna Autoryzacja (wykonywane przez aparat bazy danych hello) co najmniej co 10 godzin. Aparat bazy danych Hello prób ponowna autoryzacja przy użyciu hasła pierwotnie przesłanych hello i nie danych wejściowych użytkownika jest wymagana. Ze względu na wydajność, po zresetowaniu hasła w bazie danych SQL, hello połączenie nie jest można następuje ponowne uwierzytelnianie, nawet jeśli hello połączenia jest resetowany powodu tooconnection korzystanie z puli. To jest inna niż hello zachowanie lokalnego programu SQL Server. Jeśli hello hasło zostało zmienione, ponieważ połączenie hello początkowo został autoryzowany, hello połączenia musi być zakończona, a nowe połączenie zostało nawiązane przy użyciu hello nowe hasło. Użytkownik z hello `KILL DATABASE CONNECTION` uprawnień może jednoznacznie zakończyć tooSQL połączenia bazy danych przy użyciu hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) polecenia.

Konta użytkowników mogą być tworzone w bazie danych master hello i może otrzymać uprawnienia we wszystkich baz danych na serwerze hello, lub też można tworzyć w bazie danych hello, (nazywany zawartych użytkowników). Aby uzyskać informacje dotyczące tworzenia danych logowania i zarządzania nimi, zobacz [Zarządzanie danymi logowania](sql-database-manage-logins.md). przenośność tooenhance i scalabilty, użyj skalowalność tooenhance użytkowników zawartej bazy danych. Aby uzyskać więcej informacji na temat zawartych użytkowników, zobacz [Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) i [Zawarte bazy danych](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Jako najlepsze rozwiązanie aplikacji należy używać tooauthenticate dedykowane konto — dzięki temu można ograniczać hello uprawnienia przyznane aplikacji toohello i zmniejszenia ryzyka hello złośliwych działań, w przypadku, gdy kod aplikacji jest narażony tooa iniekcja kodu SQL atak. Witaj zalecane podejście jest toocreate [zawartej bazy danych użytkownika](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), dzięki czemu tooauthenticate Twojej aplikacji bezpośrednio toohello bazy danych. 

## <a name="authorization"></a>Autoryzacja

Toowhat odwołuje się autoryzacji użytkownika mogą wykonywać w bazie danych SQL Azure i jest to kontrolowane przez konto użytkownika w bazie danych [członkostwo w rolach](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) i [uprawnienia na poziomie obiektu](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Najlepszym rozwiązaniem należy udzielić hello użytkowników co najmniej niezbędne uprawnienia. konto administratora serwera Hello łączysz się z jest członek roli db_owner, którego urząd toodo żadnych elementów hello bazy danych. Zapisz to konto, aby móc wdrażać uaktualnienia schematów i wykonywać inne operacje zarządzania. Korzystać z bardziej ograniczone uprawnienia tooconnect z bazy danych toohello aplikacji za pomocą hello konta "ApplicationUser" hello najniższych uprawnień wymaganych przez aplikację. Aby uzyskać więcej informacji, zobacz temat [Zarządzanie danymi logowania](sql-database-manage-logins.md).

Zwykle tylko administratorzy muszą uzyskać dostęp toohello `master` bazy danych. Rutynowe dostępu tooeach użytkownika do bazy danych powinna być za pośrednictwem użytkownicy inni niż administrator zawartej bazy danych utworzone w każdej bazie danych. Gdy używasz użytkowników zawartej bazy danych nie ma potrzeby toocreate logowania w hello `master` bazy danych. Aby uzyskać więcej informacji, zobacz artykuł [Contained Database Users - Making Your Database Portable](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) (Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych).

Należy zapoznać się z hello następujące funkcje, które może być używane toolimit lub podniesienia poziomu uprawnień:   
* [Personifikacja](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) i [moduł podpisywania](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) mogą być używane toosecurely podniesienia poziomu uprawnień tymczasowo.
* [Zabezpieczeń na poziomie wiersza](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) można używać do ograniczania zbioru wierszy, do których użytkownik może uzyskać dostęp.
* [Maskowanie danych](sql-database-dynamic-data-masking-get-started.md) mogą być używane toolimit ujawnianie danych wrażliwych.
* [Procedury składowane](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) mogą być używane toolimit hello akcje, które można podjąć w bazie danych hello.

## <a name="next-steps"></a>Następne kroki

- Przegląd funkcji zabezpieczeń hello bazy danych SQL, zobacz [Omówienie zabezpieczeń SQL](sql-database-security-overview.md).
- toolearn więcej informacji na temat reguł zapory, zobacz [reguły zapory](sql-database-firewall-configure.md).
- toolearn o użytkownikach i logowania, zobacz [Zarządzanie logowania](sql-database-manage-logins.md). 
- Aby uzyskać informacje dotyczące aktywnego monitorowania, zobacz [Database Auditing](sql-database-auditing.md) i [wykrywanie zagrożeń bazy danych SQL](sql-database-threat-detection.md).
- Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](sql-database-security-tutorial.md).
