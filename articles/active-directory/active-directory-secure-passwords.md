---
title: "Usługi Azure AD do warstwy zabezpieczeń hasła | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a>To podejście wielowarstwowych zabezpieczeń hasła usługi Azure AD

W tym artykule omówiono najlepsze rozwiązania można wykonać jako użytkownik lub administrator do ochrony usługi Azure Active Directory (Azure AD) Account firmy Microsoft.

 > [!NOTE]
 > Administratorzy usług Azure AD można zresetować hasło użytkownika za pomocą wskazówki zawarte w artykule [resetowania hasła dla użytkownika w usłudze Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Użytkownicy mogą resetować swoje hasła przy użyciu wskazówek w następującym artykule w [pomocy nie pamiętam hasła usługi Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Wymagania dotyczące hasła

Usługa Azure AD zapewnia następujące popularne podejścia do zabezpieczania haseł:

* Wymagania dotyczące długości hasła
* Wymagania dotyczące złożoności hasła
* Regularne i okresowe wygasanie haseł

Aby uzyskać informacje o resetowania w usłudze Azure Active Directory, zobacz temat [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Zabezpieczenia hasła w usłudze Azure AD

Usługi Azure AD i System obsługi kont Microsoft Użyj branży sprawdzonych metod w celu zabezpieczenia bezpiecznych haseł użytkowników i administratora, w tym:

* Hasła dynamicznie zakazane
* Inteligentna blokada haseł

Informacji na temat zarządzania hasłami oparte na bieżącej badań, można znaleźć w dokumencie [wskazówki dotyczące hasła](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Hasła dynamicznie zakazane

Usługi Azure AD i Accounts Microsoft zabezpieczenia ochrony hasłem przez dynamicznie zakaz często używanych haseł. Zespół ds. usługi Azure ID Identity Protection regularnie analizuje listy zakazanych haseł, zapobiegając stosowaniu powszechnie używanych haseł przez użytkowników. Ta usługa jest dostępna dla klientów usługi Azure AD i usługi konta Microsoft.

Podczas tworzenia haseł, jest ważne dla administratorów zachęcić pracowników do wybierz fraz hasła, które obejmują unikatowej kombinacji wartości litery, cyfry, znaki lub słowa. Takie podejście ułatwia niemal uniemożliwiają hasła użytkownika, którego bezpieczeństwo zostało naruszone ale łatwiejsze do zapamiętania przez użytkowników.

#### <a name="password-breaches"></a>Naruszenia hasła

Aby pozostać w jednym kroku wcześniejsze przez przestępców zawsze działa firmy Microsoft.

Zespół ds. usługi Azure AD Identity Protection nieustannie analizuje często używane hasła. Cyberprzestępcy również często stosują podobne strategie do przeprowadzania ataków, na przykład tworzą [tęczowe tablice](https://en.wikipedia.org/wiki/Rainbow_table) w celu łamania skrótów haseł.

Firma Microsoft stale analizuje [naruszenia danych](https://www.privacyrights.org/data-breaches) w celu utrzymania dynamicznie aktualizowanej listy zakazanych haseł, dzięki której narażone hasła są zakazywane, zanim staną się prawdziwym zagrożeniem dla klientów usługi Azure AD. Więcej informacji o naszych bieżących działaniach związanych z zabezpieczeniami można znaleźć w raporcie analizy zabezpieczeń firmy Microsoft [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Inteligentna blokada haseł

Gdy usługa Azure AD wykryje próbę złamania hasła użytkownika przez potencjalnego przestępcę, blokujemy konto użytkownika przy użyciu funkcji inteligentnej blokady haseł. Usługę Azure AD zaprojektowano z myślą o określaniu ryzyka związanego z konkretnymi sesjami logowania. Następnie przy użyciu najbardziej aktualnych danych zabezpieczeń stosujemy semantyki blokady przestanie zagrożeniami przez.

Jeśli użytkownik jest zablokowany z usługi Azure AD, ich ekran podobny do następującymi:

  ![Blokada w usłudze Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

W przypadku innych kont Microsoft ich ekranu wygląda podobnie do następującymi:

  ![Blokada konta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Aby uzyskać informacje o resetowania w usłudze Azure Active Directory, zobacz temat [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT](active-directory-passwords.md).

  >[!NOTE]
  >Jeśli jesteś administratorem usługi Azure AD, możesz użyć usługi [Windows Hello](https://www.microsoft.com/windows/windows-hello), aby całkowicie uniknąć tworzenia tradycyjnych haseł przez użytkowników.
  >

## <a name="next-steps"></a>Następne kroki

* [Jak zaktualizować własne hasło](active-directory-passwords-update-your-own-password.md)
* [The fundamentals of Azure identity management](fundamentals-identity.md) (Podstawy zarządzania tożsamościami w usłudze Azure)
* [Aktywność resetowania raportów dotyczących hasła](active-directory-passwords-reporting.md)


