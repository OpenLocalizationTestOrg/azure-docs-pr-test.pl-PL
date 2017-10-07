---
title: "toodebug aaaHow SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory
Podczas debugowania integracji aplikacji opartej na SAML, jest często przydatne toouse narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) toosee hello żądania, odpowiedzi SAML hello i hello rzeczywiste tokenu SAML wystawiony toohello aplikacji SAML. Przez sprawdzenie tokenu SAML hello, upewnij się, że wszystkie hello wymaganych atrybutów, hello nazwę użytkownika w hello SAML podmiotu, a Witaj wystawca identyfikatora URI są dostępne za pośrednictwem zgodnie z oczekiwaniami.

![][1]

Hello odpowiedzi z usługi Azure AD, który zawiera hello SAML token jest zwykle Witaj, który występuje po przekierowania HTTP 302 z https://login.windows.net i skonfigurowano wysłane toohello **adres URL odpowiedzi** aplikacji hello. 

Możesz wyświetlić tokenu SAML hello tego wiersza, a następnie zaznaczając hello **inspektorzy > WebForms** kartę hello prawym panelu. Z tego miejsca, kliknij prawym przyciskiem myszy hello **SAMLResponse** wartość, a następnie wybierz **wysyłania tooTextWizard**. Następnie wybierz **Base64 z** z hello **przekształcenie** menu toodecode hello token i wyświetlić jego zawartość.

**Uwaga**: toosee hello zawartość HTTP tego żądania, Fiddler może monitować odszyfrowywanie tooconfigure ruch protokołu HTTPS, który będzie potrzebny toodo.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](../active-directory-apps-index.md)
* [Konfigurowanie jednego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory](../active-directory-saas-custom-apps.md)
* [W jaki sposób tooCustomize oświadczenia wydane w hello tokenu SAML dla aplikacji Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png