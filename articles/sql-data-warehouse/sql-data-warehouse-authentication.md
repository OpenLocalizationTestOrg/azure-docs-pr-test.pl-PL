---
title: "Uwierzytelnianie usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Azure Active Directory (AAD) i SQL Server uwierzytelniania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a>Authentication to Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Uwierzytelnianie](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Aby połączyć magazyn danych SQL, należy podać poświadczenia zabezpieczeń na potrzeby uwierzytelniania. Po ustanowieniu połączenia, niektóre ustawienia połączenia są skonfigurowane jako część ustanawianie sesji kwerendy.  

Aby uzyskać więcej informacji dotyczących zabezpieczeń i sposobie włączania połączeń do magazynu danych, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Uwierzytelnianie SQL
Aby nawiązać połączenie SQL Data Warehouse, należy podać następujące informacje:

* Servername FQDN
* Określ uwierzytelnianie SQL
* Nazwa użytkownika
* Hasło
* Domyślna baza danych (opcjonalnie)

Domyślnie połączenie łączy się z *wzorca* bazy danych, a nie bazy danych użytkowników. Aby połączyć się z bazą danych użytkownika, można wykonać jedną z następujących:

* Określ domyślną bazę danych podczas rejestrowania serwera w Eksploratorze obiektów SQL Server programu SSDT, SSMS, lub w ciągu połączenia aplikacji. Na przykład dodać parametr InitialCatalog dla połączenia ODBC.
* Przed utworzeniem sesji programu SSDT, zaznacz bazy danych użytkownika.

> [!NOTE]
> Wykonywanie instrukcji języka Transact-SQL **mojabazadanych UŻYJ;** nie jest obsługiwana dla Zmiana bazy danych dla połączenia. Wskazówki dotyczące nawiązywania połączenia z usługi SQL Data Warehouse z narzędziami SSDT można odwoływać się do [zapytania z programem Visual Studio] [ Query with Visual Studio] artykułu.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Uwierzytelnianie usługi Azure Active Directory (AAD)
[Usługa Azure Active Directory] [ What is Azure Active Directory] uwierzytelnianie jest mechanizmu nawiązywania połączenia z programu Microsoft Azure SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD). Przy użyciu uwierzytelniania usługi Azure Active Directory mogą centralnie zarządzać tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji. Centralne zarządzanie identyfikator udostępnia jedno miejsce do zarządzania użytkownikami usługi SQL Data Warehouse i upraszcza zarządzanie uprawnieniami. 

### <a name="benefits"></a>Korzyści
Azure Active Directory korzyści:

* Stanowi alternatywę dla uwierzytelniania programu SQL Server.
* Pomaga zatrzymać rozprzestrzenianie tożsamości użytkowników na serwerach bazy danych.
* Umożliwia obrotu hasła w jednym miejscu
* Zarządzaj uprawnieniami bazy danych przy użyciu zewnętrznego grup (AAD).
* Eliminuje zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.
* Używa zawarte bazy danych użytkowników do uwierzytelniania tożsamości na poziomie bazy danych.
* Obsługuje uwierzytelnianie na podstawie tokenu dla aplikacji nawiązywania połączenia z usługi SQL Data Warehouse.
* Obsługuje uwierzytelnianie wieloskładnikowe za pomocą uwierzytelniania uniwersalnego usługi Active Directory dla programu SQL Server Management Studio. Opis usługi Multi-Factor Authentication, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory jest nadal stosunkowo nowe i ma pewne ograniczenia. Aby upewnić się, że usługi Azure Active Directory jest odpowiedni dla danego środowiska, zobacz [funkcje usługi Azure AD i ograniczenia][Azure AD features and limitations], w szczególności dodatkowe zagadnienia.
> 
> 

### <a name="configuration-steps"></a>Kroki konfiguracji
Wykonaj następujące kroki, aby skonfigurować uwierzytelnianie w usłudze Azure Active Directory.

1. Utworzyć i wypełnić usługi Azure Active Directory
2. Opcjonalnie: Skojarz lub zmienić usługi active directory, który jest aktualnie powiązany z subskrypcją platformy Azure
3. Utwórz administrator usługi Azure Active Directory dla usługi Azure SQL Data Warehouse.
4. Konfigurowanie komputerów klienckich
5. Utwórz użytkowników zawartej bazy danych w bazie danych mapowany na tożsamość usługi Azure AD
6. Połącz do magazynu danych przy użyciu tożsamości usługi Azure AD

Obecnie użytkownicy usługi Azure Active Directory nie są wyświetlane w Eksploratorze obiektów program SSDT. Jako obejście, wyświetlania informacji o użytkownikach w [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-the-details"></a>Znajdź szczegóły
* Kroki konfigurowania i korzystania z uwierzytelniania usługi Azure Active Directory są niemal identyczne dla usługi Azure SQL Database i Azure SQL Data Warehouse. Wykonaj szczegółowe kroki opisane w temacie [połączenie z bazą danych SQL lub SQL danych magazynu przy użyciu Azure uwierzytelnianie usługi Active Directory](../sql-database/sql-database-aad-authentication.md).
* Tworzenie ról w niestandardowej bazie danych i dodawanie użytkowników do ról. Następnie przydziel szczegółowe uprawnienia do ról. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych aparatu uprawnień](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Następne kroki
Aby uruchomić zapytanie magazynu danych z programu Visual Studio i innymi aplikacjami, zobacz [zapytania z programem Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
