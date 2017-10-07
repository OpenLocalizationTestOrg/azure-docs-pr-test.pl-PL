---
title: "aaaConditional dostępu — baza danych SQL Azure i magazynem danych | Doc firmy Microsoft"
description: "Dowiedz się, jak tooconfigure warunkowego dostępu do bazy danych SQL Azure i magazynem danych."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Dostęp warunkowy (MFA) i baza danych Azure SQL i magazynem danych  

Zarówno bazy danych SQL i magazyn danych SQL obsługuje dostęp warunkowy firmy Microsoft. Witaj, jak po Pokaż kroki tooconfigure bazy danych SQL tooenforce zasady dostępu warunkowego.  

## <a name="prerequisites"></a>Wymagania wstępne  
- Należy skonfigurować uwierzytelnianie usługi Azure Active Directory toosupport SQL Database lub SQL Data Warehouse. Do wykonania określonych kroków, zobacz [Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Po włączeniu usługi Multi-Factor authentication, należy połączyć z na obsługiwanych narzędzia, takie jak hello najnowsze narzędzia SSMS. Aby uzyskać więcej informacji, zobacz [uwierzytelnianie wieloskładnikowe skonfigurować bazy danych SQL Azure dla programu SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Konfigurowanie urzędu certyfikacji dla bazy danych Azure SQL/magazynu danych  
1.  Logowanie toohello portalu, wybierz **usługi Azure Active Directory**, a następnie wybierz **dostępu warunkowego**. Aby uzyskać więcej informacji, zobacz [informacje techniczne dotyczące usługi Azure Active Directory dostępu warunkowego](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![Blok dostępu warunkowego](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  W hello **zasady dostępu warunkowego** bloku, kliknij przycisk **nowe zasady**, podaj nazwę, a następnie kliknij przycisk **skonfigurować reguły**.  
3.  W obszarze **przypisania**, wybierz pozycję **użytkowników i grup**, sprawdź **Wybierz użytkowników i grupy**, a następnie wybierz hello użytkownikowi lub grupie dostępu warunkowego. Kliknij przycisk **wybierz**, a następnie kliknij przycisk **gotowe** tooaccept wybór.  
  ![Wybierz użytkowników i grup](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Wybierz **aplikacji w chmurze**, kliknij przycisk **Wybierz aplikacje**. Możesz sprawdzić wszystkie aplikacje dostępne dla dostępu warunkowego. Wybierz **bazy danych SQL Azure**, u dołu powitania kliknij **wybierz**, a następnie kliknij przycisk **gotowe**.  
  ![Wybierz bazę danych SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Jeśli nie możesz znaleźć **bazy danych SQL Azure** na liście powitania po trzeci zrzut ekranu, wykonać hello następujące kroki:   
  - Zaloguj się tooyour wystąpienia DW bazy danych SQL Azure przy użyciu narzędzia SSMS przy użyciu konta administratora usługi AAD.  
  - Wykonanie `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Zaloguj się tooAAD i sprawdź, czy baza danych SQL Azure i magazynu danych są wyświetlane w aplikacji hello w Twojej usłudze AAD.  

5.  Wybierz **dostęp do formantów**, wybierz pozycję **Grant**, a następnie sprawdź zasady hello ma tooapply. Na przykład możemy wybierz **wymusić uwierzytelnianie wieloskładnikowe**.  
  ![Wybierz Udziel dostępu](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Podsumowanie  
aplikacji Hello wybrane (Azure SQL Database) tooAzure tooconnect SQL bazy danych/magazynu danych przy użyciu usługi Azure AD Premium, co wymusza teraz hello wybrane zasady dostępu warunkowego, **wymagane uwierzytelnianie wieloskładnikowe.**  
Pytania dotyczące bazy danych SQL Azure i magazynem danych dotyczących uwierzytelniania wieloskładnikowego, skontaktuj się z MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Następne kroki  

Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](sql-database-security-tutorial.md).
