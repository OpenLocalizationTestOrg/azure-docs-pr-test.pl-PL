---
title: "Konfigurowanie aplikacji SaaS do współpracy B2B w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przykłady kodu i programu PowerShell dla usługi Azure Active Directory B2B współpracy"
services: active-directory
documentationcenter: 
author: sasubram
manager: mtillman
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
ms.openlocfilehash: dc0bb3950f30b2ea676de406538e3a463ad21429
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Konfigurowanie aplikacji SaaS do współpracy B2B

Azure współpracy B2B usługi Active Directory (Azure AD) współpracuje z większości aplikacji, które integrują się z usługą Azure AD. W tej sekcji możemy przeprowadzenie instrukcje dotyczące konfigurowania niektórych popularnych aplikacji SaaS do użytku z B2B usługi Azure AD.

Przed przyjrzymy się instrukcje specyficzne dla aplikacji, poniżej przedstawiono niektóre przyjąć reguł:

* Dla większości aplikacji ustawienia użytkownika musi mieć miejsce, ręcznie. Oznacza to użytkownicy muszą być utworzone ręcznie w aplikacji, jak również.

* Dla aplikacji, które obsługują automatyczne ustawienia, takie jak Dropbox zaproszeń do skorzystania z oddzielnych są tworzone za pomocą aplikacji. Użytkownicy muszą być koniecznie Zaakceptuj każde zaproszenie.

* Atrybuty użytkownika, aby uniknąć problemów z zniekształcone funkcja dysku profilu użytkownika (UPD) w gości, zawsze wartość **identyfikator użytkownika** do **user.mail**.


## <a name="dropbox-business"></a>Dropbox biznesowa

Aby umożliwić użytkownikom na logowanie przy użyciu konta organizacji, należy ręcznie skonfigurować skrzynki firm przy użyciu usługi Azure AD jako dostawcy tożsamości Security (Assertion Markup Language SAML). Jeśli nie skonfigurowano firm Dropbox Aby to zrobić, nie może ona Monituj ani w przeciwnym razie użytkownicy mogą logować się za pomocą usługi Azure AD.

1. Aby dodać aplikacja biznesowa Dropbox z usługą Azure AD, wybierz **aplikacje dla przedsiębiorstw** w okienku po lewej stronie, a następnie kliknij przycisk **Dodaj**.

  ![Przycisk "Dodaj" na stronie aplikacji przedsiębiorstwa](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. W **dodać aplikację** okna, wprowadź **dropbox** w polu wyszukiwania, a następnie wybierz **Dropbox dla firm** na liście wyników.

  ![Wyszukaj "dropbox" na stronie Dodawanie strony aplikacji](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Na **logowanie jednokrotne** wybierz pozycję **logowanie jednokrotne** w okienku po lewej stronie, a następnie wprowadź **user.mail** w **identyfikator użytkownika** pole. (Jest ustawiona jako nazwy UPN domyślnie.)

  ![Konfigurowanie rejestracji jednokrotnej dla aplikacji](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. Aby pobrać certyfikat do użycia na potrzeby konfiguracji usługi Dropbox, wybierz **Konfigurowanie skrzynki**, a następnie wybierz **SAML pojedynczy znak na adres URL usługi** na liście.

  ![Pobieranie certyfikatu na potrzeby konfiguracji skrzynki](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Zaloguj się do usługi Dropbox z logowania jednokrotnego adres URL z **logowanie jednokrotne** strony.

  ![Strona logowania usługi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. W menu, wybierz **konsoli administracyjnej**.

  ![Łącze "Konsola administratora" w menu skrzynki](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. W **uwierzytelniania** okno dialogowe, wybierz opcję **więcej**, Przekaż certyfikat, a następnie w **Zaloguj się w adresie URL** wprowadź SAML pojedynczy adres URL logowania.

  ![Link "Więcej" w oknie dialogowym zwinięte uwierzytelniania](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  !["Zaloguj się w adresie URL" w oknie dialogowym uwierzytelniania rozszerzonej](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. Aby skonfigurować ustawienia automatycznego użytkownika w portalu Azure, wybierz **inicjowania obsługi administracyjnej** w okienku po lewej stronie wybierz **automatyczne** w **inicjowania obsługi trybu** , a następnie wybierz **autoryzacji**.

  ![Konfigurowanie użytkownika automatycznego inicjowania obsługi w portalu Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Po gościa lub element członkowski użytkowników są skonfigurowane w aplikacji Dropbox, otrzymują oddzielne zaproszenia z Dropbox. Aby korzystać z usługi Dropbox logowania jednokrotnego, zapraszane osoby musi zaakceptować zaproszenie, klikając łącze w nim.

## <a name="box"></a>Box
Umożliwia użytkownikom uwierzytelnianie przy użyciu Federacji, która jest oparta na protokole SAML pole gości z użyciem konta usługi Azure AD. W ramach tej procedury należy przekazać do Box.com metadanych.

1. Dodaj aplikację pole z aplikacje przedsiębiorstwa.

2. Konfigurowanie rejestracji jednokrotnej w następującej kolejności:

  ![Konfiguruj okno rejestracji jednokrotnej](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. W **Zaloguj się na adres URL** Sprawdź, czy adres URL logowania jest odpowiednio ustawiony dla pola w portalu Azure. Ten adres URL jest adresem URL dzierżawy Box.com. Należy stosować konwencji nazewnictwa *https://.box.com*.  
 **Identyfikator** nie ma zastosowania do tej aplikacji, ale nadal jest widoczny jako pole obowiązkowe.

 b. W **identyfikator użytkownika** wprowadź **user.mail** (na potrzeby logowania jednokrotnego dla konta gościa).

 c. W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **Utwórz nowy certyfikat**.

 d. Aby rozpocząć konfigurowanie dzierżawy Box.com przy użyciu usługi Azure AD jako dostawcy tożsamości, Pobierz plik metadanych, a następnie zapisz go na lokalny dysk.

 e. Przekazuj pliku metadanych do pola obsługuje zespół, który konfiguruje rejestracji jednokrotnej dla Ciebie.

3. Ustawienia automatycznego użytkownika usługi Azure AD, w lewym okienku wybierz **inicjowania obsługi administracyjnej**, a następnie wybierz **autoryzacji**.

  ![Zezwolić usłudze Azure AD connect do pola](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Jak Dropbox zapraszane osoby pole zapraszane osoby muszą zrealizować ich zaproszenia od aplikacji Box.

## <a name="next-steps"></a>Następne kroki

Na współpracy B2B usługi Azure AD, zobacz następujące artykuły:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie do roli użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
