---
title: "Uwierzytelnianie usługi Active Directory aaaAzure - SQL Azure (omówienie) | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toouse usługi Azure Active Directory do uwierzytelniania przy użyciu bazy danych SQL i magazyn danych SQL"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Użyj uwierzytelniania usługi Azure Active Directory do uwierzytelniania przy użyciu bazy danych SQL lub SQL Data Warehouse
Uwierzytelnianie usługi Active Directory systemu Azure jest mechanizm łączący tooMicrosoft bazy danych SQL Azure i [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD). Przy użyciu uwierzytelniania usługi Azure AD mogą centralnie zarządzać hello tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji. Centralne zarządzanie identyfikator udostępnia jedno miejsce toomanage bazy danych użytkowników i upraszcza zarządzanie uprawnieniami. Witaj następujące korzyści:

* Zapewnia alternatywny tooSQL uwierzytelniania serwera.
* Pomaga zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych.
* Umożliwia obrotu hasła w jednym miejscu
* Klientów można zarządzać za pomocą zewnętrznego grup (AAD) uprawnień do bazy danych.
* Można go wyeliminować zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.
* Azure AD uwierzytelniania przy użyciu tożsamości tooauthenticate użytkowników zawartej bazy danych na poziomie bazy danych hello.
* Usługi Azure AD obsługuje uwierzytelnianie na podstawie tokenu łączenie tooSQL bazy danych aplikacji.
* Usługa Azure AD authentication obsługuje usług AD FS (Federacja domen) lub native użytkownika i hasło uwierzytelniania lokalnej usługi Azure Active Directory bez synchronizacji domeny.  
* Usługi Azure AD obsługuje połączenia z programu SQL Server Management Studio, które używają uniwersalnych uwierzytelnianie usługi Active Directory, która obejmuje usługi Multi-Factor Authentication (MFA).  Silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe obejmuje MFA — połączenie telefoniczne, wiadomość tekstowa, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej. Aby uzyskać więcej informacji, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Łączenie tooSQL na serwerze działa na maszynie Wirtualnej platformy Azure nie jest obsługiwany przy użyciu konta usługi Azure Active Directory. Zamiast tego użyj domeny konta usługi Active Directory.  

kroki konfiguracji Hello obejmują następujące procedury tooconfigure hello i korzystać z uwierzytelniania usługi Azure Active Directory.

1. Utworzyć i wypełnić usługi Azure AD.
2. Opcjonalnie: Skojarz lub zmiany usługi active directory hello aktualnie skojarzony z subskrypcją platformy Azure.
3. Tworzenie administratora usługi Azure Active Directory dla serwera Azure SQL lub [magazyn danych SQL Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Konfigurowanie komputerów klienckich.
5. Utwórz użytkowników zawartej bazy danych programu tooAzure zamapować bazy danych tożsamości usługi AD.
6. Łączenie tooyour bazy danych przy użyciu tożsamości usługi Azure AD.

> [!NOTE]
> toolearn jak toocreate i wypełnić usługi Azure AD i skonfiguruj usługi Azure AD z bazy danych SQL Azure i SQL Data Warehouse, zobacz [Konfigurowanie usługi Azure AD z bazy danych SQL Azure](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Architektura zaufania
powitania po diagramu wysokiego poziomu zawiera podsumowanie hello architektury rozwiązania przy użyciu uwierzytelniania usługi Azure AD z bazy danych SQL Azure. Witaj tego samego uniwersalne tooSQL hurtowni danych. jest uważany za toosupport hasło macierzystego użytkownika usługi Azure AD, tylko część chmury hello i Azure AD/usługi Azure SQL Database. toosupport uwierzytelnianie federacyjne (lub użytkownika i hasło dla poświadczeń systemu Windows), hello komunikację z bloku usług AD FS jest wymagana. Witaj strzałki oznaczają ścieżki komunikacji.

![diagram uwierzytelniania usługi AAD][1]

Hello poniższym diagramie wskazuje hello federation, zaufania i relacje zezwalających na kliencie bazy danych tooa tooconnect poprzez przesłanie token obsługi. Hello token jest uwierzytelniony przez usługę Azure AD i jest uważany za zaufany przez hello bazy danych. Odbiorcy 1 może reprezentować usługi Azure Active Directory z macierzystego użytkowników lub usługi Azure AD z użytkowników federacyjnych. Odbiorcy 2 reprezentuje możliwe rozwiązanie, łącznie z importowanych użytkowników. w tym przykładzie pochodzące z federacyjnych usługi Azure Active Directory z usług AD FS są synchronizowane z usługą Azure Active Directory. Jest ważne, toounderstand, do którego dostęp tooa bazy danych przy użyciu uwierzytelniania usługi Azure AD wymaga tego hello hosting subskrypcji jest skojarzony toohello usługi Azure AD. Witaj tej samej subskrypcji musi być toocreate używane hello programu SQL Server hostingu hello Azure SQL Database lub SQL Data Warehouse.

![Relacja subskrypcji][2]

## <a name="administrator-structure"></a>Struktura administratora
Podczas korzystania z uwierzytelniania usługi Azure AD, istnieją dwa konta administratora dla serwera bazy danych SQL hello; Witaj oryginalnego administratora serwera SQL i administratora hello Azure AD. Witaj tego samego uniwersalne tooSQL hurtowni danych. Tylko administrator hello na podstawie konta usługi Azure AD można utworzyć hello pierwszego użytkownika bazy danych usługi Azure AD zawarte w bazie danych użytkownika. Identyfikator logowania administratora usługi Azure AD Hello może być użytkownika usługi Azure AD lub grupy w usłudze Azure AD. Gdy hello administrator jest konto grupy, może służyć przez dowolnego członka grupy, włączania wielu administratorów usługi Azure AD dla hello wystąpienia programu SQL Server. Przy użyciu konta grupy, jak administrator zwiększa możliwości zarządzania, pozwalając toocentrally dodawać i usuwać elementy członkowskie grupy w usłudze Azure AD bez zmiany użytkowników hello lub uprawnienia w bazie danych SQL. W dowolnym momencie można skonfigurować tylko jeden administrator usługi Azure AD (użytkownik lub grupa).

![Struktura administratora][3]

## <a name="permissions"></a>Uprawnienia
toocreate nowi użytkownicy, musi mieć hello `ALTER ANY USER` uprawnień w bazie danych hello. Witaj `ALTER ANY USER` uprawnienia można przyznać tooany bazy danych użytkownika. Witaj `ALTER ANY USER` uprawnienie jest również w posiadaniu kont administratora serwera hello i bazy danych użytkownikom hello `CONTROL ON DATABASE` lub `ALTER ON DATABASE` uprawnienia dla tej bazy danych i członkom hello `db_owner` roli bazy danych.

toocreate zawartej bazy danych użytkownika w usłudze Azure SQL Database lub SQL Data Warehouse, należy połączyć toohello bazy danych przy użyciu tożsamości usługi Azure AD. toocreate hello pierwszego zawartej bazy danych użytkownika, należy połączyć toohello bazy danych przy użyciu usługi Azure AD administratora (przy użyciu jest właścicielem hello hello bazy danych). Zostało to przedstawione w kroku 4 i 5 poniżej. Uwierzytelniania usługi Azure AD jest możliwe tylko po Witaj, Administratorze usługi Azure AD została utworzona dla serwera Azure SQL Database lub SQL Data Warehouse. Witaj, Administratorze usługi Azure Active Directory został usunięty z serwera hello, istniejących użytkowników usługi Azure Active Directory wcześniej utworzonego w programie SQL Server można już połączyć toohello bazy danych przy użyciu swoich poświadczeń usługi Azure Active Directory.

## <a name="azure-ad-features-and-limitations"></a>Funkcje platformy Azure AD i ograniczenia
Witaj następujących członków usługi Azure AD można udostępnić w Azure SQL server lub SQL Data Warehouse:

* Natywny elementów członkowskich: element członkowski utworzone w usłudze Azure AD w domenie zarządzanej hello lub w domenie klienta. Aby uzyskać więcej informacji, zobacz [dodać własne tooAzure nazwy domeny AD](../active-directory/active-directory-add-domain.md).
* Elementy członkowskie domeny federacyjnej: element członkowski utworzone w usłudze Azure AD z domeny federacyjnej. Aby uzyskać więcej informacji, zobacz [Microsoft Azure obsługuje teraz federacji z usługi Active Directory systemu Windows Server](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Importowany członków z innych usługi Azure AD, którzy są członkami domeny native lub federacyjnych.
* Grup usługi Active Directory tworzone jako grupy zabezpieczeń.

Konta Microsoft (na przykład outlook.com, hotmail.com, live.com) lub inne konta gościa (na przykład gmail.com, yahoo.com) nie są obsługiwane. Jeśli możesz zalogować się za[https://login.live.com](https://login.live.com) przy użyciu hello konto i hasło, a następnie korzystanie z konta Microsoft, który nie jest obsługiwany dla uwierzytelniania usługi Azure AD dla bazy danych SQL Azure lub usługi Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Łączenie za pomocą tożsamości usługi Azure AD

Uwierzytelnianie usługi Active Directory platformy Azure obsługuje hello następujące metody łączenia tooa bazy danych przy użyciu tożsamości usługi Azure AD:

* Przy użyciu zintegrowanego uwierzytelniania systemu Windows
* Za pomocą głównej nazwy usługi Azure AD i hasła
* Przy użyciu tokenu uwierzytelniania aplikacji

### <a name="additional-considerations"></a>Dodatkowe zagadnienia

* możliwości zarządzania tooenhance, zaleca się udostępniania dedykowanych usługi Azure AD grupy jako administrator.   
* Tylko jeden administrator usługi Azure AD (użytkownik lub grupa) można skonfigurować dla serwera Azure SQL lub usługi Azure SQL Data Warehouse w dowolnym momencie.   
* Tylko administrator usługi Azure AD dla programu SQL Server można połączyć z początkowo toohello Azure SQL server lub usługi Azure SQL Data Warehouse przy użyciu konta usługi Azure Active Directory. Hello administratora usługi Active Directory można skonfigurować na kolejnych usługi Azure AD bazy danych użytkowników.   
* Firma Microsoft zaleca ustawienie hello limit czasu połączenia w sekundach too30.   
* SQL Server 2016 Management Studio i SQL Server Data Tools dla programu Visual Studio 2015 (wersja 14.0.60311.1April 2016 lub nowszy) obsługują uwierzytelniania usługi Azure Active Directory. (Uwierzytelniania usługi azure AD jest obsługiwana przez hello **dostawcy danych .NET Framework dla serwera SQL**; co najmniej wersji .NET Framework 4.6). W związku z tym hello najnowsze wersje tych narzędzi i aplikacji warstwy danych (DAC i bacpac) można korzystać z uwierzytelniania usługi Azure AD.   
* [ODBC w wersji 13.1](https://www.microsoft.com/download/details.aspx?id=53339) obsługuje jednak uwierzytelniania usługi Azure Active Directory `bcp.exe` nie można połączyć przy użyciu uwierzytelniania usługi Azure Active Directory, ponieważ używa starszej Dostawca ODBC.   
* `sqlcmd`obsługuje usługę Azure Active Directory uwierzytelniania, począwszy od wersji dostępnej w sklepie hello 13.1 [Centrum pobierania](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools dla programu Visual Studio 2015 wymaga co najmniej wersji kwietnia 2016 hello hello narzędzia danych (wersja 14.0.60311.1). Obecnie użytkowników usługi Azure AD nie są wyświetlane w Eksploratorze obiektów program SSDT. Jako obejście, Wyświetl użytkowników hello w [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [6.0 sterownik JDBC firmy Microsoft dla programu SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) usługi Azure AD obsługuje uwierzytelnianie. Zobacz też [ustawienie właściwości połączenia hello](https://msdn.microsoft.com/library/ms378988.aspx).   
* Program PolyBase nie można uwierzytelnić przy użyciu uwierzytelniania usługi Azure AD.   
* Uwierzytelnianie usługi Azure AD jest obsługiwana dla bazy danych SQL przez hello portalu Azure **Importuj bazę danych** i **wyeksportować bazy danych** bloków. Importowanie i eksportowanie przy użyciu uwierzytelniania usługi Azure AD jest również obsługiwany z hello polecenia programu PowerShell.   
* Usługa Azure AD authentication jest obsługiwana dla bazy danych SQL i usługi SQL Data Warehouse przy użyciu interfejsu wiersza polecenia. Aby uzyskać więcej informacji, zobacz [Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse](sql-database-aad-authentication-configure.md) i [SQL Server — az programu sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Następne kroki
- toolearn jak toocreate i wypełnić usługi Azure AD i skonfiguruj usługi Azure AD z bazy danych SQL Azure lub usługi Azure SQL Data Warehouse, zobacz [Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Dostęp i kontrola w usłudze SQL Database zostały omówione w temacie [Kontrola dostępu w usłudze SQL Database](sql-database-control-access.md).
- Dane logowania, użytkownicy i role bazy danych w usłudze SQL Database zostały omówione w temacie [Logins, users, and database roles](sql-database-manage-logins.md) (Dane logowania, użytkownicy i role bazy danych).
- Aby uzyskać więcej informacji na temat podmiotów zabezpieczeń bazy danych, zobacz [Principals](https://msdn.microsoft.com/library/ms181127.aspx) (Podmioty zabezpieczeń).
- Aby uzyskać więcej informacji na temat ról bazy danych, zobacz [Database roles](https://msdn.microsoft.com/library/ms189121.aspx) (Role bazy danych).
- Aby uzyskać więcej informacji na temat reguł zapory w usłudze SQL Database, zobacz [Omówienie reguł zapory usługi SQL Database](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

