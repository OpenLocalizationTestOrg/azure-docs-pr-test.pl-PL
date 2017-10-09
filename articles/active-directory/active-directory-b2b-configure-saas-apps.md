---
title: "aplikacji SaaS aaaConfigure współpracy B2B w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przykłady kodu i programu PowerShell dla usługi Azure Active Directory B2B współpracy"
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Konfigurowanie aplikacji SaaS do współpracy B2B

Azure współpracy B2B usługi Active Directory (Azure AD) współpracuje z większości aplikacji, które integrują się z usługą Azure AD. W tej sekcji możemy przeprowadzenie instrukcje dotyczące konfigurowania niektórych popularnych aplikacji SaaS do użytku z B2B usługi Azure AD.

Przed przyjrzymy się instrukcje specyficzne dla aplikacji, poniżej przedstawiono niektóre przyjąć reguł:

* Dla większości aplikacji hello Instalator użytkownik musi ręcznie toohappen. Oznacza to użytkownicy muszą być utworzone ręcznie w aplikacji hello również.

* Dla aplikacji, które obsługują automatyczne ustawienia, takie jak Dropbox zaproszeń do skorzystania z oddzielnych są tworzone na podstawie aplikacji hello. Użytkownicy muszą być tooaccept się, że każde zaproszenie.

* Atrybuty użytkownika hello, toomitigate wszelkie problemy z zniekształcone funkcja dysku profilu użytkownika (UPD) w gości, zawsze wartość **identyfikator użytkownika** za**user.mail**.


## <a name="dropbox-business"></a>Dropbox biznesowa

tooenable toosign użytkowników w przy użyciu konta organizacji, należy ręcznie skonfigurować toouse skrzynki Business usługi Azure AD jako dostawcy tożsamości Security (Assertion Markup Language SAML). Jeśli skrzynki firm nie został skonfigurowany toodo tak, go nie Monituj lub w przeciwnym razie zezwolić toosign użytkowników za pomocą usługi Azure AD.

1. aplikacja biznesowa skrzynki hello tooadd do usługi Azure AD, wybierz **aplikacje dla przedsiębiorstw** w lewym okienku hello, a następnie kliknij **Dodaj**.

  ![przycisk "Dodaj" Hello na stronę aplikacji hello Enterprise](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. W hello **dodać aplikację** okna, wprowadź **dropbox** w hello pole wyszukiwania, a następnie wybierz **Dropbox dla firm** hello listy wyników.

  ![Wyszukaj "dropbox" na powitania Dodawanie strony aplikacji](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Na powitania **logowanie jednokrotne** wybierz pozycję **logowanie jednokrotne** w lewym okienku hello, a następnie wprowadź **user.mail** w hello **identyfikator użytkownika** pole. (Jest ustawiona jako nazwy UPN domyślnie.)

  ![Konfigurowanie rejestracji jednokrotnej dla aplikacji hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello certyfikatu toouse dla konfiguracji usługi Dropbox, wybierz **Konfigurowanie skrzynki**, a następnie wybierz **SAML pojedynczy znak na adres URL usługi** hello liście.

  ![Pobieranie certyfikatu hello konfiguracji skrzynki](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Logowanie tooDropbox z hello jednokrotnej adres URL z hello **logowanie jednokrotne** strony.

  ![Strona Hello logowania usługi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. W hello menu, wybierz **konsoli administracyjnej**.

  ![łącze "Konsola administratora" Hello, w menu skrzynki hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. W hello **uwierzytelniania** okno dialogowe, wybierz opcję **więcej**, Przekaż hello certyfikat, a następnie w hello **Zaloguj się w adresie URL** wprowadź adres URL hello SAML logowania jednokrotnego.

  ![Witaj link "Więcej" w oknie dialogowym uwierzytelniania hello zwinięte](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Witaj "Adres URL logowania" w hello rozszerzona uwierzytelniania, okno dialogowe](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. Ustawienia automatycznego użytkownika tooconfigure w hello portalu Azure, wybierz **inicjowania obsługi administracyjnej** wybierz w okienku po lewej stronie powitania **automatyczne** w hello **inicjowania obsługi trybu** , a następnie wybierz **Autoryzować**.

  ![Konfigurowanie użytkownika automatycznego inicjowania obsługi w hello portalu Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Po gościa lub element członkowski użytkowników są skonfigurowane w aplikacji Dropbox hello, otrzymują oddzielne zaproszenia z Dropbox. toouse skrzynki rejestracji jednokrotnej, zapraszane osoby muszą zaakceptować zaproszenie hello, klikając łącze w nim.

## <a name="box"></a>Box
Użytkownicy tooauthenticate pole gości z użyciem konta usługi Azure AD można włączyć, używając federacyjnego, który bazuje na powitania protokołu SAML. W tej procedurze możesz przekazać tooBox.com metadanych.

1. Dodaj aplikację pole hello z hello aplikacje przedsiębiorstwa.

2. Konfigurowanie rejestracji jednokrotnej w następującej kolejności hello:

  ![Konfiguruj okno rejestracji jednokrotnej](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. W hello **Zaloguj się na adres URL** Sprawdź, czy hello adres URL logowania jest odpowiednio ustawiony dla pola w hello portalu Azure. Ten adres URL jest adresem URL hello dzierżawy Box.com. Należy stosować konwencję nazewnictwa hello *https://.box.com*.  
 Witaj **identyfikator** nie ma zastosowania toothis aplikacji, ale nadal jest wyświetlany jako pole obowiązkowe.

 b. W hello **identyfikator użytkownika** wprowadź **user.mail** (na potrzeby logowania jednokrotnego dla konta gościa).

 c. W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **Utwórz nowy certyfikat**.

 d. toobegin konfigurowanie Twojego Box.com toouse dzierżawy usługi Azure AD jako dostawcy tożsamości, Pobierz plik metadanych hello, a następnie zapisz tooyour dysku lokalnego.

 e. Przesyła hello metadanych pliku toohello pole zespołem pomocy technicznej, który konfiguruje rejestracji jednokrotnej dla Ciebie.

3. Ustawienia automatycznego użytkownika usługi Azure AD, w okienku po lewej stronie powitania, wybierz **inicjowania obsługi administracyjnej**, a następnie wybierz **autoryzacji**.

  ![Autoryzowanie tooBox tooconnect usługi Azure AD](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Jak Dropbox zapraszane osoby pole zapraszane osoby muszą zrealizować ich zaproszenia od hello okno aplikacji.

## <a name="next-steps"></a>Następne kroki

Zobacz następujące artykuły dotyczące współpracy B2B usługi Azure AD hello:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
