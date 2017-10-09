---
title: "uwierzytelnianie wieloskładnikowe aaaConfigure - Azure SQL | Dokumentacja firmy Microsoft"
description: "Uwierzytelnianie wzięciu pod uwagę wielu z narzędzia SSMS dla bazy danych SQL i magazyn danych SQL."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Skonfiguruj usługę Multi-Factor authentication dla programu SQL Server Management Studio i Azure AD

W tym temacie opisano sposób toouse usługi Azure Active Directory uwierzytelnianie wieloskładnikowe (MFA) z programu SQL Server Management Studio. Usługa Azure AD MFA można podczas łączenia z SSMS lub SqlPackage.exe tooAzure bazy danych SQL i magazyn danych SQL Azure.

Omówienie uwierzytelniania wieloskładnikowego bazy danych SQL Azure, zobacz [uwierzytelnianiem uniwersalnym z bazy danych SQL i magazyn danych SQL (Obsługa SSMS MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Kroki konfiguracji

1. **Konfigurowanie usługi Azure Active Directory** — Aby uzyskać więcej informacji, zobacz [administrowanie katalogiem usługi Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [integrowanie tożsamości lokalnych z usługą Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Dodać własne tooAzure nazwy domeny AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure obsługuje teraz federacji z usługi Active Directory systemu Windows Server](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), i [Zarządzanie usługą Azure AD przy użyciu programu Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Skonfigurowanie uwierzytelniania Wieloskładnikowego** — Aby uzyskać instrukcje, zobacz [co to jest usługa Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [warunkowego dostępu (MFA) z bazy danych SQL Azure i magazynem danych](sql-database-conditional-access.md). (Dostępu warunkowego pełnej wymaga Premium usługi Azure Active Directory (Azure AD). Ograniczone MFA jest dostępna z standardowe usługi Azure AD).
3. **Konfigurowanie bazy danych SQL lub magazynu danych SQL na potrzeby uwierzytelniania usługi Azure AD** — Aby uzyskać instrukcje, zobacz [tooSQL łączenie bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](sql-database-aad-authentication.md).
4. **Pobierz narzędzia SSMS** — na komputerze klienckim hello, Pobierz hello najnowsze narzędzia SSMS, z [pobierania programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Dla wszystkich funkcji hello w tym temacie Użyj co najmniej 2017 lipca, wersja 17.2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Łączenie za pomocą uwierzytelniania uniwersalnego SSMS

Hello następujące kroki pokazują, jak tooSQL tooconnect bazy danych lub SQL Data Warehouse przy użyciu hello najnowsze narzędzia SSMS.

1. za pomocą uwierzytelniania uniwersalnego na powitania tooconnect **połączyć tooServer** okno dialogowe, wybierz opcję **usługi Active Directory - uniwersalnego z obsługą uwierzytelniania Wieloskładnikowego**. (Jeśli zostanie wyświetlony **uniwersalnych uwierzytelnianie usługi Active Directory** nie są na powitania najnowszą wersję programu SSMS.)  
   ![Połącz uniwersalnego 1mfa][1]  
2. Zakończenie hello **nazwy użytkownika** pole przy użyciu poświadczeń usługi Azure Active Directory hello, w formacie hello `user_name@domain.com`.  
   ![1mfa-universal połączyć — użytkownika](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Jeśli łączysz się jako użytkownik-Gość, należy kliknąć opcję **opcje**, a na powitania **właściwości połączenia** okno dialogowe, pełną hello **Identyfikatora nazwy lub dzierżawy domeny AD** pole. Aby uzyskać więcej informacji, zobacz [uwierzytelnianiem uniwersalnym z bazy danych SQL i magazyn danych SQL (Obsługa SSMS MFA)](sql-database-ssms-mfa-authentication.md).
   ![uwierzytelnianie wieloskładnikowe dzierżawy ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. W zwykły sposób dla bazy danych SQL i magazyn danych SQL, należy kliknąć opcję **opcje** i Określ bazę danych hello na powitania **opcje** okno dialogowe. (Jeśli hello połączony użytkownik jest użytkownikiem gościa (tj. joe@outlook.com), należy hello pole wyboru i dodać hello AD bieżącego Identyfikatora nazwy lub dzierżawy domeny jako część opcji. Zobacz [uwierzytelnianiem uniwersalnym z bazy danych SQL i magazyn danych SQL (Obsługa SSMS MFA)]()(sql — baza danych ssms-mfa-authentication.md. Następnie kliknij przycisk **Connect**.  
5. Gdy hello **Zaloguj się na koncie tooyour** zostanie wyświetlone okno dialogowe, podaj hello konto i hasło tożsamości usługi Azure Active Directory. Hasło nie jest wymagane, jeśli użytkownik należy do domeny Sfederowanych z usługą Azure AD.  
   ![2mfa — logowanie][2]  

   > [!NOTE]
   > Uniwersalny do uwierzytelniania przy użyciu konta, które nie wymagają usługi MFA połączenie w tym momencie. Dla użytkowników wymagających uwierzytelniania MFA Kontynuuj hello następujące kroki:
   >  
   
6. Okna dialogowe dwa ustawienia usługi MFA może być wyświetlany. Jednorazowo operacja zależy od administratora MFA hello ustawienie i dlatego może być opcjonalny. Dla domeny włączone uwierzytelnianie MFA czasami jest wstępnie zdefiniowana w tym kroku (na przykład hello domeny wymaga toouse użytkowników za pomocą kart inteligentnych i numer pin).  
   ![Instalator 3mfa][3]  
7. drugi możliwe Hello jeden raz — okno dialogowe umożliwia tooselect szczegóły hello metody uwierzytelniania. Możliwe opcje Hello są skonfigurowane przez administratora.  
   ![4mfa-Sprawdź-1][4]  
8. Witaj w usłudze Azure Active Directory wysyła hello potwierdzenie tooyou informacji. Gdy otrzymasz kod weryfikacyjny hello, wprowadzić go w hello **wprowadź kod weryfikacyjny** i kliknij **Zaloguj**.  
   ![5mfa-Sprawdź-2][5]  

Po zakończeniu weryfikacji SSMS łączy zwykle przy założeniu dostępu zapory i prawidłowe poświadczenia.

## <a name="next-steps"></a>Następne kroki

* Omówienie uwierzytelniania wieloskładnikowego bazy danych SQL Azure, zobacz uniwersalnych uwierzytelniania za pomocą [bazy danych SQL i magazyn danych SQL (Obsługa SSMS MFA)](sql-database-ssms-mfa-authentication.md).
* Przyznać dostęp innym tooyour bazy danych: [SQL bazy danych uwierzytelnianie i autoryzacja: udzielanie dostępu](sql-database-manage-logins.md)  
Upewnij się, że inne osoby mogą łączenie się za pośrednictwem zapory hello: [przy użyciu reguły zapory Konfigurowanie poziomu serwera bazy danych SQL Azure hello portalu Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

