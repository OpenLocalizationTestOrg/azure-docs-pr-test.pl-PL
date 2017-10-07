---
title: "Często zadawane pytania (FAQ) — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Usługa Azure AD B2C: Często zadawane pytania (FAQ) 
Ta strona zawiera odpowiedzi na często zadawane pytania dotyczące hello Azure Active Directory (Azure AD) B2C. Sprawdzanie wstecz do aktualizacji.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>Funkcji usługi Azure AD B2C można korzystać w mojej istniejącej, na podstawie pracownika dzierżawy usługi Azure AD?
Usługi Azure AD i Azure AD B2C ofert osobnego produktu i nie mogą współistnieć w hello sam dzierżawy.  Dzierżawa usługi Azure AD reprezentuje organizacji.  Dzierżawy usługi Azure AD B2C reprezentuje kolekcję toobe tożsamości używane z aplikacjami danej firmy.  Przy użyciu zasad niestandardowych (w publicznej wersji zapoznawczej) usługi Azure AD B2C można było wykonać Federację tooAzure AD możliwość uwierzytelniania pracowników w organizacji.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Można używać usługi Azure AD B2C tooprovide społecznościowych nazwy logowania (Facebook i Google +) do usługi Office 365?
Usługa Azure AD B2C nie może być używane tooauthenticate użytkowników dla usługi Microsoft Office 365.  Usługi Azure AD jest rozwiązanie firmy Microsoft do zarządzania aplikacjami tooSaaS dostępu pracowników i zawiera funkcji służących do tego celu, takich jak licencjonowania i warunkowego dostępu.  Usługa Azure AD B2C zapewnia platformy do zarządzania tożsamościami i dostępem do tworzenia sieci web i aplikacji dla urządzeń przenośnych.  Gdy usługi Azure AD B2C jest dzierżawa usługi Azure AD tooan toofederate skonfigurowany, dzierżawy usługi Azure AD hello zarządza tooapplications dostępu pracowników, które korzystają z usługi Azure AD B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Co to są lokalne konta w usłudze Azure AD B2C? Jak różnią się one od kont służbowych w usłudze Azure AD?
W dzierżawie usługi Azure AD, użytkownicy, którzy należą dzierżawy toohello logowania przy użyciu adresu e-mail hello formularza `<xyz>@<tenant domain>`.  Witaj `<tenant domain>` jest weryfikowany jedną hello domen w hello dzierżawy lub hello początkowej `<...>.onmicrosoft.com` domeny. Ten typ konta jest konta firmowego lub szkolnego.

W dzierżawie usługi Azure AD B2C większości aplikacji ma użytkownika hello toosign w z dowolnego adresu e-mail dowolnego (na przykład joe@comcast.net, bob@gmail.com, sarah@contoso.com, lub jim@live.com). Ten typ konta jest kontem lokalnym.  Obsługujemy również nazwy dowolnego użytkownika jako kont lokalnych (na przykład Jan, Roberta, Anetą lub jim). Skonfigurowanie usługi Azure AD B2C w portalu Azure hello, można wybrać jedną z tych dwóch typów kont lokalnych.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Które dostawców tożsamości społecznościowych możesz obsługują teraz? Czy te, które planowanie toosupport w przyszłości hello?
Firma Microsoft obsługuje obecnie Facebook, Google + LinkedIn, Amazon, usługi Twitter (wersja zapoznawcza), WeChat (wersja zapoznawcza), Weibo (wersja zapoznawcza) i q (wersja zapoznawcza). Dodamy obsługę innych dostawców tożsamości społecznościowych popularnych na życzenie klientów.

Usługa Azure AD B2C dodano również obsługę [niestandardowych zasad](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Te [zasady niestandardowe](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) Zezwalaj developer toocreate własne zasady, że z każdego dostawcy tożsamości obsługującej [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) lub SAML. 

Wprowadzenie do zasad niestandardowych przez wyewidencjonowanie naszych [pakiet początkowy zasady niestandardowe](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Można skonfigurować zakresy toogather więcej informacji na temat klientów z różnych dostawców tożsamości społecznościowymi?
Nie, ale ta funkcja jest naszego planu. są używane dla naszego zestawu obsługiwanych dostawców tożsamości społecznościowych zakresów domyślnych Hello:

* Facebook: wiadomości e-mail
* Google +: wiadomości e-mail
* Konto Microsoft: profil poczty e-mail protokołu openid
* Amazon: profil
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Moja aplikacja ma toobe uruchamiania na platformie Azure dla niego pracy z usługą Azure AD B2C?
Nie można hostować aplikację w dowolnym miejscu (hello chmurze lub lokalnie). Wszystkie niezbędne toointeract z usługi Azure AD B2C jest hello toosend możliwości i odbierania żądań HTTP na publicznie punktów końcowych.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Mam wiele dzierżaw usługi Azure AD B2C. Jak zarządzać nimi na powitania portalu Azure?
Przed otwarciem usługi Azure AD B2C w menu po lewej stronie powitania hello portalu Azure, musisz przełączyć się do katalogu hello ma toomanage.  Przełącz katalogi, klikając swoją tożsamość w hello górnym rogu hello portalu Azure, a następnie wybierz katalog hello rozwijanej który pojawia się.  Aby uzyskać szczegółowe instrukcje wraz z obrazów, zobacz [Przejdź ustawienia tooAzure AD B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Jak dostosować weryfikacyjnych wiadomości e-mail (hello zawartości i hello "od:" pole) wysyłane przez usługę Azure AD B2C?
Można użyć hello [firmowe funkcji](../active-directory/active-directory-add-company-branding.md) toocustomize zawartość hello weryfikacyjnych wiadomości e-mail. W szczególności można dostosować tych dwóch elementów hello poczty e-mail:

* **Banner Logo**: pokazywane na powitania prawym dolnym rogu.
* **Kolor tła**: wyświetlany u góry hello.

    ![Zrzut ekranu przedstawiający wiadomość e-mail z dostosowanych weryfikacji](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

Podpis e-mail Hello zawiera nazwę dzierżawy B2C hello, podane podczas tworzenia dzierżawy hello B2C. Można zmienić nazwę hello, korzystając z tych instrukcji:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) jako hello administratorem subskrypcji.
1. Przejdź tooyour B2C dzierżawy.
1. Kliknij przycisk hello **Konfiguruj** kartę.
1. Zmień hello **nazwa** pole w obszarze hello **właściwości Directory** sekcji.
1. Kliknij przycisk **zapisać** u dołu hello hello strony.

Obecnie nie istnieje żadne hello toochange sposób "od:" na powitania poczty e-mail. Głosowania [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) planuje się Dostosowywanie treści hello hello weryfikacji w wiadomości e-mail.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Jak można przeprowadzić migrację mojej istniejącej nazwy użytkownika, hasła i profile z mojej tooAzure bazy danych AD B2C?
Hello Azure AD Graph API toowrite można użyć narzędzia do migracji. Zobacz hello [przykładowy interfejs API programu Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) szczegółowe informacje.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Jakie zasady haseł jest używana dla kont lokalnych w usłudze Azure AD B2C?
Hello Azure AD B2C zasady haseł dla kont lokalnych jest oparta na powitania zasad dla usługi Azure AD. Azure AD B2C jego rejestrację, zapisywania lub logowania i hasło zresetować siły hasła "silnego" hello używa zasad, a nie wygasa hasła. Witaj odczytu [zasady haseł usługi Azure AD](https://msdn.microsoft.com/library/azure/jj943764.aspx) więcej szczegółów.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>Czy można używać tożsamości konsumentów toomigrate Azure AD Connect, które są przechowywane na moje lokalnej usługi Active Directory tooAzure AD B2C?
Nie, usługi Azure AD Connect nie jest zaprojektowana toowork z usługi Azure AD B2C. Należy rozważyć użycie hello [interfejsu API programu Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) przypadku migracji użytkownika.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Moja aplikacja może otwarcie strony usługi Azure AD B2C w obrębie elementu iFrame?
Nie, ze względów bezpieczeństwa nie można otworzyć usługi Azure AD B2C stron w ramce.  Nasza usługa komunikuje się z hello przeglądarki tooprohibit IFRAME.  Ogólnie rzecz biorąc Hello społeczności zabezpieczeń i hello specyfikację OAUTH2, zaleca się przy użyciu ramek iframe dla środowiska tożsamości powodu ryzyka toohello miejsca kliknij.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Usługi Azure AD B2C działa z systemów CRM, takich jak Microsoft Dynamics?
Integracja z usługą Microsoft Dynamics 365 portalu jest dostępny.  Zobacz [toouse Konfigurowanie Dynamics 365 portalu usługi Azure AD B2C do uwierzytelniania](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Usługi Azure AD B2C jest korzystanie z programu SharePoint 2016 lokalnymi lub starszym?
Usługa Azure AD B2C nie jest przeznaczona dla hello SharePoint zewnętrznych udostępnianie partnera scenariusz; zobacz [B2B usługi Azure AD](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) zamiast tego.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Należy używać usługi Azure AD B2C lub tożsamości zewnętrznych toomanage B2B?
Przeczytaj ten artykuł o [tożsamości zewnętrznych](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn więcej informacji na temat stosowania hello odpowiednie funkcje tooyour tożsamości zewnętrznych scenariuszy.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Jakie raportowania i inspekcji funkcje usługi Azure AD B2C oferuje? Czy na pewno one hello takie same jak Azure AD Premium?
Nie, usługi Azure AD B2C obsługuje hello sam zestaw raportów, jako Azure AD Premium. Istnieje jednak wiele commonalities:

* Witaj logowania raporty zapewniają rejestr każdego logowania z obniżonych szczegółów.
* Raporty dotyczące inspekcji są dostępne w portalu Azure w usłudze Azure Active Directory hello > dzienników inspekcji działania > Wybierz B2C oraz Zastosuj filtry zgodnie z potrzebami. Obejmuje zarówno aktywność administratora, jak i działanie aplikacji. 
* Raport użycia, obejmujących liczby użytkowników, liczba logowań i wolumin MFA jest dostępna na [użycia interfejsu API raportowania](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Czy można lokalizować hello interfejsu użytkownika obsługiwanych przez usługę Azure AD B2C stron? Jakich języków są obsługiwane?
Tak!  Przeczytaj informacje o [dostosowywania języka](active-directory-b2c-reference-language-customization.md), która znajduje się w publicznej wersji zapoznawczej.  Firma Microsoft udostępnia tłumaczenia dla 36 języków, które można zmienić toosuit dowolnego ciągu potrzeb.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Czy można użyć własnych adresów URL na stronach rejestracji i logowania, które są obsługiwane przez usługę Azure AD B2C? Na przykład należy zmienić adres URL hello z login.microsoftonline.com toologin.contoso.com
Nie można obecnie. Ta funkcja jest naszego planu. Weryfikowanie domeny w hello **domen** kartę na powitania klasycznego portalu Azure nie realizację tego celu.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Jak usunąć mojej dzierżawy usługi Azure AD B2C?
Wykonaj te kroki toodelete dzierżawy usługi Azure AD B2C:

1. Wykonaj następujące kroki zbyt[Przejdź ustawienia tooAzure AD B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
1. Przejdź toohello **aplikacji**, **dostawców tożsamości**, i **wszystkich zasad** i usunąć wszystkie wpisy hello w każdej z nich.
1. Teraz logować się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) jako hello administratorem subskrypcji. (Użyj hello tej samej pracy lub konta służbowego lub hello tego samego konta Microsoft użytą toosign dla platformy Azure).
1. Przejdź toohello rozszerzenie usługi Active Directory po lewej stronie powitania i kliknij dzierżawę B2C.
1. Kliknij przycisk hello **użytkowników** kartę.
1. Wybierz każdego użytkownika z kolei (Wyklucz hello administratorem subskrypcji użytkownika, którego obecnie zalogowano jako). Kliknij przycisk **usunąć** u dołu strony hello i kliknij przycisk hello **tak** po wyświetleniu monitu.
1. Kliknij przycisk hello **aplikacji** kartę.
1. Wybierz **aplikacji Moja firma jest właścicielem** w hello **Pokaż** pole listy rozwijanej i kliknij znacznik wyboru hello.
1. Aplikacja o nazwie **b2c rozszerzeń aplikacji**. Kliknij przycisk **usunąć** u dołu strony hello i kliknij przycisk hello **tak** po wyświetleniu monitu.
1. Ponownie Przejdź toohello rozszerzenie usługi Active Directory i wybierz dzierżawę B2C.
1. Kliknij przycisk **usunąć** u dołu hello hello strony. proces hello toocomplete, wykonaj instrukcje hello na ekranie powitania.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Czy można uzyskać usługi Azure AD B2C jako część pakietu Enterprise Mobility Suite?
Nie, usługi Azure AD B2C jest płatność za rzeczywiste użycie usługi Azure, nie jest częścią pakietu Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Jak zgłosić problemy z usługą Azure AD B2C?
Zobacz [pliku żądania pomocy technicznej usługi Azure Active Directory B2C](active-directory-b2c-support.md).
