---
title: aaaListing aplikacji w galerii aplikacji hello Azure Active Directory
description: "Jak toolist aplikacji, która obsługuje logowanie jednokrotne w hello galerii Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Wyświetlanie listy aplikacji w galerii aplikacji hello Azure Active Directory
toolist aplikacji, która obsługuje logowanie jednokrotne z usługą Azure Active Directory w hello [galerii Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplikacja hello musi najpierw tooimplement hello następujące tryby integracji:

* **OpenID Connect** — bezpośrednia Integracja z usługą Azure AD do uwierzytelniania przy użyciu protokołu OpenID Connect i hello Azure AD zgody interfejsu API dla konfiguracji. Jeśli aplikacja nie obsługuje SAML integracji jest uruchamiana, to hello zalecamy tryb.
* **SAML** — hello możliwości tooconfigure dostawcy tożsamości innych firm przy użyciu protokołu SAML hello ma już aplikacji.

Listę wymagań dotyczących każdego trybu są poniżej.

## <a name="openid-connect-integration"></a>OpenID Connect integracji
toointegrate aplikacji z usługą Azure AD, następujące hello [instrukcje developer](active-directory-authentication-scenarios.md). Następnie ukończyć powitalnych pytań poniżej i wysłać toowaadpartners@microsoft.com.

* Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacją, które mogą być używane przez hello Azure zespołu tootest hello integracji z usługą AD.  
* Zawierają informacje o tym jak zarejestrować się w team hello Azure AD i połącz wystąpienie aplikacji tooyour usługi Azure AD przy użyciu hello [framework zgody usługi Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Podaj wszelkie dodatkowe informacje wymagane dla hello Azure AD zespołu tootest rejestracji jednokrotnej z aplikacją. 
* Podaj poniższe informacje hello:

> Nazwa firmy:
> 
> Witryna sieci Web firmy:
> 
> Nazwa aplikacji:
> 
> Opis aplikacji (limit 200 znaków):
> 
> Aplikacji witryny sieci Web (informacyjnych):
> 
> Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:
> 
> Identyfikator aplikacji hello, jak pokazano w szczegółach aplikacji hello na https://portal.azure.com:
> 
> Adres URL z zapisywania się do aplikacji, gdzie toosign dla klientów i notebooka zakupu aplikacji hello:
> 
> Wybierz kategorie toothree Twojego toobe aplikacji na liście (aby dostępne kategorie Zobacz hello Azure Active Directory Marketplace):
> 
> Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):
> 
> Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):
> 
> Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):
> 
> 

## <a name="saml-integration"></a>Integrację SAML
Dowolną aplikację, który obsługuje SAML 2.0 może być bezpośrednio integrowany z dzierżawy usługi Azure AD przy użyciu [tooadd te instrukcje niestandardową aplikację](../active-directory-saas-custom-apps.md). Po przetestowaniu się, że integracją aplikacji współpracuje z usługą Azure AD, Wyślij hello zbyt następujących informacji<mailto:waadpartners@microsoft.com>.

* Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacją, które mogą być używane przez hello Azure zespołu tootest hello integracji z usługą AD.  
* Podaj hello SAML adres URL logowania, adres URL wystawcy (identyfikator jednostki,) i adres URL odpowiedzi (usługa konsumenta potwierdzenia) wartości dla aplikacji, zgodnie z opisem [tutaj](../active-directory-saas-custom-apps.md). Jeśli podasz zwykle te wartości jako część pliku metadanych SAML, można wysyłać również.
* Podaj krótki opis sposobu tooconfigure usługi Azure AD jako dostawcy tożsamości w aplikacji przy użyciu SAML 2.0. Jeśli aplikacja obsługuje konfigurowanie usługi Azure AD jako dostawcy tożsamości za pośrednictwem portalu samoobsługowego administracyjne, następnie sprawdź, czy poświadczenia hello podanego powyżej obejmują hello możliwości tooset to się.
* Podaj poniższe informacje hello:

> Nazwa firmy:
> 
> Witryna sieci Web firmy:
> 
> Nazwa aplikacji:
> 
> Opis aplikacji (limit 200 znaków):
> 
> Aplikacji witryny sieci Web (informacyjnych):
> 
> Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:
> 
> Adres URL z zapisywania się do aplikacji, gdzie toosign dla klientów i notebooka zakupu aplikacji hello:
> 
> Wybierz kategorie toothree Twojego toobe aplikacji kategorii (dostępne kategorie można znaleźć hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):
> 
> Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):
> 
> Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):
> 
> 

