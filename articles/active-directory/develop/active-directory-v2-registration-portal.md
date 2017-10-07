---
title: Tematy pomocy portalu rejestracji aaaApp | Dokumentacja firmy Microsoft
description: "Opis różnych funkcji w portalu rejestracji aplikacji Microsoft hello."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Informacje dotyczące rejestracji aplikacji
Ten dokument zawiera kontekstu i opisy różnych funkcji w portalu rejestracji aplikacji Microsoft hello [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Moje aplikacje
Ta lista zawiera wszystkie aplikacje zarejestrowany do użytkowania z punktem końcowym v2.0 usługi Azure AD hello.  Te aplikacje mają toosign możliwości hello w użytkownikom oba konta osobiste z konta Microsoft i kont pracy/służbowych z usługi Azure Active Directory.  toolearn więcej informacji na temat punktu końcowego v2.0 hello Azure AD, zobacz nasze [omówienie v2.0](active-directory-appmodel-v2-overview.md).  Te aplikacje mogą być również używane toointegrate z końcowym uwierzytelniania konta Microsoft hello, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Na żywo aplikacji zestawu SDK
Ta lista zawiera wszystkie aplikacje zarejestrowany do użytkowania wyłącznie z kontem Microsoft.  Nie są włączone do użytku w usłudze Azure Active Directory ani.  Jest to, gdzie można znaleźć wszystkie aplikacje, które wcześniej został zarejestrowany z portalu dla deweloperów MSA hello na `https://account.live.com/developers/applications`.  Wszystkie funkcje, które należy wcześniej wykonać `https://account.live.com/developers/applications` można teraz wykonać w tym nowego portalu `https://apps.dev.microsoft.com`.  Jeśli masz dodatkowe pytania dotyczące aplikacji konta Microsoft, skontaktuj się z nami.

## <a name="application-secrets"></a>Klucze tajne aplikacji
Aplikacji kluczy tajnych są poświadczeniami, umożliwiające niezawodne tooperform Twojej aplikacji [uwierzytelnianie klienta](http://tools.ietf.org/html/rfc6749#section-2.3) z usługą Azure AD.  OAuth i OpenID Connect klucze tajne aplikacji jest często określonego tooas `client_secret`.  W protokole v2.0 hello, każda aplikacja, która odbiera token zabezpieczający w lokalizacji adresowanego sieci web (przy użyciu `https` schemat) należy użyć tooidentify tajne aplikacji, sama tooAzure AD po realizacji tego tokenu zabezpieczającego.  Ponadto dowolnego klienta natywnego, czy tokeny recieves na urządzeniu będzie zabronione z przy użyciu uwierzytelniania klienta tooperform tajne aplikacji, toodiscourage hello magazynu kluczy tajnych w środowiskach niezabezpieczonych.

Każda aplikacja może zawierać dwóch hasła prawidłową aplikacją na dowolnym etapie w czasie.  Dzięki utrzymywaniu dwa klucze tajne, masz okresowe przerzucania klucza hello ablilty tooperform w środowisku całej aplikacji.  Po dokonaniu migracji całości hello aplikacji tooa nowego klucza tajnego, możesz usunąć stary klucz tajny hello i zainicjowania obsługi kolejnego.

W tej chwili tylko dwa typy aplikacji kluczy tajnych są dozwolone w portalu rejestracji aplikacji hello.  Wybieranie **wygenerować nowe hasło** będzie generować i przechowywać wspólny klucz tajny w magazynie danych odpowiednich hello, którego można użyć w aplikacji.  Wybieranie **wygenerować nową parę klucz** spowoduje utworzenie pary kluczy publiczny/prywatny nowych zostanie pobrany i używane do tooAzure uwierzytelniania klienta usługi AD.

## <a name="profile"></a>Profil
Witaj profilu części portalu rejestracji aplikacji hello może być używany znak hello toocustomize stronie aplikacji.  W tej chwili można zmienić logowania hello strony aplikacji logo, warunków adres URL usługi i zasady zachowania poufności informacji.  Witaj logo musi być przezroczyste 48 x 48 lub 50 x 50 pikseli obraz w pliku GIF, PNG lub JPEG 15 KB lub mniej.  Spróbuj zmienić wartości hello i wyświetlanie hello co strona logowania!

## <a name="live-sdk-support"></a>Obsługa w zestawie SDK na żywo
Po włączeniu "Live SDK Obsługa" przechowuje dowolnej aplikacji, które będą udostępniane klucze tajne, które możesz utworzyć w zarówno hello Azure AD, jak i dane Account Microsoft.  Pozwoli to toointegrate Twojej aplikacji bezpośrednio z hello Account Microsoft service (login.live.com).  W razie potrzeby toobuild aplikacji za pomocą Account Microsoft bezpośrednio (w przeciwieństwie toousing punktu końcowego v2.0 hello Azure AD), użytkownik powinien upewnić się, czy włączona jest obsługa Live SDK.

Wyłączenie obsługi zestaw Live SDK zagwarantować, że ten klucz tajny aplikacji hello tylko są zapisywane w magazynie danych hello Azure AD.  Magazyn danych Hello Azure AD zawiera wykonawcze korporacyjnej, umożliwiających toomeet pewne standardy, takie jak FISMA zgodności.  Jeśli zostanie włączona obsługa zestaw Live SDK, aplikacja może nie zapewnienia zgodności z niektóre z tymi standardami.

Jeśli planujesz tylko toouse punktu końcowego v2.0 usługi Azure AD dla hello, można bezpiecznie wyłączyć zestaw Live SDK pomocy technicznej.

