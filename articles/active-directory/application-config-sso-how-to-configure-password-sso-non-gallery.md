---
title: "aaaHow tooconfigure hasło rejestracji jednokrotnej dla applicationn z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure niestandardowych aplikacji z systemem innym niż galerii dla należy zabezpieczyć opartego na hasłach logowania jednokrotnego nie znajduje się w hello galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii

Ponadto opcji toohello znaleziono w galerii aplikacji hello Azure AD, masz również tooadd opcji hello **aplikacji z systemem innym niż galerii** gdy aplikacja hello ma nie ma na liście istnieje. Przy użyciu tej możliwości, możesz dodać dowolnej aplikacji, która już istnieje w danej organizacji lub dowolnej aplikacji innych firm, z którego można korzystać z dostawcy, który nie jest już częścią hello [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Po dodaniu aplikacji z systemem innym niż galerii, następnie można skonfigurować hello pojedynczego logowania jednokrotnego — metoda korzysta z tej aplikacji, wybierając hello **rejestracji jednokrotnej** element nawigacji w aplikacji przedsiębiorstwa w hello [portalu Azure ](https://portal.azure.com/).

Jednym z hello rejestracji jednokrotnej metody dostępne tooyou jest hello [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opcji. Z hello **dodania aplikacji z systemem innym niż galerii** doświadczenia, można je zintegrować w dowolnej aplikacji, która renderuje oparty na języku HTML nazwy użytkownika i hasła, wprowadź pola, nawet jeśli nie jest w naszym zestawie wstępnie zintegrowanych aplikacji.

to działanie jest metodą Hello jest strona oskrobaniu technologii, która jest częścią hello rozszerzenia Panelu dostępu, który pozwala nam tooauto-wykryć pól wejściowych użytkownika i hasło, bezpieczne przechowywanie dla swojego wystąpienia określonej aplikacji. Bezpiecznie powtarzania nazw użytkowników i haseł toothose pola, gdy użytkownik nawiguje toothat aplikacji na panelu dostępu aplikacji hello.

Jest to doskonały sposób tooget uruchomić szybkie włączenie dowolnego rodzaju aplikacji do usługi Azure AD i umożliwia:

-   Integracja **aplikacje w Witaj świecie** z dzierżawy usługi Azure AD, ile renderowania HTML nazwy użytkownika i hasła pola wejściowego

-   Włącz **rejestracji jednokrotnej dla użytkowników** bezpieczne przechowywanie i odtwarzanie nazwy użytkowników i hasła dla aplikacji hello zostały zintegrowane z usługą Azure AD

-   **Autowykrywanie wprowadzania** pól dla każdej aplikacji i pozwala toomanually wykryć tych pól przy użyciu hello rozszerzenia przeglądarki Panel dostępu, w przypadku automatycznego wykrywania ich nie znajdzie

-   **Obsługuje aplikacje, które wymagają wielu pól logowania** dla aplikacji, które wymagają więcej niż tylko nazwę użytkownika i hasło pola toosign w

-   **Dostosowywanie etykiet hello** hello nazwy użytkownika i hasła wejściowych użytkownicy zobaczą na powitania [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) po oni wprowadzić swoje poświadczenia

-   Zezwalaj na Twojej **użytkowników** tooprovide własne nazwy użytkowników i hasła dla wszystkich istniejących kont aplikacji wpisywania w ręcznie na powitania [Panel dostępu do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Zezwalaj na **grupy biznesowej hello** toospecify hello w nazwach użytkowników i haseł przypisany użytkownik tooa przy użyciu hello [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funkcji

-   Zezwalaj na **administratora** toospecify hello w nazwach użytkowników i haseł przypisany użytkownik tooa przy użyciu poświadczeń aktualizacji hello funkcji podczas [przypisywanie aplikacji tooan użytkownika](#_How_to_configure_1)

-   Zezwalaj na **administratora** toospecify hello udostępnionych w nazwa użytkownika lub hasło używane przez grupy osób przy użyciu poświadczeń aktualizacji hello funkcji podczas [przypisanie grupy aplikacji tooan](#assign-an-application-to-a-group-directly)

Poniżej opisano, jak można włączyć [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) aplikacji tooany dodać za pomocą hello **dodania aplikacji z systemem innym niż galerii** wystąpić.

## <a name="overview-of-steps-required"></a>Omówienie kroków wymaganych

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji z systemem innym niż galerii](#add-a-non-gallery-application)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

-   [Przypisz hello aplikacji tooa użytkownika lub grupy](#assign-the-application-to-a-user-or-a-group)

    -   [Bezpośrednio przypisać aplikację tooan użytkownika](#assign-a-user-to-an-application-directly)

    -   [Przypisz grupę tooa aplikacji bezpośrednio](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Dodawanie aplikacji z systemem innym niż galerii

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku

6.  Kliknij przycisk **Non galerii aplikacji.**

7.  Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego. Wybierz **dodać.**

Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego

tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  Wprowadź hello **adres URL logowania**. Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu. Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.

10. Przypisywanie użytkowników toohello aplikacji.

11. Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello. W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.

## <a name="assign-a-user-tooan-application-directly"></a>Bezpośrednio przypisać aplikację tooan użytkownika

tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.

9.  Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.

10. Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**. Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.

12. **Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.

13. Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.

14. **Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.

15. Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.

## <a name="assign-an-application-tooa-group-directly"></a>Przypisz grupę tooa aplikacji bezpośrednio

tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.

9.  Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.

10. Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**. Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.

12. **Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.

13. Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.

14. **Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.

15. Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.

Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
