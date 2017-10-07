---
title: "aaaIntegrate usługi Azure Active Directory logowania jednokrotnego dla aplikacji SaaS | Dokumentacja firmy Microsoft"
description: "Włączanie uwierzytelniania rejestracji jednokrotnej i inicjowania obsługi administracyjnej scentralizowanego zarządzania dostępu aplikacji SaaS w usłudze Azure Active Directory użytkownika. Podstawowe informacje o toointegrate usługi Azure Active Directory tooSaaS aplikacji."
services: active-directory
keywords: "Integrowanie usługi Azure AD dla aplikacji SaaS"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Integrowanie usługi Azure Active Directory logowania jednokrotnego dla aplikacji SaaS
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klasyczna witryna Azure Portal](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget pracy konfigurowania rejestracji jednokrotnej dla aplikacji, które w przypadku wprowadzenia w Twojej organizacji, używany będzie istniejący katalog w usłudze Azure Active Directory (Azure AD). Możesz użyć katalog usługi Azure AD, którą można uzyskać za pośrednictwem Microsoft Azure, Office 365 lub usługi Windows Intune. Jeśli masz dwie lub więcej z nich, zobacz [administrowanie katalogiem usługi Azure AD](active-directory-administer.md) toodetermine które toouse jeden.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak tooassign ról administratorów w usłudze Azure AD Witaj, Administratorze Centrum, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Authentication
W przypadku aplikacji, które obsługują hello SAML 2.0, WS-Federation, lub protokoły OpenID Connect, relacje zaufania tooestablish certyfikaty podpisywania używa usługi Azure Active Directory. Aby uzyskać więcej informacji na ten temat, zobacz [zarządzanie certyfikatami dla federacyjne logowanie jednokrotne](active-directory-sso-certs.md).

Dla aplikacji, które obsługują tylko HTML oparte na formularzach logowania, relacje zaufania tooestablish "archiwizowanie haseł" używa usługi Azure Active Directory. To użytkownicy w Twojej organizacji toobe hello zostanie automatycznie zalogowany tooa aplikacji SaaS przez usługę Azure AD przy użyciu informacji o koncie użytkownika hello z hello aplikacji SaaS. Usługi Azure AD zbiera i bezpiecznie przechowuje informacje o koncie użytkownika hello i hello powiązane hasło. Aby uzyskać więcej informacji, zobacz [opartego na hasłach rejestracji jednokrotnej](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autoryzacja
Konto elastycznie umożliwia toouse toobe autoryzowanych użytkowników aplikacji, po uwierzytelnienia za pośrednictwem rejestracji jednokrotnej. Inicjowanie obsługi użytkowników można ręcznie lub w niektórych przypadkach można dodawać i usuwać informacje o użytkowniku z aplikacji SaaS hello na podstawie zmian wprowadzonych w usłudze Azure Active Directory. Aby uzyskać więcej informacji na temat używania istniejące łączniki usługi Azure AD dla automatycznego inicjowania obsługi administracyjnej, zobacz [automatycznego użytkownika aprowizację i anulowanie obsługi dla aplikacji SaaS](active-directory-saas-app-provisioning.md).

W przeciwnym razie można ręcznie dodać aplikację tooan informacje użytkownika, lub użycie innych rozwiązań inicjowania obsługi, które są dostępne w witrynie marketplace hello.

## <a name="access"></a>Dostęp
Usługa Azure AD zapewnia różne sposoby dostosowania toodeploy aplikacji tooend użytkowników w organizacji. Nie są zablokowane do żadnego konkretnego wdrożenia rozwiązania dostępu. Można użyć [hello rozwiązania, które najlepiej odpowiada Twoim potrzebom](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Dodatkowe zagadnienia dotyczące aplikacji już w użyciu.
Konfigurowanie rejestracji jednokrotnej na dla aplikacji, która używa Twoja organizacja już jest inny proces z procesu tworzenia nowych kont dla nowej aplikacji hello. Istnieje kilka kroków wstępne w tym: Mapowanie tożsamości użytkownika w tożsamości tooAzure AD aplikacji hello i zrozumienie, jak użytkownicy mogą mieć rejestrowania w aplikacji tooan po jest zintegrowany.

> [!NOTE]
> tooset górę logowania jednokrotnego dla istniejącej aplikacji, niezbędne są uprawnienia administratora globalnego toohave w obu usługi Azure AD i hello aplikacji SaaS.
>
>

### <a name="mapping-user-accounts"></a>Mapowania konta użytkowników
Zazwyczaj tożsamość użytkownika ma unikatowy identyfikator, który może być adres e-mail lub główna nazwa użytkownika (UPN). Konieczne będzie toolink (map) tożsamość tootheir odpowiednich usługi Azure AD identity aplikacji każdego użytkownika. Istnieje kilka sposobów tooaccomplish to w zależności od tego, jak wymóg hello uwierzytelniania aplikacji.

Aby uzyskać więcej informacji o mapowaniu tożsamości aplikacji z tożsamości usługi Azure AD, zobacz [Dostosowywanie oświadczeń wydanych w tokenie SAML hello](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) i [Dostosowywanie mapowań atrybutów do inicjowania obsługi](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Opis hello użytkownika logowania
Po zintegrowaniu logowania jednokrotnego dla aplikacji, która jest już w użyciu, ważne jest toorealize, który hello środowisko użytkownika będzie dotyczył. Dla wszystkich aplikacji użytkowników zostanie uruchomiona przy użyciu ich toosign poświadczeń usługi Azure AD w. Przyczyną mogą być również, że muszą korzystać z aplikacji hello różnych tooaccess portalu.

Logowania jednokrotnego dla niektórych aplikacji może odbywać się na rejestracji aplikacji hello interfejsu, ale dla innych aplikacji hello będzie miał użytkownik toogo za pośrednictwem portalu centralnej takich jak ([Moje aplikacje](http://myapps.microsoft.com) lub [usługi Office 365](http://portal.office.com/myapps)) toosign w. Dowiedz się więcej o różnych typach hello logowania jednokrotnego i ich możliwości użytkowników w [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

Jest inny zasób cenne *zgody użytkownika z pominięciem* w hello [deweloperzy Guiding](active-directory-applications-guiding-developers-for-lob-applications.md) artykułu.

## <a name="next-steps"></a>Następne kroki
Dla aplikacji SaaS, które możesz znaleźć w galerii aplikacji hello, usługa Azure AD zapewnia szereg [samouczki dotyczące aplikacji SaaS toointegrate](active-directory-saas-tutorial-list.md).

Jeśli aplikacja nie jest w galerii aplikacji, możesz [dodać toohello galerii aplikacji Azure AD jako aplikację niestandardową](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Jest znacznie więcej szczegółów na wszystkich tych problemów w bibliotece witryny Azure.com hello, począwszy od [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

Ponadto nie zostały pominięte hello [indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md).
