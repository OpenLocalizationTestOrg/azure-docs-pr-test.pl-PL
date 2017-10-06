---
title: "punktu końcowego v2.0 usługi Azure AD toohello aaaChanges | Dokumentacja firmy Microsoft"
description: "Opis zmian wprowadzonych toohello app model v2.0 publicznej wersji zapoznawczej protokołów."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>Ważne aktualizacje toohello v2.0 protokoły uwierzytelniania
Deweloperzy uwagi! Za pośrednictwem hello przyszłych dwóch tygodni, wprowadzamy kilka aktualizacji tooour v2.0 protokoły, których może oznaczać fundamentalne zmiany dla wszystkich aplikacji, zapisane w okresie podglądu.  

## <a name="who-does-this-affect"></a>Kto to wpływa?
Wszystkie aplikacje zapisanych toouse hello v2.0 zbieżność punktu końcowego uwierzytelniania,

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Można znaleźć więcej informacji na temat punktu końcowego v2.0 hello [tutaj](active-directory-appmodel-v2-overview.md).

Jeśli zostały skompilowane aplikację, używając kodowania bezpośrednio toohello v2.0 protokół punktu końcowego v2.0 hello przy użyciu dowolnej z naszych OpenID Connect i OAuth middlewares sieci web lub przy użyciu innych 3 uwierzytelniania tooperform bibliotek firmy, należy przygotować tootest swoje projekty i upewnij zmiany w razie potrzeby.

## <a name="who-doesnt-this-affect"></a>Kto nie to mieć wpływ na?
Wszystkie aplikacje, które zostały zapisane do punktu końcowego uwierzytelniania usługi Azure AD w środowisku produkcyjnym hello,

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Ten protokół jest ustawiany w kamienie, a nie występują wszystkie zmiany.

Ponadto jeśli aplikacji **tylko** używa naszego uwierzytelniania tooperform biblioteki ADAL, toochange nie ma żadnych czynności.  Biblioteka ADAL ma osłonę aplikacji hello zmiany.  

## <a name="what-are-hello-changes"></a>Jakie są hello zmiany?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Usunięcie z nagłówków JWT hello x5t wartości
punktu końcowego v2.0 Hello korzysta z tokenów JWT często, która zawiera sekcja Parametry nagłówka o odpowiednie metadane dotyczące hello token.  Jeśli dekodowanie nagłówka hello jednego z naszych bieżącego tokenów Jwt, może znaleźć wyglądać mniej więcej tak:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Gdy obie właściwości "x5t" i "dziecko" hello identyfikacji klucza publicznego hello powinny być używane toovalidate hello token podpisu, ponieważ pobrana z punktu końcowego metadanych hello OpenID Connect.

zmiany Hello czynione tutaj jest tooremove hello "x5t" właściwości.  Możesz kontynuować hello toouse tego samego toovalidate mechanizmów tokeny, ale polegać wyłącznie na powitania "dziecko" właściwość tooretrieve hello prawidłowy klucz publiczny, jak określono w hello protokołu OpenID Connect. 

> [!IMPORTANT]
> **Zadania: Upewnij się, że aplikacja nie zależy od hello istnienie hello x5t wartość.**
> 
> 

### <a name="removing-profileinfo"></a>Usuwanie profile_info
Wcześniej punktu końcowego v2.0 hello ma zostały zwracając obiekt JSON kodowany w standardzie base64 w odpowiedzi tokenu o nazwie `profile_info`.  Podczas żądania tokenu dostępu z punktu końcowego v2.0 hello, wysyłając żądanie:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

odpowiedź Hello będzie wyglądać powitania po obiekt JSON:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Witaj `profile_info` wartość informacje o użytkowniku hello, która zarejestrowała się w aplikacji hello - ich nazwę wyświetlaną, imię, nazwisko, adres e-mail, identyfikator i tak dalej.  Przede wszystkim hello `profile_info` była używana do buforowania tokenu i wyświetlić celów.

Teraz zostaną usunięte hello `profile_info` wartość — nie martw się, nadal zapewniamy toodevelopers tej informacji w miejscu nieco inne.  Zamiast `profile_info`, teraz zwróci punktu końcowego v2.0 hello `id_token` w każdej odpowiedzi tokenu:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Może zdekodować i przeanalizować żądaniu hello tooretrieve hello informacje, które odebrano od profile_info.  żądaniu Hello jest JSON Web Token (JWT), o treści określonej przez OpenID Connect.  Hello kod ten powinien być bardzo podobna — wystarczy bliski hello tooextract segmentu (hello treść) żądaniu hello i base64 dekodowania obiekt JSON hello tooaccess w ciągu.

Za pośrednictwem hello przyszłych dwóch tygodni, powinien kodem aplikacji tooretrieve hello informacje o użytkowniku z obu hello `id_token` lub `profile_info`; zależności jest obecny.  W ten sposób w przypadku zmian hello aplikacji bezproblemowo może obsłużyć hello przejście od `profile_info` zbyt`id_token` bez przeszkód.

> [!IMPORTANT]
> **Zadania: Upewnij się, że aplikacja nie zależy od istnienia hello hello `profile_info` wartość.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Usuwanie id_token_expires_in
Podobnie za`profile_info`, zostaną również usunięte hello `id_token_expires_in` parametr z odpowiedzi.  Wcześniej punktu końcowego v2.0 hello zwróci wartość `id_token_expires_in` wraz z każdym odpowiedzi żądaniu, na przykład w odpowiedzi autoryzacji:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Lub w odpowiedzi tokenu:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Witaj `id_token_expires_in` wartość wskazuje hello liczbę sekund, żądaniu hello pozostanie dotyczy.  Teraz, zostaną usunięte hello `id_token_expires_in` wartości całkowite.  Zamiast tego można użyć standardowego protokołu OpenID Connect hello `nbf` i `exp` oświadczeń tooexamine hello ważności w żądaniu.  Zobacz hello [odwołania do tokenu v2.0](active-directory-v2-tokens.md) Aby uzyskać więcej informacji na temat tych oświadczeń.

> [!IMPORTANT]
> **Zadania: Upewnij się, że aplikacja nie zależy od istnienia hello hello `id_token_expires_in` wartość.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Zmiana oświadczeń hello zwrócony przez zakres = openid
Ta zmiana zostanie hello najważniejszych — w rzeczywistości, będzie miało wpływ na prawie każdej aplikacji, który używa hello punktu końcowego v2.0.  Wiele aplikacji wysyłania żądań toohello punktu końcowego v2.0 za pomocą hello `openid` zakresu, takie jak:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Obecnie, gdy użytkownik hello przyznaje zgody na powitania `openid` zakresu, aplikacji otrzymuje szereg informacji o użytkowniku hello hello wynikowa żądaniu.  Oświadczenia te mogą obejmować nazwy, preferowane nazwy użytkownika, adres e-mail i identyfikator obiektu.

W ramach tej aktualizacji, zmieniamy hello informacje o tym hello `openid` zakresu zapewnia dostęp aplikacji do comform toobetter z hello specyfikacji OpenID Connect.  Witaj `openid` zakresu zostanie tylko Zezwalaj toosign aplikacji hello użytkownika w i otrzymywanie identyfikator specyficzny dla aplikacji dla użytkownika hello hello `sub` oświadczeń o żądaniu hello.  Witaj oświadczeń w żądaniu z tylko hello `openid` zakres przyznane będzie pozbawione żadnych informacji umożliwiających identyfikację użytkownika.  Przykład żądaniu oświadczenia są:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Jeśli chcesz tooobtain dane osobowe lub informacje o użytkowniku hello w aplikacji, aplikacji należy toorequest dodatkowych uprawnień od hello użytkownika.  Wprowadzono obsługę dwa nowe zakresy z OpenID Connect specyfikacji hello — Witaj `email` i `profile` zakresy — które umożliwiają toodo tak.

* Witaj `email` zakres jest bardzo prosta — umożliwia aplikacji dostęp toohello użytkownika podstawowego adresu e-mail za pośrednictwem hello `email` oświadczeń w żądaniu hello.  Należy pamiętać, że hello `email` oświadczenia nie zawsze będą obecne w id_tokens — tylko zostanie on uwzględniony jeśli są dostępne w profilu użytkownika hello.
* Witaj `profile` zakresu zapewnia tooall dostępu do Twojej aplikacji inne podstawowe informacje dotyczące użytkownika hello — ich nazwy, preferowane username identyfikator obiektu i tak dalej.

Dzięki temu można toocode aplikacji w sposób minimalnego ujawnienie — możesz poprosić użytkownika hello właśnie hello zestawu informacje, że aplikacja wymaga toodo swojego zadania.  Jeśli chcesz toocontinue pobierania pełnego zestawu informacje o użytkowniku, który obecnie otrzymuje aplikacji hello, wszystkie trzy zakresy, należy uwzględnić w Twoich żądań autoryzacji:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Aplikację można rozpocząć wysyłanie hello `email` i `profile` natychmiast zakresy i punktu końcowego v2.0 hello będzie zaakceptować te dwa zakresy i rozpocząć żądanie uprawnień użytkowników w razie potrzeby.  Jednak zmienić hello w hello interpretacja hello `openid` zakres nie zostanie zastosowana dla kilka tygodni.

> [!IMPORTANT]
> **Zadania: Dodaj hello `profile` i `email` zakresów, jeśli aplikacja wymaga informacji na temat hello użytkownika.**  Należy pamiętać, że ADAL będzie zawierać oba te uprawnienia żądań domyślnie. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Usuwanie Witaj wystawca ukośnika.
Wcześniej Witaj wystawca wartość wyświetlana w tokenów z punktu końcowego v2.0 hello trwało hello formularza

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Gdzie hello identyfikator guid został tenantId hello dzierżawcy hello Azure AD, który wydał hello tokenu.  Wprowadzone zmiany staje się hello wartości wystawcy

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

w obu tokeny i hello OpenID Connect dokument.

> [!IMPORTANT]
> **Zadania: Upewnij się, że aplikacja akceptuje wartości wystawcy hello zarówno z i bez ukośnika podczas sprawdzania poprawności wystawcy.**
> 
> 

## <a name="why-change"></a>Dlaczego mam zmienić?
Witaj główną motywacją do wprowadzenia tych zmian jest zgodne z OpenID Connect standardowej specyfikacji hello toobe.  Będąc OpenID Connect zgodne mamy nadzieję toominimize różnice między integracji z usługami tożsamość firmy Microsoft oraz z innymi usługami tożsamościami w branży hello.  Chcemy toouse deweloperzy tooenable ich ulubionych typu open source bibliotek uwierzytelniania bez konieczności tooalter hello bibliotek tooaccommodate Microsoft różnice.

## <a name="what-can-you-do"></a>Co należy zrobić?
Obecnie można rozpocząć wprowadzania wszystkie zmiany hello opisane powyżej.  Należy natychmiast:

1. **Usuń wszelkie zależności hello `x5t` parametr nagłówka.**
2. **Obsługiwać hello przejście od `profile_info` zbyt`id_token` w odpowiedzi tokenu.**
3. **Usuń wszelkie zależności hello `id_token_expires_in` parametr odpowiedzi.**
4. **Dodaj hello `profile` i `email` zakresy tooyour aplikacji, jeśli aplikacja potrzebuje informacji użytkownika podstawowego.**
5. **Zaakceptuj wartości wystawcy tokenów zarówno z i bez ukośnika.**

Nasze [dokumentacji protokołu v2.0](active-directory-v2-protocols.md) został już zaktualizowany tooreflect te zmiany, mogą używać go jako odwołanie pomagające, zaktualizuj kod.

Jeśli masz dodatkowe pytania w zakresie hello hello zmian możesz wolnego tooreach poza toous w serwisie Twitter na @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Jak często będą protokołu zmian?
Firma Microsoft nie przewiduje dalsze fundamentalne zmiany toohello protokoły uwierzytelniania.  Firma Microsoft są celowo tworzenie pakietów te zmiany w jednej wersji, aby toogo za pośrednictwem procesu aktualizacji tego typu nie trzeba ponownie kiedykolwiek wkrótce.  Oczywiście będzie nadal toohello funkcje tooadd zbieżność v2.0 usługi uwierzytelniania, które użytkownik może skorzystać z, ale te zmiany należy dodatku i nie podziału istniejący kod.

Wreszcie chcemy toosay Dziękujemy za wypróbowanie kwestii okresie Podgląd hello.  Hello insights i doświadczenia naszych pilotażowe zostały nieoceniony w dotychczasowych i mamy nadzieję, że Twoje opinie i pomysły będzie tooshare.

Kodowanie przyjemność!

Witaj dzielenia tożsamość firmy Microsoft

