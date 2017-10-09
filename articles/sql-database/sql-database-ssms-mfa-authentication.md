---
title: "uwierzytelniania wieloskładnikowego aaaMulti - Azure SQL | Dokumentacja firmy Microsoft"
description: "Uwierzytelnianie wzięciu pod uwagę wielu z narzędzia SSMS dla bazy danych SQL i magazyn danych SQL."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Uwierzytelnianiem uniwersalnym z bazy danych SQL i magazyn danych SQL (Obsługa SSMS MFA)
Azure SQL Database i Azure SQL Data Warehouse obsługi połączeń z programu SQL Server Management Studio (SSMS) przy użyciu *uniwersalnych uwierzytelnianie usługi Active Directory*. 
**Pobierz hello najnowsze narzędzia SSMS** — na komputerze klienckim hello, Pobierz najnowszą wersję programu SSMS, hello z [pobierania programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Dla wszystkich funkcji hello w tym temacie Użyj co najmniej 2017 lipca, wersja 17.2.  Hello najnowsze połączenia dialogowym wygląda podobnie do następującej: ![połączenia uniwersalnego 1mfa](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "pole Nazwa użytkownika hello zakończeniem.")  

## <a name="hello-five-authentication-options"></a>opcje uwierzytelniania Hello 5  
- Uniwersalny uwierzytelnianie usługi Active Directory obsługuje dwie metody uwierzytelniania nieinterakcyjnym hello (`Active Directory - Password` uwierzytelniania i `Active Directory - Integrated` uwierzytelniania). Nieinterakcyjne `Active Directory - Password` i `Active Directory - Integrated` metody uwierzytelniania mogą być używane w wielu różnych aplikacji (ADO.NET JDBC, ODBC, itp.). Te dwie metody nigdy nie powoduje podręcznych oknach dialogowych.

- `Active Directory - Universal with MFA`uwierzytelnianie jest metody interakcyjnej, który również obsługuje *Azure Multi-Factor Authentication* (MFA). Usługa Azure MFA ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą zakresu opcje weryfikacji łatwe (połączenie telefoniczne, wiadomość tekstowa, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej), dzięki czemu użytkownicy toochoose hello metody preferowany. Interakcyjne MFA z usługą Azure AD może spowodować wyskakujące okno dialogowe do weryfikacji.

Opis usługi Multi-Factor Authentication, zobacz [uwierzytelnianie wieloskładnikowe](../multi-factor-authentication/multi-factor-authentication.md).
Kroki konfiguracji, zobacz [uwierzytelnianie wieloskładnikowe skonfigurować bazy danych SQL Azure dla programu SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD nazwy lub dzierżawy parametr Identyfikatora domeny   

Począwszy od [SSMS wersji 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), użytkowników, którzy są importowane do hello bieżącej usłudze Active Directory z innych katalogów Active Azure jako goście, można podać nazwę domeny hello Azure AD, lub Identyfikatorem dzierżawy podczas nawiązywania połączenia. Goście obejmują zaproszenie z innych usługa Azure AD, konta Microsoft, takich jak outlook.com, hotmail.com, live.com lub innych kont, takich jak gmail.com użytkowników. Informacje te pozwalają **Active Directory uniwersalnej przy użyciu uwierzytelniania MFA** hello tooidentify poprawne uwierzytelniania urzędu. Ta opcja jest również wymagany toosupport kont Microsoft (MSA), takich jak outlook.com, hotmail.com, live.com lub kont innych niż MSA. Identyfikator tych użytkowników, którzy chcą się, że uwierzytelniony przy użyciu uwierzytelniania uniwersalnego toobe wprowadzić odpowiednią nazwę domeny usługi Azure AD lub dzierżawy. Tego parametru reprezentuje hello Azure AD w bieżącej domeny nazwy/dzierżawy identyfikator hello Azure serwer jest połączony z. Na przykład, jeśli serwer Azure jest skojarzony z domeny usługi Azure AD `contosotest.onmicrosoft.com` gdzie użytkownika `joe@contosodev.onmicrosoft.com` znajduje się jako użytkownik zaimportowane z domeny usługi Azure AD `contosodev.onmicrosoft.com`, hello tooauthenticate wymagana jest nazwa domeny, ten użytkownik jest `contosotest.onmicrosoft.com`. Gdy użytkownik hello jest natywny użytkownik tooAzure usługi Azure AD połączone powitania serwera i nie jest konta MSA, wymagany jest identyfikator nie domeny nazwy lub dzierżawcy. tooenter hello parametr (począwszy od wersji 17.2 SSMS), w hello **połączyć tooDatabase** okno dialogowe, okno dialogowe hello pełną, wybierając **usługi Active Directory - uniwersalnego za pomocą usługi MFA** uwierzytelniania, Kliknij przycisk **opcje**, pełną hello **nazwy użytkownika** , a następnie kliknij przycisk hello **właściwości połączenia** kartę. Sprawdź hello **Identyfikatora nazwy lub dzierżawy domeny AD** polu i podaj urzędu uwierzytelniania, takie jak nazwa domeny hello (**contosotest.onmicrosoft.com**) lub hello GUID identyfikator hello dzierżawcy.  
   ![uwierzytelnianie wieloskładnikowe dzierżawy ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Obsługuje toobusiness firm w usłudze Azure AD   
Obsługiwane w przypadku scenariusze B2B usługi Azure AD jako goście Azure użytkowników usługi AD (zobacz [co to jest współpraca B2B usługi Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) można połączyć tylko jako część członków grupy utworzone w bieżącej usłudze Azure AD i mapować ręcznie tooSQL bazy danych i magazyn danych SQL przy użyciu hello języka Transact-SQL `CREATE USER` instrukcji w danej bazie danych. Na przykład jeśli `steve@gmail.com` jest zaproszonych tooAzure AD `contosotest` (z domeną usługi Azure Ad hello `contosotest.onmicrosoft.com`), grupy usługi Azure AD, takich jak `usergroup` muszą być tworzone w hello Azure AD, która zawiera hello `steve@gmail.com` elementu członkowskiego. Następnie tej grupy musi zostać utworzony dla określonej bazy danych (tj. mojabazadanych) przez administratora Azure AD SQL lub Azure AD DBO, wykonując języka Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` instrukcji. Po utworzeniu użytkownika bazy danych hello hello użytkownika `steve@gmail.com` może się zalogować za`MyDatabase` przy użyciu opcji uwierzytelniania SSMS hello `Active Directory – Universal with MFA support`. Witaj usergroup, domyślnie ma tylko hello połączenia uprawnień i wszelkie dodatkowe dostępu do danych, wymagającym toobe przyznane w hello normalny sposób. Należy pamiętać, że użytkownik `steve@gmail.com` użytkownika gościa musi hello pole wyboru i dodać nazwy domeny hello AD `contosotest.onmicrosoft.com` w hello SSMS **właściwości połączenia** okno dialogowe. Witaj **Identyfikatora nazwy lub dzierżawy domeny AD** opcja jest obsługiwana tylko dla hello uniwersalnego z użyciem opcji połączenia usługi MFA, w przeciwnym razie jest nieaktywna.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Uniwersalny uwierzytelniania ograniczeń dotyczących korzystania z bazy danych SQL i magazyn danych SQL
* SSMS i SqlPackage.exe są hello narzędzia tylko aktualnie włączone dla usługi MFA za pomocą uwierzytelniania uniwersalnego usługi Active Directory.
* SSMS wersji 17.2, obsługuje współbieżny dostęp wielu użytkowników za pomocą uwierzytelniania uniwersalnego za pomocą usługi MFA. Wersja 17,0 i 17.1, ograniczone do dziennika w dla wystąpienia programu SSMS za pomocą uwierzytelniania uniwersalnego tooa jednego konta usługi Azure Active Directory. toolog w jako innego konta usługi Azure AD, należy użyć innego wystąpienia programu SSMS. (To ograniczenie jest ograniczona tooActive uwierzytelnianiem uniwersalnym katalogu; możesz zalogować się toodifferent serwerów przy użyciu uwierzytelniania hasła w usłudze Active Directory, zintegrowane uwierzytelnianie usługi Active Directory lub uwierzytelniania programu SQL Server).
* SSMS obsługuje uwierzytelnianie usługi Active Directory uniwersalnych wizualizacji Eksplorator obiektów, edytora zapytań i Magazyn zapytań.
* SSMS wersji 17.2 zapewnia obsługę DacFx kreatora Wdróż-Export/wyodrębniania danych w bazie danych. Po uwierzytelnieniu określonego użytkownika za pomocą okna dialogowego uwierzytelniania początkowego hello za pomocą uwierzytelniania uniwersalnego hello funkcje kreatora DacFx hello sam sposób, jak dla wszystkich innych metod uwierzytelniania.
* Hello projektanta tabel SSMS nie obsługuje uwierzytelniania uniwersalnego.
* Istnieją nie dodatkowe wymagania programowe dla uniwersalnych uwierzytelnianie usługi Active Directory, z wyjątkiem tego, że musi używać obsługiwanej wersji programu SSMS.  
* Hello wersja Active Directory Authentication Library (ADAL) dla uniwersalnych uwierzytelniania został tooits zaktualizowano najnowszą wersję ADAL.dll 3.13.9 dostępne wydane. Zobacz [biblioteki uwierzytelniania usługi Active Directory 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Następne kroki

- Kroki konfiguracji, zobacz [uwierzytelnianie wieloskładnikowe skonfigurować bazy danych SQL Azure dla programu SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Przyznać dostęp innym tooyour bazy danych: [SQL bazy danych uwierzytelnianie i autoryzacja: udzielanie dostępu](sql-database-manage-logins.md)  
- Upewnij się, że inne osoby mogą łączenie się za pośrednictwem zapory hello: [przy użyciu reguły zapory Konfigurowanie poziomu serwera bazy danych SQL Azure hello portalu Azure](sql-database-configure-firewall-settings.md)  
- [Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Struktura aplikacji warstwy danych programu Microsoft SQL Server (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importuj tooa pliku pliku BACPAC nowej bazy danych SQL Azure](../sql-database/sql-database-import.md)  
- [Eksportowanie pliku pliku BACPAC tooa bazy danych Azure SQL](../sql-database/sql-database-export.md)  
- C# interfejs [IUniversalAuthProvider — interfejs](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
