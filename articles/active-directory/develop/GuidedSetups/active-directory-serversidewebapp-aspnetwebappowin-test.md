---
title: aaaAzure AD v2 ASP.NET Web Server wprowadzenie - Test | Dokumentacja firmy Microsoft
description: "Implementowanie logowania firmy Microsoft dla rozwiązania ASP.NET z aplikacji opartych na przeglądarce sieci web tradycyjnych przy użyciu standardowego protokołu OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="9d67e-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="9d67e-103">Test your code</span></span>

<span data-ttu-id="9d67e-104">Naciśnij klawisz `F5` toorun projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d67e-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="9d67e-105">Witaj przeglądarki będą otwierane i przekierować użytkownika za*http://localhost: {port}* gdzie zobaczysz hello *Zaloguj się przy użyciu programu Microsoft* przycisku.</span><span class="sxs-lookup"><span data-stu-id="9d67e-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="9d67e-106">Przejdź dalej i kliknij ją toosign w.</span><span class="sxs-lookup"><span data-stu-id="9d67e-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="9d67e-107">Gdy wszystko będzie gotowe tootest, użyj służbowego (Azure Active Directory) służbowe lub osobiste (live.com, outlook.com) konta toosign w.</span><span class="sxs-lookup"><span data-stu-id="9d67e-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="9d67e-110">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="9d67e-110">Expected results</span></span>
<span data-ttu-id="9d67e-111">Po zalogowaniu użytkownik hello jest przekierowane toohello strony głównej witryny sieci web, czyli hello URL HTTPS określony w aplikacji informacje rejestracyjne w hello portalu rejestracji aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d67e-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="9d67e-112">Ta strona zawiera obecnie *Hello {użytkownika}* i wychodzący toosign łącza, a łącze toosee hello oświadczenia użytkownika — które kontroler autoryzacji toohello łącze jest utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9d67e-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="9d67e-113">Zobacz oświadczenia użytkownika</span><span class="sxs-lookup"><span data-stu-id="9d67e-113">See user's claims</span></span>
<span data-ttu-id="9d67e-114">Wybierz hello hyperlink toosee hello oświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d67e-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="9d67e-115">To poprowadzą toohello kontrolera i widoku, który jest tylko dostępne toousers, które są uwierzytelniane.</span><span class="sxs-lookup"><span data-stu-id="9d67e-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="9d67e-116">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="9d67e-116">Expected results</span></span>
 <span data-ttu-id="9d67e-117">Powinny pojawić się tabelę zawierającą hello podstawowe właściwości użytkowników hello rejestrowane:</span><span class="sxs-lookup"><span data-stu-id="9d67e-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="9d67e-118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9d67e-118">Property</span></span> | <span data-ttu-id="9d67e-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="9d67e-119">Value</span></span> | <span data-ttu-id="9d67e-120">Opis</span><span class="sxs-lookup"><span data-stu-id="9d67e-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="9d67e-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9d67e-121">Name</span></span> | <span data-ttu-id="9d67e-122">{Pełna nazwa użytkownika}</span><span class="sxs-lookup"><span data-stu-id="9d67e-122">{User Full Name}</span></span> | <span data-ttu-id="9d67e-123">Użytkownik Hello na imię i nazwisko</span><span class="sxs-lookup"><span data-stu-id="9d67e-123">hello user’s first and last name</span></span>
|<span data-ttu-id="9d67e-124">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="9d67e-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="9d67e-125">używana nazwa Hello tooidentify hello zalogowany użytkownik</span><span class="sxs-lookup"><span data-stu-id="9d67e-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="9d67e-126">Temat</span><span class="sxs-lookup"><span data-stu-id="9d67e-126">Subject</span></span>| <span data-ttu-id="9d67e-127">{Podmiotu}</span><span class="sxs-lookup"><span data-stu-id="9d67e-127">{Subject}</span></span>|<span data-ttu-id="9d67e-128">Toouniquely ciąg identyfikacji hello logowania użytkownika w różnych hello sieci web</span><span class="sxs-lookup"><span data-stu-id="9d67e-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="9d67e-129">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="9d67e-129">Tenant ID</span></span>| <span data-ttu-id="9d67e-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="9d67e-130">{Guid}</span></span>| <span data-ttu-id="9d67e-131">A *guid* toouniquely reprezentowania hello użytkownika usługi Azure Active Directory organizacji.</span><span class="sxs-lookup"><span data-stu-id="9d67e-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="9d67e-132">Ponadto zobaczysz tabeli, w tym wszystkie oświadczenia użytkownika dołączana do uwierzytelniania żądań.</span><span class="sxs-lookup"><span data-stu-id="9d67e-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="9d67e-133">Aby uzyskać listę wszystkich oświadczeń w identyfikator tokenu wyjaśnienie i zapoznaj [artykułu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lista oświadczeń w identyfikatorze tokenu").</span><span class="sxs-lookup"><span data-stu-id="9d67e-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="9d67e-134">Test podczas uzyskiwania dostępu do metody, która ma *[Authorize]* atrybutu (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="9d67e-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="9d67e-135">W tym kroku zostanie testu podczas uzyskiwania dostępu do kontrolera uwierzytelniany hello jako użytkownik anonimowy:</span><span class="sxs-lookup"><span data-stu-id="9d67e-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="9d67e-136">Wybierz hello Połącz hello poza toosign użytkownika i hello pełną proces wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="9d67e-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="9d67e-137">Teraz w przeglądarce, wpisz http://localhost: {port} / uwierzytelniony tooaccess kontrolerze, który jest chroniony za pomocą hello `[Authorize]` atrybutu</span><span class="sxs-lookup"><span data-stu-id="9d67e-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="9d67e-138">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="9d67e-138">Expected results</span></span>
<span data-ttu-id="9d67e-139">Powinien zostać wyświetlony monit hello żądający tooauthenticate toosee hello widoku.</span><span class="sxs-lookup"><span data-stu-id="9d67e-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9d67e-140">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="9d67e-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="9d67e-141">Ochrona całej witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="9d67e-141">Protect your entire web site</span></span>
<span data-ttu-id="9d67e-142">tooprotect całej witryny sieci web, Dodaj hello `AuthorizeAttribute` za`GlobalFilters` w `Global.asax` `Application_Start` metody:</span><span class="sxs-lookup"><span data-stu-id="9d67e-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="9d67e-143">**Jak użytkownicy toorestrict z toosign tylko jednej z organizacji w aplikacji tooyour**</span><span class="sxs-lookup"><span data-stu-id="9d67e-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="9d67e-144">Domyślnie konta osobiste (takie jak outlook.com, live.com i inne), a także kont służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory można logowania tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d67e-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="9d67e-145">Twojej aplikacji tooaccept logowania z usługi Azure Active Directory tylko jednej z organizacji, Zamień hello `Tenant` parametru w *web.config* z `Common` toohello nazwa dzierżawy organizacji hello — przykład *contoso.onmicrosoft.com*. Po wykonaniu tej zmiany hello `ValidateIssuer` argumentu w Twojej *klasy początkowej OWIN* zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="9d67e-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="9d67e-146">Ustaw tooallow użytkownikom tylko listę określonym organizacjom `ValidateIssuer` hello tootrue i użyj `ValidIssuers` toospecify parametru wykaz organizacji.</span><span class="sxs-lookup"><span data-stu-id="9d67e-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="9d67e-147">Inną opcją jest wystawców hello toovalidate za pomocą parametru IssuerValidator tooimplement metody niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9d67e-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="9d67e-148">Aby uzyskać więcej informacji na temat `TokenValidationParameters`, można znaleźć pod adresem [to](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "artykuł w witrynie MSDN TokenValidationParameters") artykuł w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="9d67e-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

