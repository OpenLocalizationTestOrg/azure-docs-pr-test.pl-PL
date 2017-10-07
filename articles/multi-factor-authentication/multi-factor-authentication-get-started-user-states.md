---
title: "aaaMicrosoft stanów użytkownika uwierzytelnianie wieloskładnikowe Azure"
description: "Więcej informacji na temat stanu użytkowników w usłudze Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>Jak toorequire weryfikacji dwuetapowej dla użytkownika lub grupy

Istnieją dwa podejścia do wymagania weryfikacji dwuetapowej. Pierwsza opcja Hello jest tooenable każdy użytkownik usługi Azure Multi-Factor Authentication (MFA). Gdy użytkownicy są włączone pojedynczo, zawsze wykonywać weryfikacji dwuetapowej (z pewnymi wyjątkami, np. po zalogowaniu się z zaufanych adresów IP, lub jeśli hello zapamiętanych urządzeniach funkcja jest włączona). Druga opcja Hello jest tooset się zasady dostępu warunkowego, która wymaga weryfikacji dwuetapowej w niektórych warunkach.

>[!TIP] 
>Wybierz jedną z tych metod toorequire weryfikację dwuetapową, nie oba. Włączenie użytkownika dla usługi Azure MFA zastępuje wszystkie zasady dostępu warunkowego.

## <a name="which-option-is-right-for-you"></a>Która opcja jest dla Ciebie

**Włączanie usługi Azure MFA, zmieniając stanów użytkownika** jest hello tradycyjne podejście, wymagająca weryfikacji dwuetapowej. Działa zarówno usługi Azure MFA w chmurze hello i serwera usługi Azure MFA. Wszyscy użytkownicy hello, które można włączyć mają hello tego samego środowiska, czyli weryfikacji dwuetapowej tooperform za każdym razem zalogują się w. Włączenie użytkownik zastępuje wszystkie zasady dostępu warunkowego, które mogą mieć wpływ na tego użytkownika. 

**Włączanie usługi Azure MFA z zasad dostępu warunkowego** jest bardziej elastyczne podejście wymagająca weryfikacji dwuetapowej. Jego prawidłowe tylko dla usługi Azure MFA w chmurze hello, a dostęp warunkowy jest [płatnej funkcji usługi Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Można utworzyć zasady dostępu warunkowego, które dotyczą toogroups, a także poszczególnych użytkowników. O wysokim ryzyku grup można przydzielić więcej ograniczeń, niż niskiego ryzyka grup lub weryfikacji dwuetapowej mogą być wymagane tylko dla aplikacji w chmurze o wysokim ryzyku i pomijana dla nich niskiego ryzyka. 

Obie te opcje monit o tooregister użytkowników dla usługi Azure Multi-Factor Authentication hello zalogowaniu po wymagania hello włączyć po raz pierwszy. Obie te opcje są również współpracować z hello można skonfigurować [ustawienia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Włączyć usługi Azure MFA przez zmianę stanu użytkownika

Konta użytkowników w usłudze Azure Multi-Factor Authentication mają następujące trzy różne stany hello:

| Stan | Opis | Aplikacje korzystające z przeglądarki, których to dotyczy |
|:---:|:---:|:---:|
| Disabled (Wyłączony) |Hello stan domyślny dla nowych użytkowników niezarejestrowanych Azure Multi-Factor Authentication (MFA). |Nie |
| Enabled (Włączony) |Witaj użytkownik został zarejestrowany w usłudze Azure MFA, ale nie został zarejestrowany. Będą one hello tooregister zostanie wyświetlony monit o następnym zalogowaniu. |Nie.  Nadal toowork ukończenie procesu rejestracji hello. |
| Enforced (Wymuszony) |Hello użytkownika został zarejestrowany i ukończył procesu rejestracji hello dla usługi Azure MFA. |Tak.  Aplikacje wymagają hasła aplikacji. |

Stan użytkownika odzwierciedla czy administrator zarejestrował je w usłudze Azure MFA i czy zostały ukończone hello procesu rejestracji.

Wszyscy użytkownicy uruchamiane *wyłączone*. Po zarejestrowaniu użytkowników usługi Azure MFA, ich zmian stanu *włączone*. Gdy użytkownicy włączone Zaloguj się i ukończenie procesu rejestracji hello, ich stan zmieni się zbyt*wymuszane*.  

### <a name="view-hello-status-for-a-user"></a>Wyświetl stan powitania dla użytkownika

Użyj następujących hello kroki tooaccess hello strony, gdzie można przeglądać i zarządzać stanów użytkownika:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Przejdź za**usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**.
   ![Wybierz uwierzytelnianie wieloskładnikowe](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Zostanie otwarta strona nowe, wyświetlającego hello stanów użytkownika.
   ![Stan użytkownika usługi Multi-Factor authentication — zrzut ekranu](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Zmiana stanu powitania dla użytkownika

1. Użyj hello poprzedzających kroki tooget toohello uwierzytelniania wieloskładnikowego użytkownicy strony.
2. Znajdź użytkownika hello mają tooenable dla usługi Azure MFA. Może być konieczne toochange hello widoku u góry hello. 
   ![Znajdź użytkownika — zrzut ekranu](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Sprawdź nazwę tootheir dalej pole hello.
4. W prawo, w obszarze Szybkie kroki hello, wybierz polecenie **włączyć** lub **wyłączyć**.
   ![Włącz wybranego użytkownika — zrzut ekranu](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Włączone* użytkowników pozwala automatycznie przełączać zbyt*wymuszane* po rejestracji dla usługi Azure MFA. Nie należy ręcznie zmienić tooenforced stanu użytkownika hello. 

5. Potwierdź wybór w oknie podręcznym hello, który zostanie otwarty. 

Po włączeniu użytkowników, należy powiadomić ich za pośrednictwem poczty e-mail. Poinformuj go, że ich pojawi się monit tooregister hello następnym razem zalogują się w. Ponadto jeśli Twoja organizacja korzysta z aplikacji korzystających z przeglądarki, które nie obsługują nowoczesnego uwierzytelniania, będzie konieczne toocreate hasła aplikacji. Możesz również uwzględnić tooour łącze [przewodnik dla użytkowników końcowych usługi Azure MFA](./end-user/multi-factor-authentication-end-user.md) toohelp ich wprowadzenie.

### <a name="use-powershell"></a>Korzystanie z programu PowerShell
toochange hello użytkownika stanu stanu przy użyciu [programu Azure AD PowerShell](/powershell/azure/overview), zmień `$st.State`. Istnieją trzy stany:

* Enabled (Włączony)
* Enforced (Wymuszony)
* Disabled (Wyłączony)  

Nie przenoś użytkowników bezpośrednio toohello *wymuszone* stanu. Aplikacje oparte na przeglądarce nie będzie przestaną działać, ponieważ nie przeszli rejestracji usługi MFA i uzyskać użytkownik hello [hasła aplikacji](multi-factor-authentication-whats-next.md#app-passwords). 

Przy użyciu programu PowerShell jest dobrym rozwiązaniem, gdy potrzebujesz toobulk umożliwienie użytkownikom. Utwórz skrypt programu PowerShell w pętli listę użytkowników i umożliwia ich:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Oto przykład:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Włącz zasady dostępu warunkowego usługi Azure MFA

Dostęp warunkowy jest płatnych funkcji usługi Azure Active Directory o wiele opcji konfiguracji możliwe. Te kroki przeprowadzenie jednokierunkowej toocreate zasady. Aby uzyskać więcej informacji, przeczytaj o [dostępu warunkowego w usłudze Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Przejdź za**usługi Azure Active Directory** > **dostępu warunkowego**.
3. Wybierz **nowe zasady**.
4. W obszarze **przypisania**, wybierz pozycję **użytkowników i grup**. Użyj hello **Include** i **wykluczyć** toospecify, którzy użytkownicy i grupy będą zarządzane przez zasady hello karty.
5. W obszarze **przypisania**, wybierz pozycję **aplikacji w chmurze**. Wybierz tooinclude **wszystkich aplikacji w chmurze**.
6. W obszarze **dostęp do formantów**, wybierz pozycję **Grant**. Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.
7. Włącz **Włącz zasady** za**na** , a następnie wybierz **zapisać**.

Witaj inne opcje zasad dostępu warunkowego hello pozwalają toospecify dokładnie, gdy weryfikacja dwuetapowa powinno być wymagane. Na przykład można utworzyć zasad, które stany: gdy wykonawców próbują tooaccess aplikacji zamówień z niezaufanymi sieciami, na urządzeniach, które nie są przyłączone do domeny, wymaga weryfikacji dwuetapowej. 

## <a name="next-steps"></a>Następne kroki

- Zapoznaj się z poradami na powitania [najlepszych rozwiązań dotyczących dostępu warunkowego](../active-directory/active-directory-conditional-access-best-practices.md)

- Zarządzaj ustawieniami usługi Multi-Factor Authentication [użytkowników i urządzeń](multi-factor-authentication-manage-users-and-devices.md)