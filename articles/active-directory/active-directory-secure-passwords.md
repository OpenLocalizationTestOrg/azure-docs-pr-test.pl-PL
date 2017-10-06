---
title: "aaaAzure AD do warstwy zabezpieczeń hasła | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak usługi Azure AD wymusza silne hasła i uniemożliwia hasła użytkowników przez przestępców,"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Wielowarstwowa podejście tooAzure AD hasło zabezpieczeń

W tym artykule omówiono najlepsze rozwiązania z usługi Azure Active Directory (Azure AD) lub Account Microsoft można wykonać jako użytkownik lub administrator tooprotect.

 > [!NOTE]
 > Administratorzy usług Azure AD mogą resetować hasła użytkownika przy użyciu wskazówek hello w artykule hello [hello zresetowano hasło użytkownika w usłudze Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Użytkownicy mogą resetować swoje hasła przy użyciu wskazówek hello w artykule hello [pomocy nie pamiętam hasła usługi Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Wymagania dotyczące hasła

Usługi Azure AD zawiera następujące typowe hasła toosecuring podejścia hello:

* Wymagania dotyczące długości hasła
* Wymagania dotyczące złożoności hasła
* Regularne i okresowe wygasanie haseł

Uzyskać informacji na temat resetowania w usłudze Azure Active Directory, zobacz temat hello [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT hello](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Zabezpieczenia hasła w usłudze Azure AD

Usługi Azure AD i branży sprawdzone używane w systemie konta Microsoft hello zbliża się tooensure zabezpieczenie hasła użytkownika i administratora, w tym:

* Hasła dynamicznie zakazane
* Inteligentna blokada haseł

Uzyskać informacji na temat zarządzania hasłami oparte na bieżącej badań, zobacz oficjalny dokument hello [wskazówki dotyczące hasła](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Hasła dynamicznie zakazane

Usługi Azure AD i Accounts Microsoft zabezpieczenia ochrony hasłem przez dynamicznie zakaz często używanych haseł. zespół Azure identyfikator Identity Protection Hello regularnie analizuje listy zabronionych haseł, uniemożliwia wybranie często używanych haseł użytkowników. Ta usługa jest dostępna tooAzure AD i klienci usługi konta Microsoft hello.

Podczas tworzenia haseł, jest ważne dla administratorów tooencourage użytkowników toochoose hasło frazy, które obejmują unikatowej kombinacji wartości litery, cyfry, znaki lub słowa. Takie podejście ułatwia haseł użytkowników toomake toobe prawie niemożliwe naruszone, ale ułatwia tooremember użytkowników.

#### <a name="password-breaches"></a>Naruszenia hasła

Microsoft zawsze działa jeden krok toostay wcześniejsze przez przestępców.

Zespół usługi Azure AD Identity Protection Hello stale analizuje haseł, które są często używane. Przez przestępców również użyć podobne tooinform strategii ich ataki, takie jak tworzenie [siłowe tabeli](https://en.wikipedia.org/wiki/Rainbow_table) dla łamania skrótów haseł.

Firma Microsoft stale analizuje [naruszeń danych](https://www.privacyrights.org/data-breaches) toomaintain listy aktualizowany dynamicznie zabronione hasła, który zapewnia, że narażone hasła są niedozwolone, zanim staną się rzeczywistych zagrożenia tooAzure AD klientów. Aby uzyskać więcej informacji o bieżącym dążenie zabezpieczeń, zobacz hello [raportów analizy zabezpieczeń firmy Microsoft](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Inteligentna blokada haseł

Usługi Azure AD wykryje potencjalne toohack w trakcie karne ataków na hasło użytkownika, możemy zablokowanie hello konto użytkownika z inteligentne blokady hasła. Zaprojektowano w usłudze Azure AD toodetermine hello ryzyka związanego z określonej sesji. Następnie przy użyciu najnowszych danych zabezpieczeń hello stosujemy blokady semantyki toostop przez zagrożeń.

Jeśli użytkownik jest zablokowany z usługi Azure AD, ich ekranu wygląda podobnie toohello, co który następuje:

  ![Blokada w usłudze Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Dla innego konta Microsoft ich ekranu wygląda podobnie toohello, co który następuje:

  ![Blokada konta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Uzyskać informacji na temat resetowania w usłudze Azure Active Directory, zobacz temat hello [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT hello](active-directory-passwords.md).

  >[!NOTE]
  >Jeśli jesteś administratorem usługi Azure AD, możesz toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid o użytkownikom tworzenie haseł tradycyjnych całkowicie.
  >

## <a name="next-steps"></a>Następne kroki

* [Jak tooupdate własnego hasła](active-directory-passwords-update-your-own-password.md)
* [Witaj podstawowe informacje na temat zarządzania tożsamość platformy Azure](fundamentals-identity.md)
* [Aktywność resetowania raportów dotyczących hasła](active-directory-passwords-reporting.md)


