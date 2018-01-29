---
title: "Microsoft Azure Multi-Factor Authentication użytkownika stanów"
description: "Więcej informacji na temat stanu użytkowników w usłudze Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: ad8d531d633eb65fe90404fdab0499b8e5332db6
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2018
---
# <a name="how-to-require-two-step-verification-for-a-user-or-group"></a>Jak zażądać weryfikacji dwuetapowej dla użytkownika lub grupy

Można wybrać jedno z dwóch metod wymagająca weryfikacji dwuetapowej. Pierwsza opcja jest umożliwienie każdy użytkownik usługi Azure Multi-Factor Authentication (MFA). Gdy użytkownicy są włączone pojedynczo, wykonują weryfikacji dwuetapowej każdym logowaniu (z pewnymi wyjątkami, np. po zalogowaniu z zaufanego adresu IP adresami lub gdy _zapamiętanych urządzeniach_ funkcja jest włączona). Drugą opcją jest do konfigurowania zasad dostępu warunkowego, która wymaga weryfikacji dwuetapowej w niektórych warunkach.

>[!TIP] 
>Wybierz jedną z tych metod, aby wymagać weryfikacji dwuetapowej, nie oba. Włączenie użytkownika uwierzytelnianie wieloskładnikowe Azure zastępuje wszystkie zasady dostępu warunkowego.

## <a name="which-option-is-right-for-you"></a>Która opcja jest dla Ciebie odpowiednia?

**Włączanie usługi Azure Multi-Factor Authentication, zmieniając stanów użytkownika** jest tradycyjne podejście, wymagająca weryfikacji dwuetapowej. Działa zarówno usługi Azure MFA w chmurze i serwera usługi Azure MFA. Wszystkich użytkowników, których można włączyć przeprowadzić weryfikację dwuetapową, za każdym razem zalogują się w. Włączenie użytkownik zastępuje wszystkie zasady dostępu warunkowego, które mogą mieć wpływ na tego użytkownika. 

**Włączanie usługi Azure Multi-Factor Authentication z zasad dostępu warunkowego** jest bardziej elastyczne podejście wymagająca weryfikacji dwuetapowej. Działa ona tylko dla usługi Azure MFA w chmurze, jednak i _dostępu warunkowego_ jest [płatnej funkcji usługi Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Można utworzyć zasady dostępu warunkowego, które są stosowane do grupy, a także poszczególnych użytkowników. O wysokim ryzyku grup można przydzielić więcej ograniczeń, niż niskiego ryzyka grup lub weryfikacji dwuetapowej mogą być wymagane tylko dla aplikacji w chmurze o wysokim ryzyku i pomijana dla nich niskiego ryzyka. 

Obie te opcje monitować użytkowników o zarejestrować uwierzytelnianie wieloskładnikowe Azure po raz pierwszy zalogowaniu po Włącz wymagania. Obie te opcje są również współpracować przy konfigurowalne [ustawienia usługi Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md).

## <a name="enable-azure-mfa-by-changing-user-status"></a>Włączyć usługi Azure MFA przez zmianę stanu użytkownika

Konta użytkowników w usłudze Azure Multi-Factor Authentication mają następujące trzy różne stany:

| Stan | Opis | Aplikacje korzystające z przeglądarki, których to dotyczy | Aplikacje przeglądarki, których to dotyczy | Nowoczesnego uwierzytelniania, których to dotyczy |
|:---:|:---:|:---:|:--:|:--:|
| Disabled (Wyłączony) |Stan domyślny dla nowego użytkownika nie są zarejestrowane w usłudze Azure MFA. |Nie |Nie |Nie |
| Enabled (Włączony) |Użytkownik został zarejestrowany w usłudze Azure MFA, ale nie został zarejestrowany. Otrzymują monit do zarejestrowania przy następnym zalogowaniu. |Nie.  One nadal działać do czasu ukończenia procesu rejestracji. | Tak. Po wygaśnięciu sesji jest wymagana rejestracja usługi Azure MFA.| Tak. Po wygaśnięciu tokenu dostępu jest wymagana rejestracja usługi Azure MFA. |
| Enforced (Wymuszony) |Użytkownik został zarejestrowany i ukończył proces rejestracji dla usługi Azure MFA. |Tak.  Aplikacje wymagają hasła aplikacji. |Tak. Usługa Azure MFA jest wymagana podczas logowania. | Tak. Usługa Azure MFA jest wymagana podczas logowania. |

Stan użytkownika odzwierciedla czy administrator zarejestrował je w usłudze Azure MFA i czy zostały ukończone w procesie rejestracji.

Wszyscy użytkownicy uruchamiane *wyłączone*. Po zarejestrowaniu użytkowników usługi Azure MFA ich stan zmieni się na *włączone*. Gdy użytkownicy włączone Zaloguj się i ukończenie procesu rejestracji, ich stan zmieni się na *wymuszone*.  

### <a name="view-the-status-for-a-user"></a>Wyświetlanie stanu użytkownika

Aby uzyskać dostęp do strony, gdzie można przeglądać i zarządzać stanu użytkowników, wykonaj następujące kroki:

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) jako administrator.
2. Przejdź do **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**.
   ![Wybierz uwierzytelnianie wieloskładnikowe](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Nowa strona, wyświetlająca stanu użytkownika otwiera.
   ![Stan użytkownika usługi Multi-Factor authentication — zrzut ekranu](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-the-status-for-a-user"></a>Zmiana stanu użytkownika

1. Użyj powyższych kroków, aby uzyskać dostęp do usługi Azure Multi-Factor Authentication **użytkowników** strony.
2. Znajdź użytkownika, który chcesz włączyć dla usługi Azure MFA. Może być konieczna zmiana widoku w górnej. 
   ![Znajdź użytkownika — zrzut ekranu](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Zaznacz pole przy jego nazwie.
4. Po prawej stronie w obszarze **Szybkie kroki**, wybierz **włączyć** lub **wyłączyć**.
   ![Włącz wybranego użytkownika — zrzut ekranu](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Włączone* użytkownicy są automatycznie przełączona na *wymuszone* po rejestracji dla usługi Azure MFA. Wykonaj ręcznie nie zmiany stanu użytkownika do *wymuszone*. 

5. Potwierdź wybór w otwartym oknie podręcznym. 

Po włączeniu użytkowników powiadamiać użytkowników za pośrednictwem poczty e-mail. Poinformuj go, pojawi się pytanie do zarejestrowania przy następnym zalogowaniu. Ponadto jeśli Twoja organizacja korzysta z aplikacji korzystających z przeglądarki, które nie obsługują nowoczesnego uwierzytelniania, muszą utworzyć hasła aplikacji. Możesz również uwzględnić łącze do [przewodnik dla użytkowników końcowych usługi Azure MFA](./end-user/multi-factor-authentication-end-user.md) ułatwiającego rozpoczęcie pracy.

### <a name="use-powershell"></a>Korzystanie z programu PowerShell
Aby zmienić stan użytkownika przy użyciu [programu Azure AD PowerShell](/powershell/azure/overview), zmień `$st.State`. Istnieją trzy stany:

* Enabled (Włączony)
* Enforced (Wymuszony)
* Disabled (Wyłączony)  

Nie przenoś bezpośrednio do użytkowników *wymuszone* stanu. Jeśli to zrobisz, nie opartych na przeglądarce aplikacji przestają działać, ponieważ użytkownik nie ma przeszli rejestracji usługi Azure MFA i uzyskać [hasła aplikacji](multi-factor-authentication-whats-next.md#app-passwords). 

Przy użyciu programu PowerShell jest dobrym rozwiązaniem, gdy konieczne jest umożliwienie użytkownikom zbiorczego. Utwórz skrypt programu PowerShell w pętli listę użytkowników i umożliwia ich:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Poniższy skrypt to przykład:

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

_Dostęp warunkowy_ jest płatnych funkcji usługi Azure Active Directory o wiele opcji konfiguracji. Te kroki przeprowadzenie jedną z metod tworzenia zasad. Aby uzyskać więcej informacji, przeczytaj o [dostępu warunkowego w usłudze Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) jako administrator.
2. Przejdź do **usługi Azure Active Directory** > **dostępu warunkowego**.
3. Wybierz **nowe zasady**.
4. W obszarze **przypisania**, wybierz pozycję **użytkowników i grup**. Użyj **Include** i **wykluczyć** karty, aby określić, którzy użytkownicy i grupy zasad zarządza.
5. W obszarze **przypisania**, wybierz pozycję **aplikacji w chmurze**. Wybierz uwzględnić **wszystkich aplikacji w chmurze**.
6. W obszarze **dostęp do formantów**, wybierz pozycję **Grant**. Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.
7. Włącz **Włącz zasady** do **na**, a następnie wybierz **zapisać**.

Inne opcje zasad dostępu warunkowego zapewniają możliwość określenia dokładnie w przypadku, gdy weryfikacja dwuetapowa jest wymagana. Na przykład wprowadzisz zasady, takie jak ta: gdy wykonawców próbują uzyskać dostęp do aplikacji zamówień z niezaufanymi sieciami, na urządzeniach, które nie są przyłączone do domeny, wymaga weryfikacji dwuetapowej. 

## <a name="next-steps"></a>Kolejne kroki

- Uzyskać porady na temat [najlepszych rozwiązań dotyczących dostępu warunkowego](../active-directory/active-directory-conditional-access-best-practices.md).

- Zarządzaj ustawieniami usługi Azure Multi-Factor Authentication [użytkowników i urządzeń](multi-factor-authentication-manage-users-and-devices.md).
