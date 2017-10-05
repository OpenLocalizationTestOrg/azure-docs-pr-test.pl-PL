---
title: "Sieci Web ASP.NET w wersji 2 usługi Azure AD serwera pobieranie rozpoczęte — testowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="0f728-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="0f728-103">Test your code</span></span>

<span data-ttu-id="0f728-104">Naciśnij klawisz `F5` do uruchomienia projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f728-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="0f728-105">W przeglądarce zostanie otworzyć i przekierować użytkownika do *http://localhost: {port}* gdy zobaczysz *Zaloguj się przy użyciu programu Microsoft* przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f728-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="0f728-106">Przejdź dalej i kliknij go, aby zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="0f728-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="0f728-107">Gdy wszystko jest gotowe do testowania, użyj pracy lub szkoły (Azure Active Directory) lub konto osobiste (live.com, outlook.com) do logowania.</span><span class="sxs-lookup"><span data-stu-id="0f728-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="0f728-110">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="0f728-110">Expected results</span></span>
<span data-ttu-id="0f728-111">Po zalogowaniu zostanie przekierowany użytkownik do strony głównej witryny sieci web, czyli adres URL HTTPS określony w aplikacji informacje rejestracyjne w portalu rejestracji aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f728-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="0f728-112">Ta strona zawiera obecnie *Hello {użytkownika}* i łącze do wylogowania i łącze, aby wyświetlić oświadczeń użytkownika — czyli łącze do kontrolera autoryzacji utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0f728-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="0f728-113">Zobacz oświadczenia użytkownika</span><span class="sxs-lookup"><span data-stu-id="0f728-113">See user's claims</span></span>
<span data-ttu-id="0f728-114">Wybierz, aby zobaczyć oświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f728-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="0f728-115">To prowadzi do kontrolera i widoku, który jest dostępny tylko dla użytkowników, którzy zostali uwierzytelnieni.</span><span class="sxs-lookup"><span data-stu-id="0f728-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="0f728-116">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="0f728-116">Expected results</span></span>
 <span data-ttu-id="0f728-117">Powinny pojawić się tabeli zawierającej podstawowe właściwości zalogowanego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="0f728-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="0f728-118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0f728-118">Property</span></span> | <span data-ttu-id="0f728-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="0f728-119">Value</span></span> | <span data-ttu-id="0f728-120">Opis</span><span class="sxs-lookup"><span data-stu-id="0f728-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="0f728-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0f728-121">Name</span></span> | <span data-ttu-id="0f728-122">{Pełna nazwa użytkownika}</span><span class="sxs-lookup"><span data-stu-id="0f728-122">{User Full Name}</span></span> | <span data-ttu-id="0f728-123">Użytkownik miał na imię i nazwisko</span><span class="sxs-lookup"><span data-stu-id="0f728-123">The user’s first and last name</span></span>
|<span data-ttu-id="0f728-124">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="0f728-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="0f728-125">Nazwa użytkownika używana do identyfikacji zalogowanego użytkownika</span><span class="sxs-lookup"><span data-stu-id="0f728-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="0f728-126">Temat</span><span class="sxs-lookup"><span data-stu-id="0f728-126">Subject</span></span>| <span data-ttu-id="0f728-127">{Podmiotu}</span><span class="sxs-lookup"><span data-stu-id="0f728-127">{Subject}</span></span>|<span data-ttu-id="0f728-128">Ciąg do unikatowego identyfikowania logowania użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="0f728-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="0f728-129">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="0f728-129">Tenant ID</span></span>| <span data-ttu-id="0f728-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="0f728-130">{Guid}</span></span>| <span data-ttu-id="0f728-131">A *guid* jednoznacznie reprezentujący użytkownika usługi Azure Active Directory organizacji.</span><span class="sxs-lookup"><span data-stu-id="0f728-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="0f728-132">Ponadto zobaczysz tabeli, w tym wszystkie oświadczenia użytkownika dołączana do uwierzytelniania żądań.</span><span class="sxs-lookup"><span data-stu-id="0f728-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="0f728-133">Aby uzyskać listę wszystkich oświadczeń w identyfikator tokenu wyjaśnienie i zapoznaj [artykułu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lista oświadczeń w identyfikatorze tokenu").</span><span class="sxs-lookup"><span data-stu-id="0f728-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="0f728-134">Test podczas uzyskiwania dostępu do metody, która ma *[Authorize]* atrybutu (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0f728-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="0f728-135">W tym kroku zostanie przetestować uzyskiwanie dostępu do kontrolera uwierzytelniony jako użytkownik anonimowy:</span><span class="sxs-lookup"><span data-stu-id="0f728-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="0f728-136">Wybierz łącze do wylogowania użytkownika i ukończyć proces wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="0f728-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="0f728-137">Teraz w przeglądarce, wpisz http://localhost: {port} / uwierzytelnionego dostępu kontrolerze, który jest chroniony za pomocą do `[Authorize]` atrybutu</span><span class="sxs-lookup"><span data-stu-id="0f728-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="0f728-138">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="0f728-138">Expected results</span></span>
<span data-ttu-id="0f728-139">Powinien zostać wyświetlony monit wymaga uwierzytelniania, aby wyświetlić widok.</span><span class="sxs-lookup"><span data-stu-id="0f728-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0f728-140">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="0f728-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="0f728-141">Ochrona całej witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="0f728-141">Protect your entire web site</span></span>
<span data-ttu-id="0f728-142">Aby chronić całej witryny sieci web, Dodaj `AuthorizeAttribute` do `GlobalFilters` w `Global.asax` `Application_Start` metody:</span><span class="sxs-lookup"><span data-stu-id="0f728-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="0f728-143">**Jak uniemożliwić użytkownikom tylko jednej z organizacji logować się do aplikacji**</span><span class="sxs-lookup"><span data-stu-id="0f728-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="0f728-144">Domyślnie osobiste konta (w tym outlook.com, live.com i inne) oraz pracy i kont służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory mogą zalogować się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0f728-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="0f728-145">Aplikacja do akceptowania logowania z usługi Azure Active Directory tylko jednej z organizacji, Zamień `Tenant` parametru w *web.config* z `Common` nazwę dzierżawy organizacji — przykład *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="0f728-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="0f728-146">Po wykonaniu tej zmiany `ValidateIssuer` argumentu w Twojej *klasy początkowej OWIN* do `true`.</span><span class="sxs-lookup"><span data-stu-id="0f728-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="0f728-147">Aby zezwolić użytkownikom tylko listę określonym organizacjom, `ValidateIssuer` na true i użyj `ValidIssuers` parametr, aby określić listę organizacji.</span><span class="sxs-lookup"><span data-stu-id="0f728-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="0f728-148">Innym rozwiązaniem jest implementować niestandardowe metodę do sprawdzania poprawności wystawcy za pomocą parametru IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="0f728-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="0f728-149">Aby uzyskać więcej informacji na temat `TokenValidationParameters`, można znaleźć pod adresem [to](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "artykuł w witrynie MSDN TokenValidationParameters") artykuł w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="0f728-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

