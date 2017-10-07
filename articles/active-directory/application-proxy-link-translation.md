---
title: "aaaTranslate łącza i serwer Proxy aplikacji adresów URL usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstaw łączniki serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Przekieruj zapisane na stałe łącza do aplikacji opublikowanych przy użyciu serwera Proxy aplikacji usługi Azure AD

Serwer Proxy aplikacji usługi Azure AD sprawia, że z lokalnymi aplikacje dostępne toousers, zdalnej lub na ich własnych urządzeń. Niektóre aplikacje, jednak zostały opracowane z lokalnym łącza osadzonego w hello HTML. Tych linków nie działa prawidłowo, gdy aplikacja hello jest używany zdalnie. Masz kilka lokalnej aplikacji punktu tooeach innych użytkowników oczekiwać tookeep łącza hello pracy, gdy nie są one w biurze hello. 

Witaj najlepsze sposób toomake się, że pracy łącza hello sam zarówno wewnątrz i poza siecią firmową jest tooconfigure hello zewnętrzne adresy URL toobe Twojej aplikacji hello sam ich wewnętrzne adresy URL. Użyj [domen niestandardowych](active-directory-application-proxy-custom-domains.md) tooconfigure Twojego zewnętrznych toohave adresów URL, nazwę domeny firmowej zamiast domyślnej domeny serwera proxy aplikacji hello.

Jeśli domen niestandardowych nie można użyć w dzierżawie, funkcji tłumaczenia łącza powitania serwera proxy aplikacji zachowuje łącza działa niezależnie od tego, gdzie znajdują się użytkownicy. Znajdują się aplikacje punktu bezpośrednio toointernal punktów końcowych lub porty, możesz mapować te wewnętrzny toohello adresy URL publikowane zewnętrznego adresu URL serwera Proxy aplikacji. Po włączeniu tłumaczenia łącza, i wyszukuje serwer Proxy aplikacji za pomocą kodu HTML, CSS i JavaScript znaczniki dla łączy wewnętrznych opublikowane. Usługi serwera Proxy aplikacji hello przetwarza je tak, aby użytkownicy pobierają nieprzerwaną środowisko.

>[!NOTE]
>Witaj funkcji tłumaczenia łącza jest dla dzierżawcy, niezależnie od przyczyny, nie można użyć domen niestandardowych toohave hello tych samych adresów URL wewnętrznych i zewnętrznych dla swoich aplikacji. Przed włączeniem tej funkcji należy sprawdzić, czy [domen niestandardowych w serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-custom-domains.md) można skorzystać.
>
>Lub, jeśli aplikacja hello należy tooconfigure z tłumaczenia łącze jest programu SharePoint, zobacz [Konfigurowanie mapowań dostępu alternatywnego for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) dla innego łącza toomapping podejście.

## <a name="how-link-translation-works"></a>Jak połączyć działa tłumaczenia

Po uwierzytelnieniu gdy serwer proxy hello przekazuje użytkownika toohello danych aplikacji hello, serwer Proxy aplikacji skanuje aplikacji hello łączy zapisane na stałe i zastępuje je ich odpowiednich opublikowane zewnętrzne adresy URL.

Serwer Proxy aplikacji zakłada, że aplikacje są zakodowane w formacie UTF-8. Jeśli nie jest to przypadek hello, określ typ kodowania hello nagłówka odpowiedzi http, tak samo, jak `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Łączy, których dotyczy problem?

Funkcja tłumaczenia łączenia Hello wyszukuje tylko łącza, które znajdują się w kodu znaczników w treści hello aplikacji. Serwer Proxy aplikacji ma oddzielne funkcji tłumaczenia pliki cookie lub adresy URL w nagłówkach. 

Istnieją dwa typy typowe wewnętrzny łączy w lokalnych aplikacji:

- **Względne łączy wewnętrznych** tooa tego punktu udostępnionych zasobów w strukturze pliku lokalnego, takich jak `/claims/claims.html`. Te linki automatycznie działać w aplikacjach, które są publikowane za pośrednictwem serwera Proxy aplikacji i kontynuować toowork z lub bez tłumaczenia łącza. 
- **Łączy wewnętrznych zapisane na stałe** tooother lokalnej aplikacji, takich jak `http://expenses` lub opublikowane plików takich jak `http://expenses/logo.jpg`. Funkcja tłumaczenia łączenia Hello działa dla łączy wewnętrznych zapisane na stałe i zmiany ich toopoint toohello zewnętrzne adresy URL potrzebnych użytkownikom zdalnym w toogo za pośrednictwem.

### <a name="how-do-apps-link-tooeach-other"></a>Jak aplikacje link tooeach innych

Tłumaczenie łącze jest włączone dla każdej aplikacji, aby zachować kontrolę nad środowiskiem użytkownika hello na poziomie aplikacji hello. Włączyć łącze tłumaczenia dla aplikacji, gdy ma linki hello *z* translacji toobe tej aplikacji, nie łączy *do* danej aplikacji. 

Na przykład załóżmy, że masz trzech aplikacji opublikowanych przy użyciu serwera Proxy aplikacji, aby połączyć wszystkie tooeach innych: korzyści, kosztów i podróży. Brak aplikacji czwarty opinii, która nie jest opublikowana przy użyciu serwera Proxy aplikacji.

Po włączeniu łącze Translacja hello zalety aplikacji hello łącza tooExpenses i podróży są przekierowane toohello zewnętrzne adresy URL dla tych aplikacji, ale hello tooFeedback łącza nie zostanie przekierowana, ponieważ nie istnieje żadne zewnętrznego adresu URL. Łącza z kosztów i podróży tooBenefits Wstecz nie działa, ponieważ łącze tłumaczenia nie został włączony dla tych dwóch aplikacji.

![Łącza z korzyści tooother aplikacji po włączeniu tłumaczenia łącza](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Łącza, które nie są tłumaczone?

tooimprove wydajności i bezpieczeństwa, niektóre łącza są tłumaczone:

- Łącza nie wewnątrz znaczników kodu. 
- Łącza nie w HTML, CSS i JavaScript. 
- Łączy wewnętrznych otwarty z innych programów. Nie można przetłumaczyć łącza wysyłanych za pośrednictwem poczty e-mail lub wiadomości błyskawicznych lub zawarte w innych dokumentów. Witaj, użytkownicy muszą tooknow toogo toohello zewnętrznego adresu URL.

Należy toosupport jedną z tych dwóch scenariuszy użycia hello takie same wewnętrzne i zewnętrzne adresy URL zamiast tłumaczenia łącza.  

## <a name="enable-link-translation"></a>Włącz łącze tłumaczenia

Wprowadzenie do tłumaczenia łącze jest tak proste, jak kliknięcie przycisku:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Przejdź za**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** > aplikacji hello wybierz ma toomanage > **Serwera proxy aplikacji**.
3. Włącz **translacji adresów URL w aplikacji treści** za**tak**.

   ![W treści aplikacji wybierz adresy URL tootranslate tak](./media/application-proxy-link-translation/select_yes.png).
4. Wybierz **zapisać** tooapply zmiany.

Teraz gdy użytkownicy uzyskują dostęp do tej aplikacji, serwer proxy hello zostanie automatycznie skanowanie w poszukiwaniu wewnętrzne adresy URL, które zostały opublikowane za pośrednictwem serwera Proxy aplikacji w dzierżawie.

## <a name="send-feedback"></a>Wyślij opinię

Chcemy toomake Twojego pomocy tej pracy funkcji dla wszystkich aplikacji. Firma Microsoft wyszukiwania ponad 30 tagów w kodzie HTML i CSS i rozważa które toosupport przypadków JavaScript. Przykład wygenerowanego linki, które nie są tłumaczonym, przesyłać fragment kodu za[opinii serwera Proxy aplikacji](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Następne kroki
[Domen niestandardowych za pomocą serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-custom-domains.md) toohave hello tego samego adresu URL wewnętrznych i zewnętrznych

[Konfigurowanie mapowań dostępu alternatywnego for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx)
