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
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="0064f-103">Ważne aktualizacje toohello v2.0 protokoły uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="0064f-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="0064f-104">Deweloperzy uwagi!</span><span class="sxs-lookup"><span data-stu-id="0064f-104">Attention developers!</span></span> <span data-ttu-id="0064f-105">Za pośrednictwem hello przyszłych dwóch tygodni, wprowadzamy kilka aktualizacji tooour v2.0 protokoły, których może oznaczać fundamentalne zmiany dla wszystkich aplikacji, zapisane w okresie podglądu.</span><span class="sxs-lookup"><span data-stu-id="0064f-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="0064f-106">Kto to wpływa?</span><span class="sxs-lookup"><span data-stu-id="0064f-106">Who does this affect?</span></span>
<span data-ttu-id="0064f-107">Wszystkie aplikacje zapisanych toouse hello v2.0 zbieżność punktu końcowego uwierzytelniania,</span><span class="sxs-lookup"><span data-stu-id="0064f-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="0064f-108">Można znaleźć więcej informacji na temat punktu końcowego v2.0 hello [tutaj](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0064f-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="0064f-109">Jeśli zostały skompilowane aplikację, używając kodowania bezpośrednio toohello v2.0 protokół punktu końcowego v2.0 hello przy użyciu dowolnej z naszych OpenID Connect i OAuth middlewares sieci web lub przy użyciu innych 3 uwierzytelniania tooperform bibliotek firmy, należy przygotować tootest swoje projekty i upewnij zmiany w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0064f-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="0064f-110">Kto nie to mieć wpływ na?</span><span class="sxs-lookup"><span data-stu-id="0064f-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="0064f-111">Wszystkie aplikacje, które zostały zapisane do punktu końcowego uwierzytelniania usługi Azure AD w środowisku produkcyjnym hello,</span><span class="sxs-lookup"><span data-stu-id="0064f-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="0064f-112">Ten protokół jest ustawiany w kamienie, a nie występują wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="0064f-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="0064f-113">Ponadto jeśli aplikacji **tylko** używa naszego uwierzytelniania tooperform biblioteki ADAL, toochange nie ma żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="0064f-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="0064f-114">Biblioteka ADAL ma osłonę aplikacji hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="0064f-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="0064f-115">Jakie są hello zmiany?</span><span class="sxs-lookup"><span data-stu-id="0064f-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="0064f-116">Usunięcie z nagłówków JWT hello x5t wartości</span><span class="sxs-lookup"><span data-stu-id="0064f-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="0064f-117">punktu końcowego v2.0 Hello korzysta z tokenów JWT często, która zawiera sekcja Parametry nagłówka o odpowiednie metadane dotyczące hello token.</span><span class="sxs-lookup"><span data-stu-id="0064f-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="0064f-118">Jeśli dekodowanie nagłówka hello jednego z naszych bieżącego tokenów Jwt, może znaleźć wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="0064f-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="0064f-119">Gdy obie właściwości "x5t" i "dziecko" hello identyfikacji klucza publicznego hello powinny być używane toovalidate hello token podpisu, ponieważ pobrana z punktu końcowego metadanych hello OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0064f-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="0064f-120">zmiany Hello czynione tutaj jest tooremove hello "x5t" właściwości.</span><span class="sxs-lookup"><span data-stu-id="0064f-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="0064f-121">Możesz kontynuować hello toouse tego samego toovalidate mechanizmów tokeny, ale polegać wyłącznie na powitania "dziecko" właściwość tooretrieve hello prawidłowy klucz publiczny, jak określono w hello protokołu OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0064f-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0064f-122">**Zadania: Upewnij się, że aplikacja nie zależy od hello istnienie hello x5t wartość.**</span><span class="sxs-lookup"><span data-stu-id="0064f-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="0064f-123">Usuwanie profile_info</span><span class="sxs-lookup"><span data-stu-id="0064f-123">Removing profile_info</span></span>
<span data-ttu-id="0064f-124">Wcześniej punktu końcowego v2.0 hello ma zostały zwracając obiekt JSON kodowany w standardzie base64 w odpowiedzi tokenu o nazwie `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="0064f-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="0064f-125">Podczas żądania tokenu dostępu z punktu końcowego v2.0 hello, wysyłając żądanie:</span><span class="sxs-lookup"><span data-stu-id="0064f-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="0064f-126">odpowiedź Hello będzie wyglądać powitania po obiekt JSON:</span><span class="sxs-lookup"><span data-stu-id="0064f-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="0064f-127">Witaj `profile_info` wartość informacje o użytkowniku hello, która zarejestrowała się w aplikacji hello - ich nazwę wyświetlaną, imię, nazwisko, adres e-mail, identyfikator i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="0064f-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="0064f-128">Przede wszystkim hello `profile_info` była używana do buforowania tokenu i wyświetlić celów.</span><span class="sxs-lookup"><span data-stu-id="0064f-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="0064f-129">Teraz zostaną usunięte hello `profile_info` wartość — nie martw się, nadal zapewniamy toodevelopers tej informacji w miejscu nieco inne.</span><span class="sxs-lookup"><span data-stu-id="0064f-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="0064f-130">Zamiast `profile_info`, teraz zwróci punktu końcowego v2.0 hello `id_token` w każdej odpowiedzi tokenu:</span><span class="sxs-lookup"><span data-stu-id="0064f-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="0064f-131">Może zdekodować i przeanalizować żądaniu hello tooretrieve hello informacje, które odebrano od profile_info.</span><span class="sxs-lookup"><span data-stu-id="0064f-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="0064f-132">żądaniu Hello jest JSON Web Token (JWT), o treści określonej przez OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0064f-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="0064f-133">Hello kod ten powinien być bardzo podobna — wystarczy bliski hello tooextract segmentu (hello treść) żądaniu hello i base64 dekodowania obiekt JSON hello tooaccess w ciągu.</span><span class="sxs-lookup"><span data-stu-id="0064f-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="0064f-134">Za pośrednictwem hello przyszłych dwóch tygodni, powinien kodem aplikacji tooretrieve hello informacje o użytkowniku z obu hello `id_token` lub `profile_info`; zależności jest obecny.</span><span class="sxs-lookup"><span data-stu-id="0064f-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="0064f-135">W ten sposób w przypadku zmian hello aplikacji bezproblemowo może obsłużyć hello przejście od `profile_info` zbyt`id_token` bez przeszkód.</span><span class="sxs-lookup"><span data-stu-id="0064f-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0064f-136">**Zadania: Upewnij się, że aplikacja nie zależy od istnienia hello hello `profile_info` wartość.**</span><span class="sxs-lookup"><span data-stu-id="0064f-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="0064f-137">Usuwanie id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="0064f-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="0064f-138">Podobnie za`profile_info`, zostaną również usunięte hello `id_token_expires_in` parametr z odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0064f-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="0064f-139">Wcześniej punktu końcowego v2.0 hello zwróci wartość `id_token_expires_in` wraz z każdym odpowiedzi żądaniu, na przykład w odpowiedzi autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="0064f-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="0064f-140">Lub w odpowiedzi tokenu:</span><span class="sxs-lookup"><span data-stu-id="0064f-140">Or in a token response:</span></span>

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

<span data-ttu-id="0064f-141">Witaj `id_token_expires_in` wartość wskazuje hello liczbę sekund, żądaniu hello pozostanie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="0064f-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="0064f-142">Teraz, zostaną usunięte hello `id_token_expires_in` wartości całkowite.</span><span class="sxs-lookup"><span data-stu-id="0064f-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="0064f-143">Zamiast tego można użyć standardowego protokołu OpenID Connect hello `nbf` i `exp` oświadczeń tooexamine hello ważności w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="0064f-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="0064f-144">Zobacz hello [odwołania do tokenu v2.0](active-directory-v2-tokens.md) Aby uzyskać więcej informacji na temat tych oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0064f-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0064f-145">**Zadania: Upewnij się, że aplikacja nie zależy od istnienia hello hello `id_token_expires_in` wartość.**</span><span class="sxs-lookup"><span data-stu-id="0064f-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="0064f-146">Zmiana oświadczeń hello zwrócony przez zakres = openid</span><span class="sxs-lookup"><span data-stu-id="0064f-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="0064f-147">Ta zmiana zostanie hello najważniejszych — w rzeczywistości, będzie miało wpływ na prawie każdej aplikacji, który używa hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="0064f-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="0064f-148">Wiele aplikacji wysyłania żądań toohello punktu końcowego v2.0 za pomocą hello `openid` zakresu, takie jak:</span><span class="sxs-lookup"><span data-stu-id="0064f-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="0064f-149">Obecnie, gdy użytkownik hello przyznaje zgody na powitania `openid` zakresu, aplikacji otrzymuje szereg informacji o użytkowniku hello hello wynikowa żądaniu.</span><span class="sxs-lookup"><span data-stu-id="0064f-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="0064f-150">Oświadczenia te mogą obejmować nazwy, preferowane nazwy użytkownika, adres e-mail i identyfikator obiektu.</span><span class="sxs-lookup"><span data-stu-id="0064f-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="0064f-151">W ramach tej aktualizacji, zmieniamy hello informacje o tym hello `openid` zakresu zapewnia dostęp aplikacji do comform toobetter z hello specyfikacji OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0064f-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="0064f-152">Witaj `openid` zakresu zostanie tylko Zezwalaj toosign aplikacji hello użytkownika w i otrzymywanie identyfikator specyficzny dla aplikacji dla użytkownika hello hello `sub` oświadczeń o żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="0064f-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="0064f-153">Witaj oświadczeń w żądaniu z tylko hello `openid` zakres przyznane będzie pozbawione żadnych informacji umożliwiających identyfikację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0064f-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="0064f-154">Przykład żądaniu oświadczenia są:</span><span class="sxs-lookup"><span data-stu-id="0064f-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="0064f-155">Jeśli chcesz tooobtain dane osobowe lub informacje o użytkowniku hello w aplikacji, aplikacji należy toorequest dodatkowych uprawnień od hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0064f-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="0064f-156">Wprowadzono obsługę dwa nowe zakresy z OpenID Connect specyfikacji hello — Witaj `email` i `profile` zakresy — które umożliwiają toodo tak.</span><span class="sxs-lookup"><span data-stu-id="0064f-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="0064f-157">Witaj `email` zakres jest bardzo prosta — umożliwia aplikacji dostęp toohello użytkownika podstawowego adresu e-mail za pośrednictwem hello `email` oświadczeń w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="0064f-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="0064f-158">Należy pamiętać, że hello `email` oświadczenia nie zawsze będą obecne w id_tokens — tylko zostanie on uwzględniony jeśli są dostępne w profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="0064f-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="0064f-159">Witaj `profile` zakresu zapewnia tooall dostępu do Twojej aplikacji inne podstawowe informacje dotyczące użytkownika hello — ich nazwy, preferowane username identyfikator obiektu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="0064f-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="0064f-160">Dzięki temu można toocode aplikacji w sposób minimalnego ujawnienie — możesz poprosić użytkownika hello właśnie hello zestawu informacje, że aplikacja wymaga toodo swojego zadania.</span><span class="sxs-lookup"><span data-stu-id="0064f-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="0064f-161">Jeśli chcesz toocontinue pobierania pełnego zestawu informacje o użytkowniku, który obecnie otrzymuje aplikacji hello, wszystkie trzy zakresy, należy uwzględnić w Twoich żądań autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="0064f-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="0064f-162">Aplikację można rozpocząć wysyłanie hello `email` i `profile` natychmiast zakresy i punktu końcowego v2.0 hello będzie zaakceptować te dwa zakresy i rozpocząć żądanie uprawnień użytkowników w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0064f-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="0064f-163">Jednak zmienić hello w hello interpretacja hello `openid` zakres nie zostanie zastosowana dla kilka tygodni.</span><span class="sxs-lookup"><span data-stu-id="0064f-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0064f-164">**Zadania: Dodaj hello `profile` i `email` zakresów, jeśli aplikacja wymaga informacji na temat hello użytkownika.**</span><span class="sxs-lookup"><span data-stu-id="0064f-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="0064f-165">Należy pamiętać, że ADAL będzie zawierać oba te uprawnienia żądań domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0064f-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="0064f-166">Usuwanie Witaj wystawca ukośnika.</span><span class="sxs-lookup"><span data-stu-id="0064f-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="0064f-167">Wcześniej Witaj wystawca wartość wyświetlana w tokenów z punktu końcowego v2.0 hello trwało hello formularza</span><span class="sxs-lookup"><span data-stu-id="0064f-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="0064f-168">Gdzie hello identyfikator guid został tenantId hello dzierżawcy hello Azure AD, który wydał hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="0064f-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="0064f-169">Wprowadzone zmiany staje się hello wartości wystawcy</span><span class="sxs-lookup"><span data-stu-id="0064f-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="0064f-170">w obu tokeny i hello OpenID Connect dokument.</span><span class="sxs-lookup"><span data-stu-id="0064f-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0064f-171">**Zadania: Upewnij się, że aplikacja akceptuje wartości wystawcy hello zarówno z i bez ukośnika podczas sprawdzania poprawności wystawcy.**</span><span class="sxs-lookup"><span data-stu-id="0064f-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="0064f-172">Dlaczego mam zmienić?</span><span class="sxs-lookup"><span data-stu-id="0064f-172">Why change?</span></span>
<span data-ttu-id="0064f-173">Witaj główną motywacją do wprowadzenia tych zmian jest zgodne z OpenID Connect standardowej specyfikacji hello toobe.</span><span class="sxs-lookup"><span data-stu-id="0064f-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="0064f-174">Będąc OpenID Connect zgodne mamy nadzieję toominimize różnice między integracji z usługami tożsamość firmy Microsoft oraz z innymi usługami tożsamościami w branży hello.</span><span class="sxs-lookup"><span data-stu-id="0064f-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="0064f-175">Chcemy toouse deweloperzy tooenable ich ulubionych typu open source bibliotek uwierzytelniania bez konieczności tooalter hello bibliotek tooaccommodate Microsoft różnice.</span><span class="sxs-lookup"><span data-stu-id="0064f-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="0064f-176">Co należy zrobić?</span><span class="sxs-lookup"><span data-stu-id="0064f-176">What can you do?</span></span>
<span data-ttu-id="0064f-177">Obecnie można rozpocząć wprowadzania wszystkie zmiany hello opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="0064f-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="0064f-178">Należy natychmiast:</span><span class="sxs-lookup"><span data-stu-id="0064f-178">You should immediately:</span></span>

1. <span data-ttu-id="0064f-179">**Usuń wszelkie zależności hello `x5t` parametr nagłówka.**</span><span class="sxs-lookup"><span data-stu-id="0064f-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="0064f-180">**Obsługiwać hello przejście od `profile_info` zbyt`id_token` w odpowiedzi tokenu.**</span><span class="sxs-lookup"><span data-stu-id="0064f-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="0064f-181">**Usuń wszelkie zależności hello `id_token_expires_in` parametr odpowiedzi.**</span><span class="sxs-lookup"><span data-stu-id="0064f-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="0064f-182">**Dodaj hello `profile` i `email` zakresy tooyour aplikacji, jeśli aplikacja potrzebuje informacji użytkownika podstawowego.**</span><span class="sxs-lookup"><span data-stu-id="0064f-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="0064f-183">**Zaakceptuj wartości wystawcy tokenów zarówno z i bez ukośnika.**</span><span class="sxs-lookup"><span data-stu-id="0064f-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="0064f-184">Nasze [dokumentacji protokołu v2.0](active-directory-v2-protocols.md) został już zaktualizowany tooreflect te zmiany, mogą używać go jako odwołanie pomagające, zaktualizuj kod.</span><span class="sxs-lookup"><span data-stu-id="0064f-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="0064f-185">Jeśli masz dodatkowe pytania w zakresie hello hello zmian możesz wolnego tooreach poza toous w serwisie Twitter na @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="0064f-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="0064f-186">Jak często będą protokołu zmian?</span><span class="sxs-lookup"><span data-stu-id="0064f-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="0064f-187">Firma Microsoft nie przewiduje dalsze fundamentalne zmiany toohello protokoły uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0064f-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="0064f-188">Firma Microsoft są celowo tworzenie pakietów te zmiany w jednej wersji, aby toogo za pośrednictwem procesu aktualizacji tego typu nie trzeba ponownie kiedykolwiek wkrótce.</span><span class="sxs-lookup"><span data-stu-id="0064f-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="0064f-189">Oczywiście będzie nadal toohello funkcje tooadd zbieżność v2.0 usługi uwierzytelniania, które użytkownik może skorzystać z, ale te zmiany należy dodatku i nie podziału istniejący kod.</span><span class="sxs-lookup"><span data-stu-id="0064f-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="0064f-190">Wreszcie chcemy toosay Dziękujemy za wypróbowanie kwestii okresie Podgląd hello.</span><span class="sxs-lookup"><span data-stu-id="0064f-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="0064f-191">Hello insights i doświadczenia naszych pilotażowe zostały nieoceniony w dotychczasowych i mamy nadzieję, że Twoje opinie i pomysły będzie tooshare.</span><span class="sxs-lookup"><span data-stu-id="0064f-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="0064f-192">Kodowanie przyjemność!</span><span class="sxs-lookup"><span data-stu-id="0064f-192">Happy coding!</span></span>

<span data-ttu-id="0064f-193">Witaj dzielenia tożsamość firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="0064f-193">hello Microsoft Identity Division</span></span>

