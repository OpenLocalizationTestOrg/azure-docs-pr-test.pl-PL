---
title: aaaProblems logowanie tooa aplikacji firmy Microsoft | Dokumentacja firmy Microsoft
description: "Rozwiązywanie typowych problemów, które muszą ponieść przy logowaniu się w toofirst firmy Microsoft Applications przy użyciu usługi Azure AD (takich jak usługi Office 365)"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problemy przy logowaniu tooa aplikacji firmy Microsoft

Microsoft Applications (takich jak Office 365 Exchange, SharePoint, Yammer itp.) są przypisane i zarządzane nieco inaczej niż 3 aplikacji SaaS innych producentów i inne aplikacje, które integracji z usługą Azure AD na logowanie jednokrotne w.

Istnieją trzy sposoby, które użytkownik może uzyskać dostęp tooa firma Microsoft opublikowała aplikacji.

-   W przypadku aplikacji hello usługi Office 365 lub innych mechanizmów płatną użytkownicy uzyskują dostęp za pośrednictwem **przypisania licencji** albo bezpośrednio tootheir konta użytkownika, a lub za pośrednictwem grupy za pomocą naszych możliwość przypisania na podstawie grupy licencji.

-   W przypadku aplikacji czy firmy Microsoft lub stron trzecich publikuje za darmo dla każdego toouse użytkownicy mogą otrzymać dostęp za pośrednictwem **zgody użytkownika**. This0 oznacza Zaloguj toohello aplikacji przy użyciu swojego konta usługi Azure AD pracy lub nauki i umożliwić jego toohave dostępu toosome ograniczony zestaw danych na koncie.

-   W przypadku aplikacji czy firmy Microsoft lub 3rd Strona publikuje za darmo dla każdego toouse użytkownicy mogą również uzyskać dostęp za pośrednictwem **zgody administratora**. Oznacza to, że administrator wykrył, że aplikacja hello mogą być używane przez wszyscy użytkownicy w organizacji hello, zaloguj się w aplikacji toohello przy użyciu konta administratora globalnego i przyznać dostęp tooeveryone w organizacji hello.

tootroubleshoot problemu, rozpoczyna się od hello [ogólne obszarów problemów z tooconsider dostęp do aplikacji](#general-problem-areas-with-application-access-to-consider) , a następnie odczytywane hello [wskazówki: tootroubleshoot kroki Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget hello uzyskać szczegółowe informacje.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Ogólne obszarów problemów z tooconsider dostęp do aplikacji

Poniżej znajduje się lista hello obszarów problemów ogólne, które można wejść do, jeśli masz informacje o tym, gdzie toostart, ale firma Microsoft zaleca się przeczytanie tooget wskazówki hello szybkie przechodzenie: [wskazówki: tootroubleshoot kroki Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problemy z kontem użytkownika hello](#problems-with-the-users-account)

-   [Problemy z grupy](#problems-with-groups)

-   [Problemy z zasadami dostępu warunkowego](#problems-with-conditional-access-policies)

-   [Problemy z zgody aplikacji](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Kroki tootroubleshoot Microsoft Application dostępu

Poniżej są niektóre typowe problemy pracowników wystąpiły podczas ich nie logowania tooa aplikacji firmy Microsoft.

-   Ogólne problemy toocheck najpierw

  * Upewnij się, że hello użytkownik loguje się toohello **Popraw adres URL** , a nie adres URL lokalnej aplikacji.

  * Upewnij się, że konto użytkownika hello jest **bez blokady.**

  * Upewnij się, że hello **konto użytkownika istnieje** w usłudze Azure Active Directory. [Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory](#problems-with-the-users-account)

  * Upewnij się, że konto użytkownika hello jest **włączone** dla logowania. [Sprawdź stan konta użytkownika](#problems-with-the-users-account)

  * Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.** [Resetuj hasło użytkownika](#reset-a-users-password) lub [włączyć samoobsługowe Resetowanie hasła](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika. [Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)

   * Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika. [Sprawdź zasady dostępu warunkowego określonych](#problems-with-conditional-access-policies) lub [Sprawdź zasady dostępu warunkowego określonej aplikacji](#check-a-specific-applications-conditional-access-policy) lub [zasad dostępu warunkowego określonych wyłączone](#disable-a-specific-conditional-access-policy)

   * Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane. [Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)

-   Aby uzyskać **Microsoft** **aplikacje, które wymagają licencji** (takich jak usługi Office 365), poniżej przedstawiono niektóre toocheck określonych problemów po zostały wykluczone powyższe problemy ogólne hello:

   * Upewnij się, hello użytkownika lub ma **przypisanej licencji.** [Sprawdź przypisane licencje użytkownika](#check-a-users-assigned-licenses) lub [Sprawdź grupy przypisane licencje.](#check-a-groups-assigned-licenses)

   * Jeśli jest licencja hello **przypisane tooa** **Grupa statyczna**, upewnij się, że hello **użytkownik jest członkiem** tej grupy. [Sprawdzanie członkostwa w grupach użytkownika](#check-a-users-group-memberships)

   * W przypadku licencji hello **przypisane tooa** **Dynamiczna grupa**, upewnij się, że hello **grupa dynamiczna reguła została poprawnie ustawiona**. [Sprawdź kryteria członkostwa grupy dynamicznej](#check-a-dynamic-groups-membership-criteria)

   * Jeśli licencja hello jest **przypisane tooa** **Dynamiczna grupa**, upewnij się, że hello grupa dynamiczna ma **zakończyło się przetwarzanie** członkostwa i że hello **jest użytkownik element członkowski** (może to zająć pewien czas). [Sprawdzanie członkostwa w grupach użytkownika](#check-a-users-group-memberships)

   *  Po wprowadzeniu się licencji hello jest przypisany, upewnij się, że licencja hello jest **niewygasły**.

   *  Upewnij się, że licencja hello jest **dla aplikacji hello** uzyskują oni dostęp.

-   Dla **Microsoft** **aplikacje, które nie wymagają licencji**, w tym miejscu są inne toocheck rzeczy:

   * Jeśli aplikacja hello żąda **uprawnienia na poziomie użytkownika** (na przykład "dostęp do skrzynek pocztowych użytkowników"), upewnij się, że ten użytkownik hello zalogował się toohello aplikacji i wykonał **operacji zgody na poziomie użytkownika**  aplikacja hello toolet dostęp do swoich danych.

   * Jeśli aplikacja hello żąda **uprawnień na poziomie administratora** (na przykład "dostęp do skrzynek pocztowych wszystkich użytkowników"), upewnij się, że przeprowadził administratora globalnego **operacja zgody na poziomie administratora imieniu wszyscy użytkownicy** hello organizacji.

## <a name="problems-with-hello-users-account"></a>Problemy z kontem użytkownika hello

Dostęp do aplikacji mogą zostać zablokowane powodu tooa problem z użytkownika, który jest przypisany toohello aplikacji. Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:

-   [Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Sprawdź stan konta użytkownika](#check-a-users-account-status)

-   [Resetowanie hasła użytkownika](#reset-a-users-password)

-   [Włącz samoobsługowe resetowanie haseł](#enable-self-service-password-reset)

-   [Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status)

-   [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)

-   [Sprawdzanie członkostwa w grupach użytkownika](#check-a-users-group-memberships)

-   [Sprawdź przypisane licencje użytkownika](#check-a-users-assigned-licenses)

-   [Przypisywanie licencji użytkownika](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory

toocheck, jeśli konto użytkownika jest obecny, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Sprawdź właściwości hello hello użytkownika obiektu toobe się upewnić, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.

### <a name="check-a-users-account-status"></a>Sprawdź stan konta użytkownika

toocheck użytkownika konta stanu, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **profilu**.

8.  W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono zbyt**nr**.

### <a name="reset-a-users-password"></a>Resetowanie hasła użytkownika

tooreset hasło użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk hello **resetowania hasła** przycisk u góry bloku użytkownika hello hello.

8.  Kliknij przycisk hello **resetowania hasła** przycisk na powitania **resetowania hasła** wyświetlonym bloku.

9.  Kopiuj hello **hasło tymczasowe** lub **wprowadź nowe hasło** hello użytkownika.

10. Komunikować się z nowym użytkowniku toohello hasła, one toochange wymagane hasło podczas następnego Zaloguj tooAzure usługi Active Directory.

### <a name="enable-self-service-password-reset"></a>Włącz samoobsługowe Resetowanie hasła

hasło samoobsługi tooenable resetowania, wykonaj poniższe kroki wdrażania hello:

-   [Włącz użytkowników tooreset swoich haseł w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Włącz tooreset użytkowników lub zmieniać swoje hasła lokalnej usługi Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Sprawdź stan usługi Multi-Factor authentication użytkownika

toocheck użytkownika do usługi Multi-Factor stanu uwierzytelniania, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  Kliknij przycisk hello **uwierzytelnianie wieloskładnikowe** u góry hello hello bloku.

7.  Raz hello **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, znajdują się na powitania **użytkowników** kartę.

8.  Znajdź użytkownika hello hello listy użytkowników przez wyszukiwanie, filtrowanie i sortowanie.

9.  Wybierz hello użytkownika z listy hello użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.

  * **Uwaga**: Jeśli użytkownik znajduje się w **wymuszone** stanu może ustawić je także**wyłączone** tymczasowo toolet je z powrotem do swojego konta. Gdy są one ponownie, można zmienić stanu za**włączone** ponownie toorequire je zarejestrować toore, zaloguj się do niego swoje informacje kontaktowe podczas następnego. Alternatywnie można wykonać kroki hello w hello [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) tooverify lub ustaw dla nich dane.

### <a name="check-a-users-authentication-contact-info"></a>Sprawdź informacje kontaktowe uwierzytelniania użytkownika

toocheck uwierzytelniania użytkownika informacje używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania haseł, skontaktuj się z pomocą wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **profilu**.

8.  Przewiń w dół za**informacje kontaktowe uwierzytelniania**.

9.  **Przegląd** hello danych zarejestrowane dla użytkownika hello i aktualizacji, zgodnie z potrzebami.

### <a name="check-a-users-group-memberships"></a>Sprawdzanie członkostwa w grupach użytkownika

toocheck użytkownika członkostw, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **grup** toosee, który grupuje hello użytkownika jest członkiem.

### <a name="check-a-users-assigned-licenses"></a>Sprawdź przypisane licencje użytkownika

toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.

### <a name="assign-a-user-a-license"></a>Przypisywanie licencji użytkownika 

tooassign tooa licencji użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.

8.  Kliknij przycisk hello **przypisać** przycisku.

9.  Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.

10. **Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów. Kliknij przycisk **Ok** po zakończeniu.

11. Kliknij przycisk hello **przypisać** przycisk tooassign użytkownika toothis tych licencji.

## <a name="problems-with-groups"></a>Problemy z grupy

Dostęp do aplikacji mogą zostać zablokowane powodu tooa problem z grupy, która jest przypisany toohello aplikacji. Poniżej przedstawiono kilka sposobów, można rozwiązać i rozwiązać problemy z grupy i członkostwa w grupach:

-   [Sprawdź członkostwo w grupie](#check-a-groups-membership)

-   [Sprawdź kryteria członkostwa grupy dynamicznej](#check-a-dynamic-groups-membership-criteria)

-   [Sprawdź grupy przypisane licencje.](#check-a-groups-assigned-licenses)

-   [Ponownie przetworzyć grupy licencji](#reprocess-a-groups-licenses)

-   [Przypisz grupę licencji](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Sprawdź członkostwo w grupie

toocheck członkostwa w grupie, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkich grup**.

6.  **Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **członków** tooreview hello listę użytkowników przypisane toothis grupy.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Sprawdź kryteria członkostwa grupy dynamicznej 

toocheck kryteria członkostwa grupy dynamicznej, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkich grup**.

6.  **Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **członkostwo dynamiczne reguły.**

8.  Przejrzyj hello **proste** lub **zaawansowane** reguły zdefiniowane dla tej grupy i upewnij się, hello ma toobe członkiem tej grupy użytkownika spełnia te kryteria.

### <a name="check-a-groups-assigned-licenses"></a>Sprawdź grupy przypisane licencje.

toocheck grupy przypisane licencje, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkich grup**.

6.  **Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.

### <a name="reprocess-a-groups-licenses"></a>Ponownie przetworzyć grupy licencji

tooreprocess grupy przypisane licencje, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkich grup**.

6.  **Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.

8.  Kliknij przycisk hello **ponownie przetworzyć** tooensure przycisku, który hello członków grupy licencji przypisanych toothis są aktualne. Może to zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy.

   >[!NOTE]
   >toodo to szybsze, należy wziąć pod uwagę tymczasowo przypisywanie licencji użytkownika toohello bezpośrednio. [Przypisywanie licencji użytkownika](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Przypisz grupę licencji

tooassign tooa grupę licencji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkich grup**.

6.  **Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.

8.  Kliknij przycisk hello **przypisać** przycisku.

9.  Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.

10. **Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów. Kliknij przycisk **Ok** po zakończeniu.

11. Kliknij przycisk hello **przypisać** przycisk tooassign grupy toothis tych licencji. Może to zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy.

   >[!NOTE]
   >toodo to szybsze, należy wziąć pod uwagę tymczasowo przypisywanie licencji użytkownika toohello bezpośrednio. [Przypisywanie licencji użytkownika](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problemy z zasadami dostępu warunkowego

### <a name="check-a-specific-conditional-access-policy"></a>Sprawdzanie zasad określonych dostępu warunkowego

toocheck albo do sprawdzania zasad pojedynczego dostępu warunkowego:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.

5.  Kliknij przycisk hello **dostępu warunkowego** element nawigacji.

6.  Kliknij zasady hello myślisz sprawdzania.

7.  Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.

   >[!NOTE]
   >Możesz wyłączyć tootemporarily to tooensure zasad go nie wpływają na znak ubezp toodo hello tego zestawu **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Sprawdź zasady dostępu warunkowego określonej aplikacji

toocheck albo do sprawdzania zasad aktualnie skonfigurowany dostęp warunkowy pojedynczej aplikacji:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.

5.  Kliknij przycisk **wszystkie aplikacje**.

6.  Wyszukiwanie aplikacji hello interesuje lub hello użytkownik próbuje toosign w aplikacji tooby wyświetlanie identyfikatora aplikacji lub nazwa.

     >[!NOTE]
     >Jeśli nie widzisz aplikacji hello, którego szukasz, kliknij przycisk hello **filtru** przycisk i zwiększa zakresu hello listy hello zbyt**wszystkie aplikacje**. Toosee więcej kolumn, kliknij przycisk hello **kolumn** przycisk tooadd dodatkowe szczegóły dla aplikacji.
     >
     >

7.  Kliknij przycisk hello **dostępu warunkowego** element nawigacji.

8.  Kliknij zasady hello myślisz sprawdzania.

9.  Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.

     >[!NOTE]
     >Możesz wyłączyć tootemporarily to tooensure zasad go nie wpływają na znak ubezp toodo hello tego zestawu **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Wyłącz zasady dostępu warunkowego określonych

toocheck albo do sprawdzania zasad pojedynczego dostępu warunkowego:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.

5.  Kliknij przycisk hello **dostępu warunkowego** element nawigacji.

6.  Kliknij zasady hello myślisz sprawdzania.

7.  Wyłącz zasady hello przez ustawienie hello **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisk.

## <a name="problems-with-application-consent"></a>Problemy z zgody aplikacji

Dostęp do aplikacji mogą zostać zablokowane, ponieważ nie przeprowadzono hello odpowiednich uprawnień zgodą operacji. Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywaniu problemów zgody aplikacji:

-   [Wykonanie operacji zgody na poziomie użytkownika](#perform-a-user-level-consent-operation)

-   [Operacja zgody na poziomie administratora dla dowolnej aplikacji](#perform-administrator-level-consent-operation-for-any-application)

-   [Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Wykonanie operacji zgody na poziomie użytkownika

-   Dla dowolnego Open ID Connect aplikacja obsługująca żąda uprawnień nawigowanie po znaku toohello aplikacji na ekranie wykonuje aplikacji toohello poziomu zgody użytkownika hello zalogowanego użytkownika.

-   Jeśli chcesz toodo to programowo, zobacz [żąda zgody użytkownika](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Operacja zgody na poziomie administratora dla dowolnej aplikacji

-   Dla **tylko aplikacje opracowane za pomocą modelu aplikacji hello V1**, możesz wymusić ten toooccur poziomu zgody administratora, dodając "**? prompt = admin\_zgody**" toohello koniec Zaloguj się adres URL aplikacji.

-   Dla **dowolnej aplikacji utworzony przy użyciu modelu aplikacji hello V2**, wykonując instrukcje hello w obszarze hello można wymusić ten toooccur zgody na poziomie administratora **zażądać uprawnień hello z katalogu Administrator** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy

-   Dla **aplikacji pojedynczej dzierżawy** który zażądać uprawnień (np. te opracowujesz lub własny w organizacji), można wykonać **zgody na poziomie administracyjnym** operacji imieniu wszystkie Użytkownicy zalogować się jako Administrator globalny i klikając hello **udzielić uprawnień** u góry hello hello **rejestru aplikacji -&gt; wszystkie aplikacje —&gt; wybierz aplikację - &gt; Wymagane uprawnienia** bloku.

-   Dla **dowolnej aplikacji utworzony przy użyciu hello V1 lub V2 modelu aplikacji**, wykonując instrukcje hello w obszarze hello można wymusić ten toooccur zgody na poziomie administratora **zażądać uprawnień hello z Administrator katalogu** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji

-   Dla **aplikacje wielodostępne** tego zażądać uprawnień (np. aplikacji innej firmy lub firmy Microsoft, które zostały zaakceptowane), można wykonać **zgody na poziomie administracyjnym** operacji. Zaloguj się jako Administrator globalny i klikając hello **udzielić uprawnień** przycisku w obszarze hello **aplikacje przedsiębiorstwa -&gt; wszystkie aplikacje —&gt; wybierz aplikację -&gt; Uprawnienia** bloku (dostępne wkrótce).

-   Może również wymuszać toooccur tej zgody na poziomie administratora, wykonując instrukcje hello w obszarze hello **poprosić hello uprawnienia administratora katalogu** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Następne kroki
[Przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

