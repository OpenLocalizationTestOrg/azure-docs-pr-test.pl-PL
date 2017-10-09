---
title: "aaaHow aplikacje pojawiają się na panelu dostępu hello | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z niemożnością aplikacji pojawia się w hello panelu dostępu"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Jak aplikacje pojawiają się na powitania panelu dostępu

Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do. Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello. Witaj, Administratorze można udostępnić użytkownika toohello aplikacji hello bezpośrednio lub tooa grupę, którą użytkownik wchodzi w skład powodujące aplikacji hello znajdujących się w panelu dostępu hello użytkownika.

## <a name="general-issues-toocheck-first"></a>Ogólne problemy toocheck najpierw

-   Jeśli aplikacja właśnie został usunięty przez użytkownika lub grupy hello użytkownik jest członkiem, spróbuj toosign i wylogowywanie ponownie do panelu dostępu użytkownika powitania po kilku minutach toosee usunięcie aplikacji hello.

-   Jeśli licencji właśnie został usunięty z użytkownik lub grupa hello użytkownik jest członkiem to może zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy toobe zmiany wprowadzone. Zezwalaj na dodatkowy czas przed zalogowaniem się do hello panelu dostępu.

## <a name="problems-related-tooassigning-applications-toousers"></a>Toousers aplikacji powiązanych tooassigning problemów

Użytkownik może być widoczny aplikacji na ich panelu dostępu ponieważ one była wcześniej przypisane tooit. Poniżej przedstawiono niektóre toocheck sposobów:

-   [Sprawdź, czy użytkownik jest przypisany toohello aplikacji](#check-if-a-user-is-assigned-to-the-application)

-   [Sprawdź, czy użytkownik jest objętych licencją powiązane toohello aplikacji](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Sprawdź, czy użytkownik jest przypisany toohello aplikacji

toocheck Jeśli użytkownik jest przypisany toohello aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

6.  **Wyszukiwanie** hello nazwy aplikacji hello jest zagrożona.

7.  Kliknij przycisk **użytkowników i grup**.

8.  Określ, czy toosee użytkownikowi przypisano toohello aplikacji.

  * Jeśli użytkownik hello tooremove z aplikacji hello **kliknij wiersz hello** hello użytkownika i wybierz **usunąć**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Sprawdź, czy użytkownik jest objętych licencją powiązane toohello aplikacji

toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.

   * Jeśli użytkownik hello jest tooan przypisanej licencji pakietu Office to włączenie tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Toogroups aplikacji powiązanych tooassigning problemów

Użytkownik może być widoczny aplikacji na ich Panel dostępu, ponieważ są one częścią grupy przypisanej do aplikacji hello. Poniżej przedstawiono niektóre toocheck sposobów:

-   [Sprawdzanie członkostwa w grupach użytkownika](#check-a-users-group-memberships)

-   [Sprawdź, czy użytkownik jest członkiem grupy przypisane tooa licencji](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Sprawdzanie członkostwa w grupach użytkownika

toocheck członkostwa w grupie, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **grup.**

8.  Określ, czy toosee użytkownika jest częścią grupy przypisane toohello aplikacji.

   * Jeśli chcesz, aby tooremove hello użytkownika z grupy hello **kliknij wiersz hello** hello grupy i wybierz opcję Usuń.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Sprawdź, czy użytkownik jest członkiem grupy przypisane tooa licencji

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **grup.**

8.  Kliknij wiersz hello określonej grupy.

9.  Kliknij przycisk **licencji** toosee grupy hello licencji, do której przypisany tooit.

  * Jeśli grupa hello jest tooan przypisanej licencji pakietu Office może to włączenie niektórych tooappear aplikacji pierwszej strony pakietu Office na panelu dostępu hello użytkownika.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Identyfikator dzierżawy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
