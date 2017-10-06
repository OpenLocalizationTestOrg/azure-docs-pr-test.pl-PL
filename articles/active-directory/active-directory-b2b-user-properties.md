---
title: "aaaProperties użytkownik współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Właściwości użytkownika współpraca w usłudze Azure Active Directory B2B są konfigurowane"
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
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Właściwości użytkownika współpracy usługi Azure Active Directory B2B

Azure Active Directory (Azure AD) biznesowych między firmami (B2B) współpracy użytkownik jest użytkownikiem z UserType = gościa. Zazwyczaj tego użytkownika gościa jest od organizacji będącej partnerem i ma ograniczone uprawnienia w hello zapraszanie katalogu, domyślnie.

W zależności od hello zapraszanie potrzeb organizacji użytkownik współpracy B2B usługi Azure AD można w jednym z hello następujące stany konta:

- Stan 1: Adresem IP w zewnętrznych wystąpienia usługi Azure AD i reprezentowana jako użytkownik-Gość w hello zapraszanie organizacji. W takim przypadku hello B2B użytkownik loguje się przy użyciu konta usługi Azure AD, które należy toohello zaproszenie dzierżawy. Jeśli organizacja partnerska hello nie używa usługi Azure AD, tworzona jest nadal hello użytkownik-Gość w usłudze Azure AD. wymagania Hello są one zrealizować ich zaproszenia, a usługi Azure AD, sprawdza swój adres e-mail. To rozmieszczenie jest również nazywany just in time (JIT) dzierżawy lub "wirusa" dzierżawy.

- Stan 2: Adresem IP w ramach konta Microsoft i reprezentowana jako użytkownik-Gość w hello hosta organizacji. W takim przypadku użytkownik-Gość hello zaloguje się za pomocą konta Microsoft. Hello zaproszenie społecznościowych tożsamości użytkownika (google.com lub podobny), który nie jest kontem Microsoft, zostanie utworzona jako konto Microsoft podczas realizacji oferty.

- Stan 3: Adresem IP w usłudze Active Directory lokalne powitania hosta organizacji i zsynchronizowane z organizacji hosta hello Azure AD. W tej wersji należy użyć programu PowerShell toomanually zmiany hello UserType takich użytkowników w chmurze hello.

- Stan 4: Adresem IP w organizacji hosta usługi Azure AD z UserType = gościa i poświadczenia, które organizacja hosta hello zarządza.

  ![Wyświetlanie inicjały zapraszającej hello](media/active-directory-b2b-user-properties/redemption-diagram.png)


Teraz zobaczmy, jak wygląda użytkownika współpracy B2B usługi Azure AD w stanie 1 w usłudze Azure AD.

### <a name="before-invitation-redemption"></a>Przed realizacji zaproszenia

![Przed realizacji oferty](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Po realizacji zaproszenia

![Po realizacji oferty](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Właściwości klucza użytkownika współpracy B2B usługi Azure AD hello
### <a name="usertype"></a>UserType
Ta właściwość wskazuje relacji hello hello użytkownika toohello hosta dzierżawy. Ta właściwość może mieć dwie wartości:
- Element członkowski: Ta wartość wskazuje pracownika hello hosta organizacji i użytkowników w organizacji hello płacowego. Na przykład ten użytkownik oczekuje toohave dostęp tylko do toointernal witryny. Ten użytkownik mogą nie być uważane za zewnętrzne współpracownika.

- Gość: Ta wartość wskazuje użytkownika, który nie jest uznawane za firma toohello wewnętrznego, na przykład współpracownika zewnętrznych, partnera, klienta lub podobne użytkownika. Takiego użytkownika nie jest oczekiwanym tooreceive memo wewnętrzny Dyrektora Generalnego lub uzyskać korzyści firmy, na przykład.

  > [!NOTE]
  > Hello UserType ma nie relacji toohow hello użytkownik loguje, hello katalogu roli użytkownika hello i tak dalej. Tej właściwości po prostu wskazuje użytkownika hello relacji toohello hosta organizacji i umożliwia organizacji hello tooenforce zasad, które są zależne od tej właściwości.

### <a name="source"></a>Element źródłowy
Ta właściwość wskazuje, jak hello użytkownik się zaloguje.

- Zaproszonych użytkowników: Tego użytkownika zaproszono, ale nie ma jeszcze zrealizowane zaproszenia.

- Zewnętrzne usługi Active Directory: Tego użytkownika jest adresem IP w organizacji zewnętrznych i przeprowadza uwierzytelnianie za pomocą konta usługi Azure AD, które należy toohello innej organizacji. Ten typ logowania odpowiada tooState 1.

- Konto Microsoft: tego użytkownika jest adresem IP w ramach konta Microsoft i przeprowadza uwierzytelnianie za pomocą konta Microsoft. Ten typ logowania odpowiada tooState 2.

- Windows Server Active Directory: Ten użytkownik jest zalogowany z lokalnej usłudze Active Directory należy toothis organizacji. Ten typ logowania odpowiada tooState 3.

- Azure Active Directory: Ten użytkownik jest uwierzytelniany przy użyciu konta usługi Azure AD, które należy toothis organizacji. Ten typ logowania odpowiada tooState 4.
  > [!NOTE]
  > Źródło i UserType są niezależne właściwości. Wartość źródła dla UserType nie oznacza określonej wartości.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Użytkownicy B2B usługi Azure AD można dodać jako członków zamiast gości?
Zazwyczaj użytkownik B2B usługi Azure AD i użytkownika gościa oznaczają to samo. W związku z tym użytkownikiem współpracy B2B usługi Azure AD nie zostanie dodany jako użytkownik z UserType = domyślnie gościa. Jednak w niektórych przypadkach organizacji partnerskiej hello jest należy także członkiem większej organizacji hosta hello toowhich organizacji. Jeśli tak, tootreat użytkowników w organizacji partnerskiej hello jako elementy członkowskie zamiast Goście mają hello hosta organizacji. Użyj tooadd interfejsów API usługi Azure AD B2B zaproszenia Menedżera hello lub zaprosić użytkownika z organizacji organizacji partnerskiej hello hosta toohello jako element członkowski.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filtr dla gości w katalogu hello

![Filtr gości](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Konwertuj UserType
Obecnie istnieje możliwość użytkowników tooconvert UserType z elementu członkowskiego tooGuest i na odwrót przy użyciu programu PowerShell. Jednak hello Właściwość UserType powinien toorepresent hello relacji toohello organizacja użytkownika. W związku z tym hello wartość tej właściwości należy zmieniać tylko wtedy, gdy relacja hello hello użytkownika toohello organizacji ulegnie zmianie. Jeśli relacja hello użytkownika hello ulegnie zmianie, problemów, takich jak określa, czy należy zmienić hello nazwa główna użytkownika (UPN), była skierowana? Użytkownika hello kontynuowania toohave toohello dostęp do tych samych zasobów? Należy przypisać skrzynki pocztowej? W związku z tym nie zaleca się zmiany hello UserType przy użyciu programu PowerShell jako atomic działania. Ponadto w przypadku, gdy ta właściwość staje się modyfikować za pomocą programu PowerShell, nie zaleca się przyjmowanie zależności od tej wartości.

## <a name="remove-guest-user-limitations"></a>Usuń ograniczenia użytkownika gościa
Może to być przypadków miejscu toogive gościa uprawnienia wyższej użytkowników. Możesz dodać roli tooany użytkownika gościa i nawet usuwać ograniczenia użytkownika gościa domyślne hello w toogive katalogu hello hello użytkownika, takie same uprawnienia jako elementy członkowskie.

Jest możliwe tooturn poza ograniczenia użytkownika gościa domyślne hello tak, aby użytkownik-Gość w katalogu firmy hello podano hello takie same uprawnienia jak użytkownika elementu członkowskiego.

![Usuń ograniczenia użytkownika gościa](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Użytkownik współpracy B2B inspekcji i raportowanie](active-directory-b2b-auditing-and-reporting.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
