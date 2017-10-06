---
title: "aaaTroubleshooting współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Środki zaradcze dla typowych problemów z współpracy usługi Azure Active Directory B2B"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B

Poniżej przedstawiono niektóre środki zaradcze dla typowych problemów z współpracy B2B usługi Azure Active Directory (Azure AD).


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Chcę dodano użytkownika zewnętrznego, ale nie ma ich w książce adresowej globalne lub selektora osób hello

W przypadkach, gdy użytkownicy zewnętrzni nie zostały wypełnione na liście hello obiektu hello może potrwać kilka minut tooreplicate.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Użytkownik-Gość B2B nie pojawia się w selektorze użytkowników usługi SharePoint Online/OneDrive 
 
Witaj toosearch możliwości istniejących użytkowników gościa w selektora osób hello SharePoint Online (SPO) został WYŁĄCZONY przez domyślne zachowanie starszych toomatch.

Aby włączyć tę funkcję, należy za pomocą hello ustawienie "ShowPeoplePickerSuggestionsForGuestUsers" na poziomie hello dzierżawy i zbioru witryn. Można ustawić opcję hello przy użyciu hello SPOTenant zestawu i SPOSite zestaw poleceń cmdlet, która zezwala na elementy członkowskie toosearch wszyscy istniejący użytkownicy gościa w katalogu hello. Zmiany w zakresie dzierżawy hello nie wpływają na lokacje SPO już zainicjowaną.

## <a name="invitations-have-been-disabled-for-directory"></a>Wyłączono zaproszeń do skorzystania z katalogu

Jeśli zostanie wyświetlone powiadomienie, że nie masz uprawnienia tooinvite użytkowników, sprawdź, czy konto użytkownika jest tooinvite autoryzowanych użytkowników zewnętrznych, w obszarze Ustawienia użytkownika:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Jeśli niedawno zmieniono te ustawienia lub przypisany hello zapraszającej gościa roli tooa użytkownik, mogą wystąpić opóźnienia 15 – 60 minut przed wprowadzeniem zmian hello.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>Użytkownik Hello I zaproszenie otrzymuje wystąpił błąd podczas realizacji

Typowe błędy:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Zaproszonej administrator nie zezwolił użytkowników EmailVerified utworzenie w swojej dzierżawy

Jeśli zaproszenie użytkowników, których organizacja korzysta z usługi Azure Active Directory, ale których hello konta określonego użytkownika nie istnieje (na przykład hello użytkownik nie istnieje w usłudze Azure AD w domenie contoso.com). administrator Hello contoso.com może mieć zasady w miejscu uniemożliwia tworzone przez użytkowników. Hello użytkownika musi skontaktuj się z ich toodetermine administratora, jeśli użytkownicy zewnętrzni są dozwolone. Witaj użytkownika zewnętrznego administratora może być konieczne tooallow zweryfikować poczty E-mail użytkowników w swojej domenie (zobacz [artykułu](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) na zezwolenie użytkownikom zweryfikować poczty E-mail).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Użytkownik zewnętrzny nie istnieje już w domenie federacyjnych

Jeśli używasz uwierzytelniania federacyjnego i użytkownik hello nie istnieje już w usłudze Azure Active Directory, nie mogą być zapraszani hello użytkownika.

Ten problem, hello tooresolve użytkownika zewnętrznego administratora musi zsynchronizować tooAzure konta hello użytkownika usługi Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Jak jest\#", która nie jest zwykle prawidłowym znakiem synchronizacji z usługą Azure AD?

"\#" jest zarezerwowany znak w UPN współpracy B2B usługi Azure AD lub użytkowników zewnętrznych, ponieważ hello zaproszenie konta user@contoso.com staje się user_contoso.com#EXT@fabrikam.onmicrosoft.com. W związku z tym \# w pochodzące z lokalnymi nazwy UPN nie są dozwolone toosign w toohello portalu Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Dodawanie użytkowników zewnętrznych tooa synchronizowane grupy, wystąpi błąd

Użytkownicy zewnętrzni można dodać tylko za "przypisane" lub "Zabezpieczenia" grup i nie toogroups, który jest zarządzany lokalnie.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Moje użytkownika zewnętrznego nie otrzymały tooredeem poczty e-mail

osoby zaproszonej Hello skontaktować się z Usługodawcą lub tooensure filtru spamu, który hello następującego adresu są niedozwolone:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>I należy zauważyć, że wiadomości powitania niestandardowych nie można uzyskać dołączana do komunikatów zaproszenia w czasie

toocomply z przepisów dotyczących prywatności, naszych interfejsów API, nie dołączaj niestandardowych komunikatów w wiadomości e-mail z zaproszeniem powitania po:

- zapraszającej Hello nie ma adresu e-mail w hello zapraszanie dzierżawy
- Gdy podmiot zabezpieczeń appservice wysyła hello zaproszenie

Ten scenariusz jest ważne tooyou, można pominąć naszych wiadomość e-mail z zaproszeniem interfejsu API i wysłać go za pomocą mechanizmu e-mail hello wybranych przez użytkownika. Zapoznaj się w organizacji korzystania z pomocy prawnej toomake się, że wszystkie wiadomości e-mail wysyłanych w ten sposób również spełnia przepisów dotyczących prywatności.

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API](active-directory-b2b-api.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
