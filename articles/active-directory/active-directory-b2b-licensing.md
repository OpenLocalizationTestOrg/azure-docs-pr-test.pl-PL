---
title: "wskazówki dotyczące licencjonowania współpracy aaaAzure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Azure Active Directory B2B nie wymagają współpracy płatnej licencji usługi Azure AD, ale można również pobrać płatności funkcje dla gości B2B"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Wskazówki dotyczące licencjonowania funkcji współpracy między firmami przy użyciu usługi Azure Active Directory

Służy użytkownikom tooinvite możliwości współpracy B2B usługi Azure AD do Twojej tooallow dzierżawy usługi Azure AD ich tooaccess usługi Azure AD i innych zasobów w organizacji. Jeśli chcesz, aby funkcje usługi Azure AD toopaid dostępu tooprovide, B2B współpracy gościa użytkownicy muszą mieć licencję z odpowiednie licencje usługi Azure AD. 

W szczególności:
* Azure AD możliwości wolnego są dostępne dla gości bez dodatkowych licencji.
* Jeśli chcesz tooprovide dostępu toopaid usługi Azure AD funkcji tooB2B użytkowników, musi mieć za mało toosupport licencji tych gości B2B.
* Zapraszanie dzierżawcy z usługą Azure AD, płatną licencję dzierżawą B2B współpracy Użyj prawa tooan dodatkowe pięć B2B gościa zaproszonych użytkowników toohello.
* powitania klienta, który jest właścicielem hello zapraszanie dzierżawy musi być hello jeden toodetermine muszą ilu użytkowników współpracy B2B płatnej możliwości usługi Azure AD. W zależności od hello płatnej usługi Azure AD funkcje dla użytkownika gościa musi mieć wystarczająco usługi Azure AD płatnej licencji użytkowników współpracy toocover B2B w hello zachowaniem 5:1.

Współpraca B2B gościa jest dodawana jako użytkownik z partnerskiej firmy, a nie pracownika z organizacji lub pracownik służbowych w Twojej konglomeratu. Użytkownika gościa B2B można zalogować się przy użyciu poświadczeń zewnętrznych poświadczeń należących do organizacji zgodnie z opisem w tym artykule. 

Innymi słowy B2B licencjonowania ustawiono nie jak hello użytkownik jest uwierzytelniany, ale raczej relacji hello hello użytkownika tooyour organizacji. Jeśli Ci użytkownicy nie są partnerów, są one traktowane inaczej w umowy licencyjnej. Nie są wliczane toobe użytkownika współpracy B2B do celów licencjonowania, nawet jeśli ich UserType jest oznaczona jako "Gość". Powinny być one licencjonowane zwykle na jedną licencję dla poszczególnych użytkowników. Tych użytkowników należą:
* Pracownikom
* Personel logowanie przy użyciu tożsamości zewnętrznych
* Pracownik służbowych w Twojej konglomeratu


## <a name="licensing-examples"></a>Przykłady licencjonowania
- Odbiorca chce otrzymywać tooinvite 100 B2B współpracy użytkowników tooits dzierżawy usługi Azure AD. przypisuje powitania klienta zarządzania dostępem i Inicjowanie obsługi administracyjnej dla wszystkich użytkowników, ale 50 użytkowników wymagają usługi MFA i dostępu warunkowego. Ten klient musi zakupić 10 licencji Azure AD podstawowa i 10 toocover licencji Azure AD Premium P1 tych użytkowników B2B poprawnie. Jeśli powitania klienta plany toouse Identity Protection funkcje B2B użytkownikom, muszą one mieć usługi Azure AD Premium P2 licencji toocover hello zaproszonych użytkowników w hello zachowaniem 5:1.
- Klient ma 10 pracowników, którzy mają wszystkie aktualnie licencję z usługi Azure AD Premium P1. Teraz chcą tooinvite 60 B2B użytkownicy którzy wymusić uwierzytelnianie wieloskładnikowe (MFA). W obszarze hello 5:1 licencjonowania reguły powitania klienta musi mieć co najmniej 12 toocover licencji Azure AD Premium P1 wszystkim użytkownikom 60 współpracy B2B. Ponieważ są one już 10 Premium P1 licencji dla swoich pracowników, 10, mają prawa tooinvite 50 B2B użytkowników z funkcji Premium P1, takich jak uwierzytelnianie wieloskładnikowe. W tym przykładzie następnie one musi zakupić 2 dodatkowe licencje Premium P1 toocover hello pozostałe 10 B2B współpracy użytkowników.

> [!NOTE]
> Jeszcze tooassign licencje bezpośrednio tooenable użytkowników toohello B2B te prawa użytkownika współpracy B2B nie istnieje sposób.

powitania klienta, który jest właścicielem hello zapraszanie dzierżawy musi być hello jeden toodetermine muszą ilu użytkowników współpracy B2B płatnej możliwości usługi Azure AD. W zależności od tego, który płatnej funkcje usługi Azure AD, które chcesz dla użytkownika gościa musi mieć wystarczająco Azure AD płatnej użytkowników współpracy B2B toocover licencji hello współczynnika 5:1. 

## <a name="additional-licensing-details"></a>Dodatkowe szczegóły licencjonowania
- Konta użytkowników tooB2B tooactually przypisanie licencji nie jest konieczne. W oparciu o wskaźnik 5:1 hello, licencjonowania jest obliczana i automatycznie zgłaszane.
- Jeśli nr płatnej licencji usługi Azure AD istnieje w dzierżawie powitalnych, co prawa hello pobiera zaproszonych użytkowników, które hello Azure AD wolne oferty edition.
- Jeśli licencji B2B współpracy użytkownik ma już płatne Azure AD w organizacji, nie zużywają jedną licencji współpracy hello B2B hello zaproszenia dzierżawcy.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Zaawansowane dyskusji: jakie są hello zagadnień związanych z licencjami, gdy możemy dodać użytkowników z konglomeratu organizacji jako "Członkowie" przy użyciu swoje interfejsy API?
Użytkownik-Gość B2B to taki, który jest zaproszenie z toowork organizacji partnera, z organizacją hosta hello. Zazwyczaj innym przypadku nie kwalifikuje się B2B nawet go używa funkcji B2B. Oto dwa przypadki w szczególności:

1. Jeśli host zaprasza pracownika przy użyciu adresu konsumenta
  * W tym scenariuszu nie jest zgodne z naszych zasadami licencjonowania i nie jest zalecane.

2. Jeśli organizacja hosta dodaje użytkownika z innej organizacji konglomeratu
  1. W takim przypadku użytkownik hello jest zaproszony przy użyciu interfejsów API B2B, ale ten przypadek nie jest tradycyjnie B2B. W idealnym przypadku powinien mieć organizacje te zaproszenia hello innym użytkownikom organizacjami jako elementy członkowskie (interfejsach API umożliwia które). W takim przypadku licencji ma toobe przypisane toothese członków dla nich zasoby tooaccess w hello zapraszanie organizacji.

  2. W niektórych organizacjach może być tooadd hello toobe użytkowników innych organizacji dodany jako "Gość" jako zasady. Istnieją dwa przypadki, w tym miejscu:
      * Witaj konglomeratu organizacja już korzysta z usługi Azure AD i hello zaproszonych użytkowników są licencjonowane w hello innej organizacji: w tym przypadku nie powinien hello toofollow tooneed zaproszonych użytkowników formuła 1:5, którego układ określa się wcześniej w tym dokumencie. 

      * Witaj konglomeratu organizacja nie korzysta z usługi Azure AD lub nie mieć odpowiedniej licencji: W tym przypadku należy wykonać hello formuła 1:5, którego układ określa się wcześniej w tym dokumencie.

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API](active-directory-b2b-api.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
