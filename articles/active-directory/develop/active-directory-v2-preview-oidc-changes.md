---
title: "Zmienia się z punktem końcowym v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opis zmian wprowadzonych w protokołach app model v2.0 publicznej wersji zapoznawczej."
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="becc3-103">Ważne aktualizacje protokoły uwierzytelniania w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="becc3-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="becc3-104">Deweloperzy uwagi!</span><span class="sxs-lookup"><span data-stu-id="becc3-104">Attention developers!</span></span> <span data-ttu-id="becc3-105">W ciągu przyszłych dwóch tygodni wprowadzamy kilka aktualizacji do naszej v2.0 protokoły uwierzytelniania, które może oznaczać fundamentalne zmiany dla wszystkich aplikacji, zapisane w okresie podglądu.</span><span class="sxs-lookup"><span data-stu-id="becc3-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="becc3-106">Kto to wpływa?</span><span class="sxs-lookup"><span data-stu-id="becc3-106">Who does this affect?</span></span>
<span data-ttu-id="becc3-107">Wszystkie aplikacje, które zostały zapisane do użycia w wersji 2.0 zbieżność punktu końcowego uwierzytelniania,</span><span class="sxs-lookup"><span data-stu-id="becc3-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="becc3-108">Można znaleźć więcej informacji na temat punktu końcowego v2.0 [tutaj](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="becc3-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="becc3-109">Jeśli utworzono aplikację, używając kodowania bezpośrednio do protokołu v2.0 punktu końcowego v2.0, za pomocą dowolnej z naszych OpenID Connect i OAuth middlewares sieci web lub innych 3 bibliotek strony do uwierzytelniania, musisz powinna być przygotowana do testowania projektów i wprowadzić zmiany, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="becc3-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="becc3-110">Kto nie to mieć wpływ na?</span><span class="sxs-lookup"><span data-stu-id="becc3-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="becc3-111">Wszystkie aplikacje, które zostały napisane względem punktu końcowego uwierzytelniania usługi Azure AD w środowisku produkcyjnym,</span><span class="sxs-lookup"><span data-stu-id="becc3-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="becc3-112">Ten protokół jest ustawiany w kamienie, a nie występują wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="becc3-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="becc3-113">Ponadto jeśli aplikacja **tylko** używa naszego biblioteki ADAL do uwierzytelniania, nie będziesz mieć wprowadzanie zmian.</span><span class="sxs-lookup"><span data-stu-id="becc3-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="becc3-114">Biblioteka ADAL ma osłonę aplikacji z zmiany.</span><span class="sxs-lookup"><span data-stu-id="becc3-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="becc3-115">Jakie są zmiany?</span><span class="sxs-lookup"><span data-stu-id="becc3-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="becc3-116">Usunięcie z nagłówków JWT wartości x5t</span><span class="sxs-lookup"><span data-stu-id="becc3-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="becc3-117">Punktu końcowego v2.0 korzysta z tokenów JWT często, która zawiera sekcja Parametry nagłówka o odpowiednie metadane dotyczące tokenu.</span><span class="sxs-lookup"><span data-stu-id="becc3-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="becc3-118">Jeśli dekodowanie nagłówka jednego z naszych bieżącego tokenów Jwt, może znaleźć wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="becc3-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="becc3-119">Gdzie "x5t" i "kid" właściwości identyfikacji klucza publicznego, który powinien być używany do weryfikacji podpisu tokenu, ponieważ pobrana z punktu końcowego metadanych OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="becc3-120">Zmiana, którą czynione tutaj jest Usuń właściwość "x5t".</span><span class="sxs-lookup"><span data-stu-id="becc3-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="becc3-121">Może nadal używać te same mechanizmy do sprawdzania poprawności tokenów, ale polegać wyłącznie na właściwość "kid" można pobrać prawidłowy klucz publiczny, jak określono w protokołu OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="becc3-122">**Zadania: Upewnij się, że aplikacja nie zależy od istnienia wartość x5t.**</span><span class="sxs-lookup"><span data-stu-id="becc3-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="becc3-123">Usuwanie profile_info</span><span class="sxs-lookup"><span data-stu-id="becc3-123">Removing profile_info</span></span>
<span data-ttu-id="becc3-124">Wcześniej punktu końcowego v2.0 ma zostały zwracając obiekt JSON kodowany w standardzie base64 w odpowiedzi tokenu o nazwie `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="becc3-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="becc3-125">Podczas żądania tokenu dostępu z punktem końcowym v2.0, wysyłając żądanie:</span><span class="sxs-lookup"><span data-stu-id="becc3-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="becc3-126">Odpowiedź będzie wyglądać w następujący obiekt JSON:</span><span class="sxs-lookup"><span data-stu-id="becc3-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="becc3-127">`profile_info` Wartość informacji o użytkowniku, która zarejestrowała się w aplikacji - ich nazwę wyświetlaną, imię, nazwisko, adres e-mail, identyfikator i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="becc3-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="becc3-128">Przede wszystkim `profile_info` była używana do buforowania tokenu i wyświetlić celów.</span><span class="sxs-lookup"><span data-stu-id="becc3-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="becc3-129">Teraz zostaną usunięte `profile_info` wartość — nie martw się, nadal zapewniamy te informacje dla deweloperów w miejscu nieco inne.</span><span class="sxs-lookup"><span data-stu-id="becc3-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="becc3-130">Zamiast `profile_info`, teraz zwróci punktu końcowego v2.0 `id_token` w każdej odpowiedzi tokenu:</span><span class="sxs-lookup"><span data-stu-id="becc3-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="becc3-131">Może zdekodować i przeanalizować żądaniu, aby pobrać informacje, które odebrano od profile_info.</span><span class="sxs-lookup"><span data-stu-id="becc3-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="becc3-132">W żądaniu jest JSON Web Token (JWT), o treści określonej przez OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="becc3-133">Kod może powinien być tak bardzo podobne — należy po prostu wyodrębnić środkowej segmentu (jednostka) żądaniu i base64 zdekodować dostępu do obiektu JSON w.</span><span class="sxs-lookup"><span data-stu-id="becc3-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="becc3-134">W ciągu przyszłych dwóch tygodni, powinien kodu aplikację, aby pobrać informacje o użytkowniku z albo `id_token` lub `profile_info`; zależności jest obecny.</span><span class="sxs-lookup"><span data-stu-id="becc3-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="becc3-135">Dzięki temu podczas wprowadzania zmian aplikacji bezproblemowo może obsłużyć przejście od `profile_info` do `id_token` bez przeszkód.</span><span class="sxs-lookup"><span data-stu-id="becc3-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becc3-136">**Zadania: Upewnij się, że aplikacja nie zależy od istnienia `profile_info` wartość.**</span><span class="sxs-lookup"><span data-stu-id="becc3-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="becc3-137">Usuwanie id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="becc3-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="becc3-138">Podobnie jak `profile_info`, zostaną również usunięte `id_token_expires_in` parametr z odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="becc3-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="becc3-139">Wcześniej punktu końcowego v2.0 zwróci wartość `id_token_expires_in` wraz z każdym odpowiedzi żądaniu, na przykład w odpowiedzi autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="becc3-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="becc3-140">Lub w odpowiedzi tokenu:</span><span class="sxs-lookup"><span data-stu-id="becc3-140">Or in a token response:</span></span>

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

<span data-ttu-id="becc3-141">`id_token_expires_in` Wartość wskazuje liczbę sekund żądaniu pozostanie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="becc3-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="becc3-142">Teraz, zostaną usunięte `id_token_expires_in` wartości całkowite.</span><span class="sxs-lookup"><span data-stu-id="becc3-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="becc3-143">Zamiast tego można użyć standardowego protokołu OpenID Connect `nbf` i `exp` oświadczeń do sprawdzenia poprawności żądaniu.</span><span class="sxs-lookup"><span data-stu-id="becc3-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="becc3-144">Zobacz [odwołania do tokenu v2.0](active-directory-v2-tokens.md) Aby uzyskać więcej informacji na temat tych oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="becc3-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becc3-145">**Zadania: Upewnij się, że aplikacja nie zależy od istnienia `id_token_expires_in` wartość.**</span><span class="sxs-lookup"><span data-stu-id="becc3-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="becc3-146">Zmiana oświadczeń zwrócony przez zakres = openid</span><span class="sxs-lookup"><span data-stu-id="becc3-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="becc3-147">Ta zmiana będzie najbardziej znaczących — w rzeczywistości, będzie miało wpływ na prawie każdej aplikacji, który używa punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="becc3-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="becc3-148">Wiele aplikacji wysyłać żądania przy użyciu punktu końcowego v2.0 `openid` zakresu, takie jak:</span><span class="sxs-lookup"><span data-stu-id="becc3-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="becc3-149">Obecnie, gdy użytkownik udziela zgody na `openid` zakresu, aplikacja odbiera szereg informacji o użytkowniku w żądaniu wynikowy.</span><span class="sxs-lookup"><span data-stu-id="becc3-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="becc3-150">Oświadczenia te mogą obejmować nazwy, preferowane nazwy użytkownika, adres e-mail i identyfikator obiektu.</span><span class="sxs-lookup"><span data-stu-id="becc3-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="becc3-151">W ramach tej aktualizacji, zmieniamy informacje który `openid` zakresu daje aplikacji dostęp do, aby lepiej comform ze specyfikacją OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="becc3-152">`openid` Zakres będzie tylko umożliwić zalogować użytkownika w aplikacji, a wyświetlony identyfikator specyficzny dla aplikacji dla użytkownika w `sub` oświadczeń o żądaniu.</span><span class="sxs-lookup"><span data-stu-id="becc3-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="becc3-153">Oświadczenia w żądaniu tylko z `openid` zakres przyznane będzie pozbawione żadnych informacji umożliwiających identyfikację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="becc3-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="becc3-154">Przykład żądaniu oświadczenia są:</span><span class="sxs-lookup"><span data-stu-id="becc3-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="becc3-155">Jeśli chcesz uzyskać dane osobowe lub informacje o użytkowniku w aplikacji, aplikacji należy zażądać dodatkowych uprawnień od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="becc3-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="becc3-156">Wprowadzono obsługę dwa nowe zakresy z OpenID Connect specyfikacji — `email` i `profile` zakresy — które umożliwiają zrobić.</span><span class="sxs-lookup"><span data-stu-id="becc3-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="becc3-157">`email` Zakres jest bardzo prosta — umożliwia dostęp aplikacji do użytkownika podstawowego adresu e-mail za pośrednictwem `email` oświadczeń w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="becc3-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="becc3-158">Należy pamiętać, że `email` oświadczenia nie zawsze będą obecne w id_tokens — tylko zostanie on uwzględniony jeśli są dostępne w profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="becc3-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="becc3-159">`profile` Zakresu daje aplikacji dostęp do wszystkich innych podstawowe informacje o użytkowniku — ich nazwy, preferowane username identyfikator obiektu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="becc3-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="becc3-160">Dzięki temu można kod aplikacji w sposób minimalnego ujawnienie — użytkownik może uzyskać tylko w zestawie danych, czy aplikacja wymaga, aby rozpocząć tworzenie.</span><span class="sxs-lookup"><span data-stu-id="becc3-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="becc3-161">Jeśli chcesz kontynuować pobieranie pełny zestaw informacje o użytkowniku, który obecnie otrzymuje aplikacji, należy uwzględnić wszystkie trzy zakresy w swoje żądania autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="becc3-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="becc3-162">Aplikację można rozpocząć wysyłanie `email` i `profile` natychmiast zakresy i punktu końcowego v2.0 będzie zaakceptować te dwa zakresy i rozpocząć żądanie uprawnień użytkowników w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="becc3-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="becc3-163">Jednak zmiana interpretacji `openid` zakres nie zostanie zastosowana dla kilka tygodni.</span><span class="sxs-lookup"><span data-stu-id="becc3-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becc3-164">**Zadania: Dodaj `profile` i `email` zakresów, jeśli aplikacja wymaga informacji o użytkowniku.**</span><span class="sxs-lookup"><span data-stu-id="becc3-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="becc3-165">Należy pamiętać, że ADAL będzie zawierać oba te uprawnienia żądań domyślnie.</span><span class="sxs-lookup"><span data-stu-id="becc3-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="becc3-166">Usuwanie wystawcy ukośnikiem na końcu.</span><span class="sxs-lookup"><span data-stu-id="becc3-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="becc3-167">Wcześniej wartość wystawcy, która jest wyświetlana w tokenach z punktem końcowym v2.0 trwało formularza</span><span class="sxs-lookup"><span data-stu-id="becc3-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="becc3-168">W przypadku, gdy identyfikatora dzierżawy usługi Azure AD został identyfikator guid dzierżawy, która wystawiła token.</span><span class="sxs-lookup"><span data-stu-id="becc3-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="becc3-169">Wprowadzone zmiany staje się wartości wystawcy</span><span class="sxs-lookup"><span data-stu-id="becc3-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="becc3-170">w obu tokeny i w dokumencie odnajdywania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becc3-171">**Zadania: Upewnij się, że aplikacja akceptuje wartości wystawcy, zarówno z i bez ukośnika podczas sprawdzania poprawności wystawcy.**</span><span class="sxs-lookup"><span data-stu-id="becc3-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="becc3-172">Dlaczego mam zmienić?</span><span class="sxs-lookup"><span data-stu-id="becc3-172">Why change?</span></span>
<span data-ttu-id="becc3-173">Główną motywacją do wprowadzenia tych zmian jest zgodny ze specyfikacją standardowe OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becc3-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="becc3-174">Będąc OpenID Connect zgodne mamy nadzieję zminimalizować różnice między integracji z usługami tożsamość firmy Microsoft oraz z innymi usługami tożsamościami w branży.</span><span class="sxs-lookup"><span data-stu-id="becc3-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="becc3-175">Chcemy umożliwiają deweloperom używanie bibliotek uwierzytelniania ich ulubionych typu open source bez konieczności zmiany w bibliotekach w celu uwzględnienia różnic między Microsoft.</span><span class="sxs-lookup"><span data-stu-id="becc3-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="becc3-176">Co należy zrobić?</span><span class="sxs-lookup"><span data-stu-id="becc3-176">What can you do?</span></span>
<span data-ttu-id="becc3-177">Obecnie można rozpocząć wprowadzania wszystkie zmiany opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="becc3-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="becc3-178">Należy natychmiast:</span><span class="sxs-lookup"><span data-stu-id="becc3-178">You should immediately:</span></span>

1. <span data-ttu-id="becc3-179">**Usuń wszelkie zależności na `x5t` parametr nagłówka.**</span><span class="sxs-lookup"><span data-stu-id="becc3-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="becc3-180">**Obsługiwać przejście od `profile_info` do `id_token` w odpowiedzi tokenu.**</span><span class="sxs-lookup"><span data-stu-id="becc3-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="becc3-181">**Usuń wszelkie zależności na `id_token_expires_in` parametr odpowiedzi.**</span><span class="sxs-lookup"><span data-stu-id="becc3-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="becc3-182">**Dodaj `profile` i `email` zakresów do aplikacji, jeśli aplikacja potrzebuje informacji użytkownika podstawowego.**</span><span class="sxs-lookup"><span data-stu-id="becc3-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="becc3-183">**Zaakceptuj wartości wystawcy tokenów zarówno z i bez ukośnika.**</span><span class="sxs-lookup"><span data-stu-id="becc3-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="becc3-184">Nasze [dokumentacji protokołu v2.0](active-directory-v2-protocols.md) już została zaktualizowana w celu odzwierciedlenia tych zmian, mogą używać go jako odwołanie pomagające, zaktualizuj kod.</span><span class="sxs-lookup"><span data-stu-id="becc3-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="becc3-185">Jeśli masz dodatkowe pytania na zakres zmian, proszę Możesz dotrzeć do nas w serwisie Twitter na @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="becc3-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="becc3-186">Jak często będą protokołu zmian?</span><span class="sxs-lookup"><span data-stu-id="becc3-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="becc3-187">Firma Microsoft nie przewiduje się, że dodatkowe fundamentalne zmiany protokoły uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="becc3-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="becc3-188">Te zmiany w jednej wersji celowo są zostać grupowania, dzięki czemu nie trzeba przechodzić przez ten typ procesu aktualizacji ponownie kiedykolwiek wkrótce.</span><span class="sxs-lookup"><span data-stu-id="becc3-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="becc3-189">Oczywiście Będziemy nadal dodawania do usługi uwierzytelniania konwergentnej v2.0, co użytkownik może skorzystać z funkcji, ale te zmiany należy dodatku i nie podziału istniejący kod.</span><span class="sxs-lookup"><span data-stu-id="becc3-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="becc3-190">Wreszcie chcemy powiedzieć Dziękujemy za wypróbowanie kwestii okresie używania wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="becc3-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="becc3-191">Szczegółowe informacje i doświadczenia naszych pilotażowe zostały nieoceniony w dotychczasowych i mamy nadzieję, że nastąpi przejście do udostępniania opinie i pomysłów.</span><span class="sxs-lookup"><span data-stu-id="becc3-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="becc3-192">Kodowanie przyjemność!</span><span class="sxs-lookup"><span data-stu-id="becc3-192">Happy coding!</span></span>

<span data-ttu-id="becc3-193">Dzielenie tożsamość firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="becc3-193">The Microsoft Identity Division</span></span>

