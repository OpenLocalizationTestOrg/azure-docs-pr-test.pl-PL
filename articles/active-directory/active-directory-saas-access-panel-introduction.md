---
title: "aaaWhat jest hello panelu dostępu w usłudze Azure Active Directory? | Microsoft Docs"
description: "Dowiedz się, jak zmiany toouse hello uzyskują dostęp do panelu (przeglądarki sieci web, aplikacji systemu Android, aplikacji iPhone i iPad) tooaccess aplikacji SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Co to jest hello panelu dostępu?

Witaj panel dostępu jest portalem sieci web. Umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory tooview i rozpocząć aplikacje oparte na chmurze się, że administrator usługi Azure AD udzielił im dostęp do. Można również użyć grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu hello.

panel dostępu Hello jest oddzielony od hello portalu Azure i jest nie możesz toohave subskrypcji platformy Azure.

![Panel dostępu][1]

panel dostępu Hello umożliwia tooedit hello niektóre ustawienia profilu, w tym możliwość:

- Zmień hello hasło skojarzone z kontem służbowym

- Edytuj ustawienia resetowania hasła

- Edytuj kontaktów i preferencji ustawienia pokrewne toomulti uwierzytelniania (dla kont, które są wymagane toouse go przez administratora)

- Wyświetl konta alternatywne szczegóły, takie jak nazwa użytkownika, poczty e-mail oraz mobile i office numery telefonów i urządzeń

- Widok i rozpocząć chmurowych aplikacji, które hello administratora usługi Azure AD udzielił im dostępu do. Aby uzyskać więcej informacji na temat hello panelu dostępu z punktu widzenia użytkownika hello Zobacz przy użyciu hello panelu dostępu. 

- Własnym Zarządzanie grupami. W szczególności hello administrator można tworzyć i zarządzanie grupami zabezpieczeń i żądania członkostwa w grupach zabezpieczeń w usłudze Azure AD. Aby uzyskać więcej informacji, zobacz [Samoobsługowe zarządzanie grupami użytkowników w usłudze Azure AD](active-directory-accessmanagement-self-service-group-management.md) i [Zarządzanie grupami](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Uzyskiwanie dostępu do panelu dostępu hello

Aby dostęp do panelu dostępu hello, odwiedzając hello następującego adresu URL w przeglądarce sieci web:`http://myapps.microsoft.com`

Jeśli masz niestandardowe znakowanie skonfigurowana dla strony logowania, należy załadować tego znakowania przez dołączenie organizacji domeny toohello koniec hello adresu URL:`http://myapps.microsoft.com/<your domain>.com`

W takim przypadku można użyć dowolnej nazwy aktywnych lub zweryfikowanej domeny, skonfigurowanego w portalu Azure.

![Nazwa domeny Wingtip Toys][2]  

Należy toodistribute hello adresu URL tooall użytkowników, którzy będą Zaloguj tooapplications, które są zintegrowane z usługą Azure AD.

## <a name="authentication"></a>Authentication

panel dostępu hello tooreach, użytkownik musi zostać uwierzytelniony przy użyciu konta służbowego w usłudze Azure AD. Może być uwierzytelniony tooAzure AD w bezpośrednio. Alternatywnie Jeśli organizacji skonfigurował Federacji przy użyciu usługi Active Directory Federation Services (AD FS) ani innych technologii, możesz mogą być uwierzytelniane przez usługę Active Directory systemu Windows Server.

Jeśli ma subskrypcji platformy Azure lub usługi Office 365 i był używany hello portalu Azure lub aplikacji pakietu Office 365, zobaczysz listę aplikacji hello bez logowanie się ponownie. Jeśli nie są uwierzytelniane są zostanie wyświetlony monit o toosign w za pomocą hello nazwę użytkownika i hasło dla swojego konta w usłudze Azure AD. Jeśli organizacji skonfigurował Federacji, wpisując nazwę użytkownika hello jest wystarczająca.

Gdy użytkownik jest uwierzytelniony, możesz użyć aplikacji hello, które administrator ma zintegrowane z katalogiem hello. toolearn toointegrate aplikacji za pomocą usługi Azure AD, zobacz temat [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Wymagania dotyczące przeglądarki sieci Web

Co najmniej hello panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. Dla hello toobe użytkownik zalogowany tooapplications za pomocą opartego na hasłach rejestracji jednokrotnej (SSO) rozszerzenia panel dostępu hello musi być zainstalowany w przeglądarce. rozszerzenie Hello jest pobierany automatycznie po wybraniu aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

rozszerzenie panelu dostępu Hello jest obecnie dostępny dla programu Internet Explorer 8 lub nowszy, krawędzi i Chrome, Firefox przeglądarek.

## <a name="mobile-app-support"></a>Obsługa aplikacji mobilnej

Zespół usługi Azure Active Directory Hello publikuje hello mojej aplikacji mobilnej aplikacji. Po zainstalowaniu aplikacji hello może zalogować się toopassword logowania jednokrotnego aplikacji na urządzeniach z systemem Android i iOS.

> [!NOTE]
> Aby móc się zalogować w tooapplications obsługujące federacji z usługą Azure AD (w tym Salesforce, usługi Google Apps, Dropbox, pole, Concur, produktu Workday, usługi Office 365 i więcej niż 70 innych użytkowników) w praktycznie dowolnej przeglądarki sieci web, na dowolnym urządzeniu, bez konieczności aplikacji dodatku plug-in lub przenośnych. Wszystkie inne [dostęp do środowiska panelu](https://myapps.microsoft.com/) również nie wymagają hello toobe aplikacji mobilnej Moje aplikacje używane na urządzeniu przenośnym.
>
>

### <a name="my-apps-for-android"></a>Moje aplikacje dla systemu Android

Moje aplikacje dla systemu Android jest obsługiwana na dowolnym urządzeniu z systemem Android, którym jest uruchomiona wersja systemu Android 4.1 lub nowszej.  
Jest on dostępny w hello [sklepu Google Play](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Moje aplikacje dla systemu Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Moje aplikacje dla urządzenia iPhone i iPad

Moje aplikacje dla systemu iOS jest obsługiwana na wszystkie urządzenia iPhone lub iPad z systemem iOS w wersji 7 lub nowszy.  
Jest on dostępny w hello [sklepu Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Moje aplikacje dla systemu iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Zarządzane przeglądarki pod kątem Moje aplikacje

Moje aplikacje również jest zintegrowana z hello Intune Managed Browser. Witaj Intune Managed Browser dla urządzeń iOS i Android odgrywa kluczową rolę w zapewnieniu, że dane na urządzeniach przenośnych jest bezpieczne. Umożliwia ona bezpiecznie przeglądać i przejdź do strony sieci web, które mogą zawierać informacje o firmie i zapewnia bezpieczne przeglądanie sieci web.  
Możesz znaleźć aplikacji toomy szybki dostęp na stronie głównej Managed Browser oraz w zakładki, umożliwiając mniej kliknie tooreach dowolną aplikację tooaccess.

Jest on dostępny w hello [sklepu Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) i [sklepu Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Przeglądarka Mananged Moje aplikacje][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Porady dotyczące testowania czynności użytkownika hello

Jeśli jesteś administratorem Azure i toohello Azure portal jest zalogowany przy użyciu konta w katalogu hello, użytkownik zostanie automatycznie zarejestrowany w panelu dostępu toohello jako swoim aktualnym kontem. W takim przypadku widoczne wszystkie aplikacje, które zostały przypisane tooyou.

**tootest jako *różnych* konta użytkownika:**

1. Kliknij menu użytkownika hello w hello prawym górnym rogu portalu Azure hello lub hello panelu dostępu, a następnie wybierz **Wyloguj**. 
2. Przejdź toohello [panelu dostępu](http://myapps.microsoft.com).
3. Na powitania strony logowania, nazwy typu hello użytkownika i hasło dla konta hello w katalogu ma tootest.


## <a name="starting-applications"></a>Uruchamianie aplikacji

Kilka typów aplikacji mogą być wyświetlane na powitania panelu dostępu.

### <a name="office-365-applications"></a>Aplikacje pakietu Office 365

Jeśli organizacja korzysta z aplikacji usługi Office 365, jest udzielana dla nich hello usługi Office 365 aplikacje pojawiają się na Twoje panelu dostępu.

Po kliknięciu kafelka aplikacji dla aplikacji usługi Office 365 zostaną przekierowane toohello aplikacji i automatycznie zalogowany.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego

Administrator może dodać aplikacje w hello sekcji usługi Active Directory hello portalu Azure w trybie logowania jednokrotnego hello ustawić także**Azure AD rejestracji jednokrotnej**. Te aplikacje może zobaczyć tylko, jeśli administrator ma jawnie przyznane uprawnienia dostępu toohello aplikacji.

Po kliknięciu kafelka dla jednej z tych aplikacji, są przekierowywane i zostanie automatycznie zalogowany toohello aplikacji.

### <a name="password-based-sso-without-identity-provisioning"></a>Na podstawie hasła logowania jednokrotnego bez obsługi tożsamości

Administrator może dodać aplikacje w hello sekcji usługi Active Directory hello portalu Azure w trybie logowania jednokrotnego hello ustawić także**opartego na hasłach rejestracji jednokrotnej**. Wszyscy użytkownicy w katalogu hello widzą wszystkie aplikacje, które zostały skonfigurowane w tym trybie.

Witaj po raz pierwszy, kliknięciu kafelka dla jednej z tych aplikacji, są hello tooinstall zostanie wyświetlony monit o hasło SSO dodatek dla programu Internet Explorer lub przeglądarki Chrome. Witaj instalacji może wymagać toorestart możesz przeglądarki sieci web. Gdy wróć toohello panelu dostępu i kliknij Kafelek aplikacji hello ponownie, zostanie wyświetlony monit o nazwę użytkownika i hasło dla aplikacji hello. Po wprowadzeniu nazwy użytkownika i hasła, te poświadczenia są bezpiecznie przechowywane i połączyć tooyour konta w usłudze Azure AD.

Witaj następnym kliknięciu kafelka aplikacji hello, użytkownik zostanie automatycznie zarejestrowany w toohello aplikacji.  
Nie masz tooenter poświadczenia ponownie i lub zainstalować hello logowania jednokrotnego hasła wtyczki.

Jeśli poświadczenia zostały zmienione w aplikacji innej firmy docelowej hello, musisz zaktualizować swoje poświadczenia, które są przechowywane w usłudze Azure AD. 

**poświadczenia tooupdate:**

1. Wybierz ikonę hello na kafelku aplikacji hello.
2. Wybierz **zaktualizować poświadczenia** tooreenter hello w nazwę użytkownika i hasło hello aplikacji.


### <a name="password-based-sso-with-identity-provisioning"></a>Oparte na hasłach rejestracji Jednokrotnej z inicjowaniem obsługi administracyjnej tożsamości

Administrator może dodać aplikacje w hello **usługi Active Directory** sekcji hello portalu Azure w trybie logowania jednokrotnego hello ustawić także**opartego na hasłach rejestracji jednokrotnej**, oraz inicjowanie obsługi tożsamości.

Witaj po raz pierwszy, kliknięciu kafelka aplikacji dla jednej z tych aplikacji, są hello zostanie wyświetlony monit o tooinstall **logowania jednokrotnego hasła dodatek dla programu Internet Explorer lub przeglądarki Chrome**. Witaj instalacji może wymagać toorestart możesz przeglądarki sieci web.  
Gdy wróć toohello panelu dostępu i ponownie, kliknij Kafelek aplikacji hello użytkownik zostanie automatycznie zarejestrowany w aplikacji toohello.

Niektóre aplikacje mogą wymagać hasła na powitania pierwszego logowania użytkownik toochange. Jeśli poświadczenia zostały zmienione w aplikacji innej firmy docelowej hello, należy również zaktualizować hello poświadczenia, które są przechowywane w usłudze Azure AD. 

**poświadczenia tooupdate:**

1. Wybierz ikonę hello na kafelku aplikacji hello.
2. Wybierz **zaktualizować poświadczenia** tooreenter hello w nazwę użytkownika i hasło hello aplikacji.


### <a name="application-with-existing-sso-solutions"></a>Aplikacja z istniejącymi rozwiązaniami do logowania jednokrotnego

tooconfigure logowania jednokrotnego dla aplikacji hello Azure portal udostępnia trzecia opcja o nazwie **istniejących rejestracji jednokrotnej**. Ta opcja umożliwia toocreate Twojego administratora aplikacji tooan łącza i umieść ją na powitania panel dostępu dla wybranych użytkowników.

Na przykład jeśli aplikacja jest skonfigurowany tooauthenticate użytkowników za pomocą usług AD FS 2.0, administrator może użyć hello **istniejących rejestracji jednokrotnej** toocreate opcji tooit łącza na powitania panelu dostępu. Po otwarciu łącze hello są uwierzytelniane za pomocą usług AD FS 2.0 lub udostępnia niezależnie od istniejącej aplikacji hello rozwiązania logowania jednokrotnego.


## <a name="next-steps"></a>Następne kroki

- toosee listę wszystkich tematów, które są powiązane tooapplication zarządzania, zobacz hello [indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md).
 
- toolearn toointegrate aplikacji SaaS, do usługi Azure AD, zobacz temat hello [lista samouczków dotyczących aplikacji SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn więcej informacji o zarządzanie aplikacjami za pomocą usługi Azure AD, zobacz hello [wprowadzenie toosingle logowania jednokrotnego i zarządzanie dostępem do aplikacji za pomocą usługi Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn więcej informacji na temat Inicjowanie obsługi użytkowników, zobacz [zautomatyzować użytkownika alokowania i anulowania alokowania aplikacji tooSaaS](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
