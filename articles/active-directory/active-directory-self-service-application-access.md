---
title: "dostęp do aplikacji usługi aaaSelf i delegowane zarządzanie za pomocą usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak uzyskać dostęp do aplikacji Sklep internetowy tooenable i delegowane zarządzanie za pomocą usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Dostęp do aplikacji Sklep internetowy i delegowane zarządzanie za pomocą usługi Azure Active Directory
Włączenie funkcji samoobsługi dla użytkowników końcowych jest typowym scenariuszem dla organizacji IT. Wielu użytkowników, wiele aplikacji i hello osoba best-informed dostępu toomake Przydziel decyzji może nie być hello administratora katalogu. Realizacji zespołu lub innych administratora delegowanego jest często hello najlepsze osoby toodecide kto ma dostęp do aplikacji. Jest jednak hello użytkownika, który korzysta z aplikacji hello i hello użytkownik wie, co potrzebują toobe toodo stanie ich zadania.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. 

Dostęp do aplikacji Sklep internetowy jest funkcją [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 i P2 licencjonowania, która pozwala administratorom katalogu:

* Włącz dostęp toorequest użytkowników przy użyciu "Pobierz więcej aplikacji" tooapplications kafelka w hello [Panel dostępu usługi Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Zestaw, do których aplikacji użytkownicy mogą żądać dostępu do
* Ustaw czy zatwierdzenia jest wymagana dla użytkowników toobe można przypisać tooself dostępu tooan aplikacji
* Zestaw, który należy zatwierdzać żądania hello i zarządzanie dostępem dla każdej aplikacji

Obecnie ta funkcja jest obsługiwana dla wszystkich wstępnie zintegrowanych i niestandardowych aplikacji obsługujących federacyjnych lub opartego na hasłach rejestracji jednokrotnej w hello [galerii aplikacji usługi Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/), w tym aplikacji, takich jak Salesforce, Dropbox, Usługi Google Apps i inne.
W tym artykule opisano sposób:

* Konfigurowanie dostępu do aplikacji Sklep internetowy dla użytkowników końcowych, łącznie z konfigurowaniem zatwierdzeń opcjonalnych przepływu pracy 
* Delegowanie zarządzanie dostępem dla określonych aplikacji toohello najbardziej odpowiednie osoby w Twojej organizacji i je włączyć żądania dostępu tooapprove panelu dostępu toouse hello Azure AD, bezpośrednio przypisać dostęp użytkowników tooselected i (opcjonalnie) poświadczenia dostępu do aplikacji podczas opartego na hasłach rejestracji jednokrotnej jest skonfigurowany

## <a name="configuring-self-service-application-access"></a>Konfigurowanie dostępu do aplikacji Sklep internetowy
dostęp do aplikacji Sklep internetowy tooenable i skonfigurować aplikacje, które można dodać lub żądane przez użytkowników końcowych, wykonaj te instrukcje.

1. Zaloguj się na powitania [klasycznego portalu Azure](https://manage.windowsazure.com/).

2.   W obszarze hello **usługi Active Directory** sekcji, wybierz swój katalog, a następnie wybierz hello **aplikacji** kartę. 

3. Wybierz hello **Dodaj** przycisk i użyj hello galerii opcji tooselect i dodać aplikację.

4. Po dodaniu aplikacji można uzyskać strony Szybki Start aplikacji hello. Kliknij przycisk **skonfigurować logowanie jednokrotne**, wybierz hello żądaną logowania jednokrotnego tryb pojedynczy i Zapisz konfigurację hello. 

5. Następnie wybierz pozycję hello **Konfiguruj** kartę tooenable użytkowników toorequest toothis aplikacji dostępu z poziomu panelu dostępu hello Azure AD, ustaw **Zezwalaj na dostęp do aplikacji Sklep internetowy** zbyt**tak**.
  
  ![][1]

6. toooptionally Konfigurowanie zatwierdzania żądań dostępu, ustaw **wymagają zatwierdzenia przed udzieleniem im dostępu** za**tak**. Następnie można wybrać jedną lub więcej osób zatwierdzających za pomocą hello **osób zatwierdzających** przycisku.

  Osoba zatwierdzająca może być dowolny użytkownik w organizacji hello przy użyciu konta usługi Azure AD i może być odpowiedzialny za inicjowanie obsługi kont, licencjonowania, lub inne procesy biznesowe organizacja wymaga przed udzieleniem im dostępu tooan aplikacji. Osoba zatwierdzająca Hello można nawet hello właściciel grupy co najmniej jednego udostępnionego konta grup i przypisanie hello tooone użytkowników o toogive tych grup, których ich dostęp za pośrednictwem udostępnionego konta. 

  Jeśli nie zatwierdzenia jest wymagana, użytkownicy natychmiast uzyskać panelu dostępu dodano tootheir usługi Azure AD aplikacji hello. Jeśli aplikacja hello została ustawiona dla [użytkownika automatycznego inicjowania obsługi administracyjnej](active-directory-saas-app-provisioning.md), lub nie został skonfigurowany ["zarządzane przez użytkownika" hasło logowania jednokrotnego tryb](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), hello użytkownik ma już użytkownika konta i hasło hello.

7. Jeśli aplikacja hello została skonfigurowana toouse opartego na hasłach rejestracji jednokrotnej, następnie opcję stosowanie poświadczeń logowania jednokrotnego hello tooset imieniu każdego użytkownika osoba zatwierdzająca hello jest również dostępna. Aby uzyskać więcej informacji, zobacz sekcję hello na [delegowane zarządzanie dostępem](#delegated-application-access-management).

8. Na koniec hello **grupy użytkowników Self-Assigned** pokazuje hello nazwę grupy hello, która jest używana toostore hello użytkowników, którzy zostały przyznane lub przypisać dostępu toohello aplikacji. Osoba zatwierdzająca dostępu Hello staje się właścicielem hello tej grupy. Jeśli nazwa grupy hello pokazano nie istnieje, jest tworzona automatycznie. Opcjonalnie hello Nazwa grupy można ustawić toohello nazwę istniejącej grupy.

9. toosave hello konfiguracji, kliknij przycisk **zapisać** u dołu hello hello ekranu. Użytkownicy mogą teraz toorequest dostępu toothis aplikacji hello panelu dostępu.

10. środowisko użytkownika końcowego hello tootry, zaloguj się do panelu dostępu usługi Azure AD w organizacji pod adresem https://myapps.microsoft.com, najlepiej przy użyciu innego konta, która nie jest osobą zatwierdzającą aplikacji. 

11. W obszarze hello **aplikacji** , kliknij pozycję hello **Pobierz więcej aplikacje** kafelka. Ten Kafelek Wyświetla galerii wszystkich aplikacji hello, które zostały włączone samoobsługi dostępu do aplikacji w katalogu hello hello możliwości toosearch i Filtruj według kategorii aplikacji hello po lewej stronie. 

12. Kliknięcie aplikacji rozpoczyna przetwarzanie żądania hello. Jeśli nie jest wymagany żaden proces zatwierdzania, a następnie aplikacja hello natychmiast dodany w obszarze hello **aplikacji** kartę po krótkim potwierdzenia. Jeśli zatwierdzenia jest wymagana, czym pojawi się okno dialogowe tego wskazująca i osób zatwierdzających toohello zostanie wysłana wiadomość e-mail. Użytkownik musi zalogować się do hello dostępu panelu jako toosee z systemem innym niż osoba zatwierdzająca ten proces żądania.

13. e-mail Hello kieruje toosign osoba zatwierdzająca hello do panelu dostępu do usługi Azure AD hello i zatwierdzić Żądanie hello. Po hello żądanie zostanie zatwierdzone i wszelkie specjalne procesy, należy zdefiniować mogły zostać wykonane przez osoby zatwierdzającej hello, hello użytkownik widzi aplikacji hello są wyświetlane w obszarze ich **aplikacji** kartę, której można zalogować do niego.

## <a name="delegated-application-access-management"></a>Zarządzanie dostępem aplikacji delegowanego
Osoba zatwierdzająca dostępu aplikacji można każdy użytkownik w organizacji, który jest najbardziej odpowiednia tooapprove osoby hello lub odmówić dostępu toohello aplikacji. Ten użytkownik może być odpowiedzialny za inicjowanie obsługi konta licencjonowania, lub inne proces biznesowy organizacja wymaga przed udzieleniem im dostępu tooan aplikacji.

Podczas konfigurowania dostępu aplikacji samoobsługi opisane powyżej, wszelkie przypisane aplikacji, zobacz osób zatwierdzających dodatkowe **Zarządzanie aplikacjami** kafelka w panelu dostępu hello Azure AD, które zawiera ich aplikacji, które mają uzyskać Hello dostępu administratora. Kliknięcie aplikacji powoduje wyświetlenie ekranu z kilku opcji.

![][2]

### <a name="approve-requests"></a>Zatwierdzanie żądań
Witaj **zatwierdzanie żądań** kafelka umożliwia osób zatwierdzających toosee oczekujących zatwierdzeń toothat określonych aplikacji i przekierowuje toohello zatwierdzenia kartę, gdy zażąda hello potwierdzone lub odrzucone. zawsze, gdy żądanie jest tworzony, która sprawia, że ich jakie toodo osoba zatwierdzająca Hello Ponadto otrzymuje zautomatyzowane wiadomości e-mail.

### <a name="add-users"></a>Dodawanie użytkowników
Witaj **Dodaj użytkowników** kafelka umożliwia osób zatwierdzających toodirectly grant wybrane użytkowników dostępu toohello aplikacji. Po kliknięciu tego kafelka, osoba zatwierdzająca hello widzi się, że okno dialogowe umożliwia im tooview i Wyszukaj użytkowników w ich katalogu. Dodawanie wyników użytkownika w aplikacji hello jest pokazywany w tych użytkowników usługi Azure AD dostęp paneli lub usługi Office 365. Jeśli wymagana jest dowolny użytkownik ręcznego procesu udostępniania w aplikacji hello zanim użytkownik hello jest możliwe toosign w, a następnie osoba zatwierdzająca hello należy to zrobić przed udzieleniem im dostępu.  

### <a name="manage-users"></a>Zarządzanie użytkownikami
Witaj **Zarządzanie użytkownikami** kafelka umożliwia osób zatwierdzających toodirectly aktualizacji lub usuń użytkowników, którzy mają dostęp do aplikacji toohello. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Skonfiguruj poświadczenia logowania jednokrotnego hasło (jeśli dotyczy)
Witaj **Konfiguruj** kafelka jest wyświetlana tylko, jeśli aplikacji hello zostały skonfigurowane przez hello IT administrator toouse opartego na hasłach logowania jednokrotnego, a hello administrator przyznane osoba zatwierdzająca hello poświadczenia logowania jednokrotnego hello możliwości tooset hasła jak opisano wcześniej. Po wybraniu hello osoba zatwierdzająca zostanie wyświetlony kilka opcji jak hello poświadczenia są propagowany tooassigned użytkowników:

![][3]

* **Użytkownicy, zaloguj się przy użyciu swoje hasła** — w tym trybie hello przypisane użytkownicy wiedzieli, co ich nazwami użytkowników i hasła są dla aplikacji hello i są tooenter zostanie wyświetlony monit o ich po ich pierwszym aplikacji toohello logowania. Witaj scenariusz odpowiada toohello hasła Usługa rejestracji Jednokrotnej w przypadku gdy hello [zarządzania przez użytkowników poświadczeń](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Użytkownicy są automatycznie logowani przy użyciu osobnych kont, którymi zarządza** — w tym trybie hello przypisanych użytkowników nie są wymagane tooenter lub znać poświadczeń specyficzny dla aplikacji, podczas logowania do aplikacji hello. Zamiast tego, osoba zatwierdzająca hello Ustawia poświadczenia hello dla każdego użytkownika, po przypisaniu dostęp przy użyciu hello **Dodaj użytkownika** kafelka. Gdy użytkownik hello kliknie aplikacji hello w panelu dostępu i usługi Office 365, zostaną automatycznie wylogowani przy użyciu poświadczeń hello ustawione przez osoby zatwierdzającej hello. Witaj scenariusz odpowiada toohello hasła Usługa rejestracji Jednokrotnej w przypadku gdy hello [administratorom zarządzanie poświadczeniami](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Użytkownicy zostaną automatycznie wylogowani za pomocą jednego konta, które mogę zarządzać** -szczególnych przypadkach, przypadkiem jest toouse odpowiednie w przypadku wszystkich użytkowników przypisanych muszą toobe prawa dostępu przy użyciu jednego, udostępnionego konta. Witaj najczęściej przypadek użycia dla tej funkcji jest z aplikacjami mediów społecznościowych, w którym organizacja ma konto pojedynczy "firmy" i wielu użytkowników wymagane jest konto toothat aktualizacje toomake. Hello scenariusz również odpowiada toohello hasła Usługa rejestracji Jednokrotnej w przypadku gdy hello [administratorom zarządzanie poświadczeniami](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Jednak po wybraniu tej opcji, osoba zatwierdzająca hello będą zostanie wyświetlony monit o tooenter hello w nazwę użytkownika i hasło hello jednego, udostępnionego konta. Po ukończeniu wszystkich użytkowników przypisanych jest zalogowany przy użyciu tego konta, po kliknięciu przycisku w aplikacji hello w ich panele dostępu do usługi Azure AD lub usługi Office 365.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
