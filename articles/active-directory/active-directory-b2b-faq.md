---
title: "aaaAzure współpracy B2B usługi Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Pobierz zadawane pytania na temat współpracy usługi Azure Active Directory B2B toofrequently odpowiedzi."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure współpracy B2B usługi Active Directory — często zadawane pytania

Często zadawane pytania (FAQ) dotyczące współpracy między firmami (B2B) w usłudze Azure Active Directory (Azure AD) są okresowo aktualizowane tooinclude nowych tematów.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Współpraca B2B usługi Azure AD jest dostępna w hello klasycznego portalu Azure?
Nie. Funkcje współpracy B2B usługi AD platformy Azure są dostępne tylko w hello [portalu Azure](https://portal.azure.com) w hello [panelu dostępu](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Dlatego jest bardziej intuicyjne dla naszych gości współpracy B2B możemy dostosować stronę logowania?
Absolutnie! Zobacz nasze [wpis w blogu o tej funkcji](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Aby uzyskać więcej informacji na temat sposobu toocustomize organizacji logowania strony, zobacz [Dodaj firmowe toosign w i strony panelu dostępu](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Można B2B współpracy użytkownicy uzyskują dostęp do usługi SharePoint Online i OneDrive?
Tak. Jednak hello toosearch możliwości istniejących użytkowników Gość w usłudze SharePoint Online przy użyciu selektora osób hello jest **poza** domyślnie. Ustaw tooturn na powitania toosearch opcji dla istniejących gości, **ShowPeoplePickerSuggestionsForGuestUsers** za**na**. Można włączyć to ustawienie na poziomie dzierżawy hello lub na poziomie zbioru witryn hello. To ustawienie można zmienić za pomocą polecenia cmdlet Set-SPOTenant i SPOSite zestaw hello. Z tych poleceń cmdlet elementy członkowskie umożliwia wyszukiwanie istniejących Goście w katalogu hello. Zmiany w zakresie dzierżawy hello nie wpływają na witryn usługi SharePoint Online, które zostały już zainicjowane.

### <a name="is-hello-csv-upload-feature-still-supported"></a>To jest funkcja nadal obsługiwane przekazywania CSV hello?
Tak. Aby uzyskać więcej informacji o korzystaniu z funkcji przekazywania plików CSV hello, zobacz [w tym przykładzie programu PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Jak można dostosować wiadomości e-mail z zaproszeniem?
Prawie wszystkie informacje o procesie zapraszającej hello można dostosować za pomocą hello [zaproszenia B2B interfejsów API](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Zaproszonych użytkowników zewnętrznych można pozostawić organizacji powitania po trwa zaproszenie?
Hello zaproszenia organizacji administrator może usunąć użytkownika gościa współpracy B2B z ich katalogu, ale hello użytkownika gościa nie może opuścić hello zapraszanie katalogu organizacji samodzielnie. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Goście resetowania ich uwierzytelnianie wieloskładnikowe — metoda
Tak. Goście mogą resetować ich hello metody uwierzytelniania wieloskładnikowego, tak samo sposób przez regularne użytkowników czy.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Której organizacji jest odpowiedzialny za licencje usługi Multi-Factor authentication?
organizacja zaproszenia Hello przeprowadza uwierzytelnianie wieloskładnikowe. Hello zapraszanie organizacji należy się upewnić, że organizacja hello ma wystarczającą liczbę licencji dla ich B2B użytkowników, którzy korzystają z usługi Multi-Factor authentication.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Co zrobić, jeśli już organizacji partnerskiej ma skonfigurować uwierzytelnianie wieloskładnikowe? Można możemy zaufania ich uwierzytelnianie wieloskładnikowe i nie używać własnej uwierzytelnianie wieloskładnikowe?
Ta funkcja jest planowane w przyszłości, który możesz można wybrać określonych partnerów tooexclude z uwierzytelniania wieloskładnikowego (hello zaproszenia organizacji).

### <a name="how-can-i-use-delayed-invitations"></a>Jak używać opóźnione zaproszenia?
Organizacja może użytkownicy współpracy tooadd B2B, ich tooapplications w razie potrzeby udostępnić, a następnie Wyślij zaproszenia. Możesz użyć hello B2B współpracy zaproszenia interfejsu API toocustomize hello dołączania przepływu pracy.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Można utworzyć użytkownika gościa administratorem ograniczonym?
Naturalnie. Aby uzyskać więcej informacji, zobacz [Dodawanie gościa użytkowników tooa roli](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Współpraca B2B usługi Azure AD pozwala B2B użytkowników tooaccess hello portalu Azure?
Chyba że użytkownik jest przypisany roli hello ograniczone administratora lub administratora globalnego, użytkownicy współpracy B2B nie wymagają toohello dostęp do portalu Azure. Jednak użytkownicy współpracy B2B, którzy mają przypisaną rolę hello ograniczone administratora lub administratora globalnego może uzyskać dostęp do portalu hello. Ponadto jeśli użytkownika gościa, który nie jest przypisany jeden z tych ról Administrator uzyskuje dostęp do portalu hello, hello użytkownika może być możliwe tooaccess niektórych części hello środowisko. Rola użytkownika gościa Hello ma niektóre uprawnienia w katalogu hello.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Czy można zablokować toohello dostęp do portalu Azure dla gości
Tak! Podczas konfigurowania tych zasad, należy zachować ostrożność tooavoid przypadkowo blokowanie dostępu toomembers i Administratorzy.
tooblock użytkownika gościa dostęp toohello [portalu Azure](https://portal.azure.com), użyj zasad dostępu warunkowego w hello interfejs API modelu klasycznym wdrażania systemu Windows Azure:
1. Modyfikowanie hello **wszyscy użytkownicy** grupy tak, aby zawierał tylko elementy członkowskie.
  ![Modyfikowanie grupy hello w zrzut ekranu](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Utwórz grupy dynamicznej, która zawiera gości.
  ![Tworzenie grupy zrzut ekranu](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Konfigurowanie użytkowników gościa tooblock zasad dostępu warunkowego dostępu do portalu hello, jak pokazano poniżej hello wideo:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Współpraca B2B usługi Azure AD obsługuje uwierzytelnianie wieloskładnikowe i konta poczty e-mail użytkownika?
Tak. Wieloskładnikowego uwierzytelniania i konsumentów konta e-mail są obsługiwane dla współpracy B2B usługi Azure AD.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Czy firma planuje toosupport resetowania haseł dla użytkowników współpracy B2B usługi Azure AD?
Tak. Poniżej przedstawiono istotne szczegóły samoobsługowego resetowania hasła (SSPR) dla użytkownika B2B, który jest zaproszenie od organizacji będącej partnerem hello:
 
* SSPR występuje tylko w dzierżawie tożsamości hello hello B2B użytkownika.
* Jeśli konto Microsoft jest dostępna dzierżawa tożsamości hello, hello konta Microsoft mechanizm SSPR jest używany.
* Jeśli hello tożsamość dzierżawcy jest just-in-time (JIT) lub "wirusa" dzierżawy, jest wysyłane e-mail resetowania hasła.
* W przypadku pozostałych dzierżaw hello standardowy proces SSPR nastąpią B2B użytkowników. Takie jak member SSPR B2B użytkowników, w kontekście hello zasobu hello dzierżawy jest zablokowany. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>Jest resetowania hasła dostępne dla gości w just-in-time (JIT) lub "wirusa" dzierżawy, którzy zaakceptowali zaproszeń do skorzystania z pracą lub służbowego adresu e-mail, ale który nie ma istniejące konto usługi Azure AD?
Tak. Wiadomości resetowania hasła można wysyłać, która umożliwia tooreset użytkownika hasła w hello JIT dzierżawy.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM oferuje pomocy online do współpracy B2B usługi Azure AD?
Obecnie programu Microsoft Dynamics CRM nie zapewnia pomoc online współpracy B2B usługi Azure AD. Jednak planujemy toosupport to w przyszłości hello.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Co to jest okres istnienia hello hasła początkowego dla nowo utworzonego użytkownika współpracy B2B?
Usługa Azure AD ma ustalony zbiór znaków, siły hasła i wymagania dotyczące blokady konta, które są stosowane jednakowo kont użytkowników w chmurze Azure AD tooall. Konta użytkowników w chmurze są kontami, które nie są Sfederowane przy użyciu innego dostawcy tożsamości, na przykład 
* Konto Microsoft
* Facebook
* Usługi federacyjne Active Directory
* Innej chmurze dzierżawy (Współpraca B2B)

Dla kont federacyjnych zasad haseł zależy od zasad hello, które są stosowane w ustawieniach konta Microsoft hello lokalnymi dzierżawy i hello użytkownika.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Organizacja może być toohave różnych napotka w aplikacjach dla użytkowników dzierżawy i gości. Czy istnieje standardowa wskazówki dotyczące to? To jest obecność hello hello tożsamości dostawcy oświadczeń hello prawidłowy model toouse?
 Użytkownika gościa można użyć dowolnego tooauthenticate dostawcy tożsamości. Aby uzyskać więcej informacji, zobacz [właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md). Użyj hello **UserType** środowisko użytkownika toodetermine właściwości. Witaj **UserType** oświadczenia jest obecnie niedostępna w hello tokenu. Aplikacje powinny używać hello interfejsu API programu Graph tooquery hello katalogu dla użytkownika hello i tooget hello UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Gdzie mogę znaleźć tooshare społeczności współpracy B2B rozwiązań i pomysły toosubmit?
Firma Microsoft stale jest nasłuchiwanie tooyour opinie na temat tooimprove współpracy B2B. Zapraszamy tooshare możesz użytkownika scenariuszy, najlepsze rozwiązania i co Ci się podoba współpracy B2B usługi Azure AD. Dołącz do dyskusji hello w hello [społeczność techniczna Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Również Zapraszamy możesz toosubmit swoich koncepcji i głosów dla przyszłych funkcje na [pomysły współpracy B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Możemy wysłać zaproszenie, który jest automatycznie zrealizowane, tak że hello użytkownika jest po prostu "gotowe toogo"? Lub hello użytkownik zawsze ma tooclick za pomocą adresu URL realizacji toohello?
Nie wymagają realizacji przez użytkownika B2B hello zaproszenia, które są wysyłane przez użytkownika w hello zapraszanie organizacji, która jest również członkiem hello organizacji partnera.

Firma Microsoft zaleca, aby zaprosić jednego użytkownika z hello partnera organizacji toojoin hello zapraszanie organizacji. [Dodaj tej roli użytkownika toohello gościa zapraszającej w organizacji zasobów hello](active-directory-b2b-add-guest-to-role.md). Ten użytkownik zaprosić innych użytkowników w organizacji partnera hello przy użyciu logowania hello interfejsu użytkownika, skrypty programu PowerShell lub interfejsów API. Następnie użytkownicy współpracy B2B z tej organizacji nie są wymagane tooredeem zaproszenia.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Współpraca B2B działanie partnera hello zaproszenie korzysta ze tooadd federacyjnego uwierzytelniania lokalnego?
Jeśli dzierżawa usługi Azure AD, która ma być federacyjne partnera hello toohello lokalnej infrastruktury do uwierzytelniania, lokalna Usługa rejestracji jednokrotnej (SSO) automatycznie uzyskuje się. Jeśli hello partner nie jest dzierżawa usługi Azure AD, konto usługi Azure AD jest tworzone dla nowych użytkowników. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Po próbie B2B usługi Azure AD nie zaakceptował gmail.com i outlook.com adresy e-mail i że B2C był używany przez te typy kont?
Zostaną usunięte hello różnice między B2B i współpracę (B2C) biznesowych do firmy, zgodnie z którą tożsamości są obsługiwane. tożsamość Hello używane nie jest toochoose powód, między przy użyciu B2B lub B2C. Informacje o wybieraniu opcjach współpracy, zobacz [współpracy B2B porównania i B2C w usłudze Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Jakie aplikacje i usługi obsługują gości B2B usługi Azure?
Wszystkie aplikacje Azure zintegrowanej z usługą AD obsługuje gości B2B usługi Azure. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Naszych partnerów, braku uwierzytelniania wieloskładnikowego możemy wymusić uwierzytelnianie wieloskładnikowe dla gości B2B?
Tak. Aby uzyskać więcej informacji, zobacz [dostępu warunkowego dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>W programie SharePoint można zdefiniować listę "Zezwalaj" lub "odmowa" dla użytkowników zewnętrznych. Firma Microsoft to zrobić na platformie Azure?
Tak. Azure obsługuje współpracy AD B2B listy zezwalania i odmowy dla. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Co zrobić, licencje potrzebujemy toouse B2B usługi Azure AD?
Aby uzyskać informacje o co licencje organizacji musi toouse B2B usługi Azure AD, zobacz [współpracy usługi Azure Active Directory B2B licencjonowania wskazówki](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure AD dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Rozwiązywanie problemów z współpracy B2B usługi Azure AD](active-directory-b2b-troubleshooting.md)
* [Dostosowywanie i Azure współpracy AD B2B interfejsu API](active-directory-b2b-api.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure AD](active-directory-apps-index.md)
