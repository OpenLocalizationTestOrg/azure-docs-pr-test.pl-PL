---
title: "aaaCustomizing oświadczeń wydanych w hello tokenu SAML dla wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wystawianie oświadczeń hello toocustomize w w hello tokenie SAML dla wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Dostosowywanie oświadczeń wydanych w hello tokenie SAML dla wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory
Dzisiaj usługi Azure Active Directory obsługuje tysięcy wstępnie zintegrowanych aplikacji w galerii aplikacji usługi Azure AD, łącznie z ponad 360, która obsługuje logowanie jednokrotne hello przy użyciu protokołu hello SAML 2.0. Podczas uwierzytelniania użytkownika tooan aplikacji za pomocą usługi Azure AD za pomocą protokołu SAML, usługi Azure AD wysyła do aplikacji toohello tokenu (za pośrednictwem protokołu HTTP POST). A następnie, aplikacja hello weryfikuje i używa hello tokenu toolog hello użytkownika w zamiast monitowania o nazwę użytkownika i hasło. Te tokeny SAML zawierają informacje o użytkowniku hello znana jako "oświadczeń".

W tożsamości mowy, "roszczenie" informacje stwierdzający przez dostawcę tożsamości użytkownika w tokenie hello wydawać się one dla tego użytkownika. W [tokenu SAML](http://en.wikipedia.org/wiki/SAML_2.0), dane te zwykle znajduje się w hello instrukcję Attribute SAML. Witaj Unikatowy identyfikator użytkownika jest zazwyczaj reprezentowany w powitalne skrót jako identyfikator nazwy SAML podmiotu.

Domyślnie program Azure Active Directory wystawia aplikacji tooyour tokenu SAML, która zawiera oświadczenie NameIdentifier o wartości hello użytkownika (AKA główna nazwa użytkownika) w usłudze Azure AD. Ta wartość może jednoznacznie zidentyfikować hello użytkownika. Hello SAML token zawiera również dodatkowe roszczenia, zawierające adres e-mail użytkownika hello, imię i nazwisko.

wystawianie oświadczeń hello tooview lub edycji w hello aplikacji toohello tokenu SAML, otwórz hello aplikacji w portalu Azure. Następnie wybierz hello **widoku i edytować wszystkie atrybuty użytkowników** checkbox w hello **atrybuty użytkownika** części aplikacji hello.

![Użytkownik atrybutów sekcji][1]

Istnieją dwie możliwe przyczyny, dlaczego może być konieczne tooedit hello oświadczeń wydanych w tokenie SAML hello:
* Aplikacja Hello została zapisana toorequire inny zestaw oświadczeń identyfikatorów URI lub wartości oświadczeń.
* Aplikacja Hello została wdrożona w sposób, który wymaga hello NameIdentifier oświadczeń toobe inną niż hello username (AKA główna nazwa użytkownika) przechowywanych w usłudze Azure Active Directory.

Możesz edytować dowolne hello domyślnych wartości oświadczenia. Wybierz hello oświadczeń wiersza w tabeli atrybutów tokenu SAML hello. Spowoduje to otwarcie hello **atrybutu Edytuj** sekcji, a następnie możesz edytować nazwę oświadczenia, wartość oraz skojarzone z oświadczeń hello przestrzeni nazw.

![Edytuj atrybut użytkownika][2]

Można również usunąć oświadczeń (inne niż NameIdentifier) przy użyciu menu kontekstowe hello, który otwiera, klikając hello **...**  ikony.  Możesz także dodać nowe oświadczeń przy użyciu hello **Dodaj atrybut** przycisku.

![Edytuj atrybut użytkownika][3]

## <a name="editing-hello-nameidentifier-claim"></a>Edytowanie hello NameIdentifier oświadczeń
problem hello toosolve, gdzie aplikacja hello została wdrożona przy użyciu innej nazwy użytkownika, kliknij na powitania **identyfikator użytkownika** listy rozwijanej w hello **atrybuty użytkownika** sekcji. Ta akcja zawiera okno dialogowe z kilku różnych opcji:

![Edytuj atrybut użytkownika][4]

Witaj listy rozwijanej wybierz **user.mail** tooset hello NameIdentifier oświadczeń toobe hello adres e-mail użytkownika w katalogu hello. Lub wybierz **user.onpremisessamaccountname** nazwy konta SAM użytkownika toohello tooset, które zostały zsynchronizowane z lokalnej usługi Azure AD.

Można również użyć hello specjalne **ExtractMailPrefix()** sufiks domeny hello tooremove funkcja hello adres e-mail, nazwa konta SAM lub hello głównej nazwy użytkownika. Spowoduje to wyodrębnienie tylko nazwa hello pierwsza część hello użytkownika są przekazywane (na przykład "joe_smith" zamiast joe_smith@contoso.com).

![Edytuj atrybut użytkownika][5]

Teraz dodaliśmy również hello **join()** hello toojoin funkcja zweryfikowaną domeną z wartością identyfikatora użytkownika hello. Po wybraniu funkcji join() hello hello **identyfikator użytkownika** najpierw wybierz hello identyfikator użytkownika podobne wiadomości e-mail adres lub główna nazwa użytkownika, a następnie w w hello drugi rozwijanej wybierz zweryfikowanej domeny. Jeśli wybierz hello adres e-mail z hello zweryfikowanej domeny, a następnie usługi Azure AD wyodrębnia hello username z pierwszego joe_smith wartość hello z joe_smith@contoso.com i dołącza go z contoso.onmicrosoft.com. Zobacz poniższy przykład hello:

![Edytuj atrybut użytkownika][6]

## <a name="adding-claims"></a>Dodawanie oświadczeń
Podczas dodawania oświadczenia, można określić nazwy atrybutu hello (co nie wymaga ściśle toofollow wzorzec URI zgodnie z harmonogramem hello specyfikacji SAML). Atrybut hello wartość tooany użytkownika, który jest przechowywany w katalogu hello.

![Dodaj atrybut użytkownika][7]

Na przykład konieczne toosend dział hello hello użytkownika należy tooin organizacji jako oświadczeń (na przykład, sprzedaż). Wprowadź nazwę oświadczenia hello zgodnie z oczekiwaniami aplikacji hello, a następnie wybierz **user.department** jako wartość hello.

> [!NOTE]
> Jeśli dla danego użytkownika nie ma żadnej wartości przechowywanych dla wybranego atrybutu, następnie roszczenie nie został opublikowany w tokenie hello.

> [!TIP]
> Witaj **user.onpremisesecurityidentifier** i **user.onpremisesamaccountname** są obsługiwane tylko podczas synchronizowania danych użytkownika z lokalnej usługi Active Directory przy użyciu hello [Azure Narzędzie AD Connect](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Ograniczone oświadczeń

Brak niektórych ograniczeniami oświadczeń w SAML. Jeśli dodasz te oświadczenia, następnie usługi Azure AD nie będzie wysyłać te oświadczenia. Poniżej przedstawiono hello SAML ograniczony zestaw oświadczeń:

    | Typ oświadczenia (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/Expiration |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/EXPIRED |
    | http://schemas.microsoft.com/Identity/Claims/accesstoken |
    | http://schemas.microsoft.com/Identity/Claims/openid2_id |
    | http://schemas.microsoft.com/Identity/Claims/identityprovider |
    | http://schemas.microsoft.com/Identity/Claims/objectidentifier |
    | http://schemas.microsoft.com/Identity/Claims/PUID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/NameIdentifier [MR1] |
    | http://schemas.microsoft.com/Identity/Claims/tenantid |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationInstant |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationMethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/Claims/identityprovider |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/groups |
    | http://schemas.microsoft.com/Claims/groups.Link |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/role |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/Claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/Claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/Claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/Claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/Identity/Claims/Actor |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/samlissuername |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/confirmationkey |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsaccountname |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/primarygroupsid |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/Authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SID |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/denyonlysid |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsdevicegroup |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsfqbnversion |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowssubauthority |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/UPN |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/GroupSID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SPN |
    | http://schemas.microsoft.com/WS/2008/06/Identity/Claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/Identity/Claims/SCOPE |

## <a name="next-steps"></a>Następne kroki
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](../active-directory-apps-index.md)
* [Konfigurowanie jednego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory](../active-directory-saas-custom-apps.md)
* [Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png