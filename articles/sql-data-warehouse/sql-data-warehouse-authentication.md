---
title: tooAzure aaaAuthentication SQL Data Warehouse | Dokumentacja firmy Microsoft
description: Azure Active Directory (AAD) i SQL Server authentication tooAzure SQL Data Warehouse.
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
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>TooAzure uwierzytelniania SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Uwierzytelnianie](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooSQL tooconnect hurtowni danych, należy podać poświadczenia zabezpieczeń na potrzeby uwierzytelniania. Po ustanowieniu połączenia, niektóre ustawienia połączenia są skonfigurowane jako część ustanawianie sesji kwerendy.  

Aby uzyskać więcej informacji na temat zabezpieczeń i w jaki sposób tooenable połączeń tooyour hurtowni danych, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Uwierzytelnianie SQL
tooSQL tooconnect hurtowni danych, należy podać hello następujących informacji:

* Servername FQDN
* Określ uwierzytelnianie SQL
* Nazwa użytkownika
* Hasło
* Domyślna baza danych (opcjonalnie)

Domyślnie nawiązaniu połączenia toohello *wzorca* bazy danych, a nie bazy danych użytkowników. tooconnect tooyour użytkownika bazy danych, można wybrać toodo jedną z następujących operacji:

* Określ hello domyślnej bazy danych podczas rejestrowania serwera w Eksploratorze obiektów SQL Server programu SSDT, SSMS, lub w ciągu połączenia aplikacji hello. Na przykład obejmować hello parametru InitialCatalog dla połączenia ODBC.
* Przed utworzeniem sesji programu SSDT, zaznacz hello bazy danych użytkownika.

> [!NOTE]
> Witaj instrukcji języka Transact-SQL **mojabazadanych UŻYJ;** nie jest obsługiwana dla Zmiana bazy danych hello połączenia. Wskazówki dotyczące łączenia tooSQL magazynu danych z narzędziami SSDT można odwoływać się toohello [zapytania z programem Visual Studio] [ Query with Visual Studio] artykułu.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Uwierzytelnianie usługi Azure Active Directory (AAD)
[Usługa Azure Active Directory] [ What is Azure Active Directory] uwierzytelnianie jest mechanizm łączący tooMicrosoft Azure SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD). Przy użyciu uwierzytelniania usługi Azure Active Directory mogą centralnie zarządzać hello tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji. Centralne zarządzanie identyfikator udostępnia jedno miejsce toomanage SQL Data Warehouse użytkowników i upraszcza zarządzanie uprawnieniami. 

### <a name="benefits"></a>Korzyści
Azure Active Directory korzyści:

* Zapewnia alternatywny tooSQL uwierzytelniania serwera.
* Pomaga zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych.
* Umożliwia obrotu hasła w jednym miejscu
* Zarządzaj uprawnieniami bazy danych przy użyciu zewnętrznego grup (AAD).
* Eliminuje zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.
* Używa zawarte bazy danych użytkowników tooauthenticate tożsamości na poziomie hello bazy danych.
* Obsługuje uwierzytelnianie na podstawie tokenu dla aplikacji łączenie tooSQL hurtowni danych.
* Obsługuje uwierzytelnianie wieloskładnikowe za pomocą uwierzytelniania uniwersalnego usługi Active Directory dla programu SQL Server Management Studio. Opis usługi Multi-Factor Authentication, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory jest nadal stosunkowo nowe i ma pewne ograniczenia. tooensure, że usługi Azure Active Directory jest odpowiedni dla danego środowiska, zobacz [funkcje usługi Azure AD i ograniczenia][Azure AD features and limitations], w szczególności hello dodatkowe zagadnienia.
> 
> 

### <a name="configuration-steps"></a>Kroki konfiguracji
Wykonaj te kroki tooconfigure usługi Azure Active Directory uwierzytelniania.

1. Utworzyć i wypełnić usługi Azure Active Directory
2. Opcjonalnie: Skojarz lub zmienić usługi active directory hello aktualnie skojarzony z subskrypcją platformy Azure
3. Utwórz administrator usługi Azure Active Directory dla usługi Azure SQL Data Warehouse.
4. Konfigurowanie komputerów klienckich
5. Utwórz użytkowników zawartej bazy danych w sieci tooAzure zamapować bazy danych tożsamości usługi AD
6. Połącz tooyour hurtowni danych przy użyciu tożsamości usługi Azure AD

Obecnie użytkownicy usługi Azure Active Directory nie są wyświetlane w Eksploratorze obiektów program SSDT. Jako obejście, Wyświetl użytkowników hello w [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Znajduje szczegóły hello
* Hello kroki tooconfigure i używanie usługi Azure Active Directory uwierzytelniania są niemal identyczne dla usługi Azure SQL Database i Azure SQL Data Warehouse. Wykonaj czynności opisane w temacie hello szczegółowe hello [tooSQL łączenie bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](../sql-database/sql-database-aad-authentication.md).
* Tworzenie ról w niestandardowej bazie danych i Dodawanie ról toohello użytkowników. Następnie przydziel uprawnienia szczegółowego toohello ról. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych aparatu uprawnień](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Następne kroki
toostart badania magazynu danych z programu Visual Studio i innych aplikacji, zobacz [zapytania z programem Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
