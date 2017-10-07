---
title: "aaaSession zarządzania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="4b076-103">Ramka zabezpieczeń: Zarządzanie sesjami | Artykuły</span><span class="sxs-lookup"><span data-stu-id="4b076-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="4b076-104">Produktów i usług</span><span class="sxs-lookup"><span data-stu-id="4b076-104">Product/Service</span></span> | <span data-ttu-id="4b076-105">Artykuł</span><span class="sxs-lookup"><span data-stu-id="4b076-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="4b076-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="4b076-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="4b076-107">Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b076-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="4b076-108">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="4b076-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="4b076-109">Użyj ograniczone okresy istnienia generowanych tokenach SaS</span><span class="sxs-lookup"><span data-stu-id="4b076-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="4b076-110">**Dokumentów w usłudze Azure DB**</span><span class="sxs-lookup"><span data-stu-id="4b076-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="4b076-111">Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów</span><span class="sxs-lookup"><span data-stu-id="4b076-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="4b076-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="4b076-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="4b076-113">Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS</span><span class="sxs-lookup"><span data-stu-id="4b076-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="4b076-114">**Tożsamości serwera**</span><span class="sxs-lookup"><span data-stu-id="4b076-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="4b076-115">Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="4b076-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="4b076-116">**Aplikacja sieci Web**</span><span class="sxs-lookup"><span data-stu-id="4b076-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="4b076-117">Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie</span><span class="sxs-lookup"><span data-stu-id="4b076-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="4b076-118">Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie</span><span class="sxs-lookup"><span data-stu-id="4b076-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="4b076-119">Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4b076-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="4b076-120">Konfigurowanie sesji dla okresu istnienia aktywności</span><span class="sxs-lookup"><span data-stu-id="4b076-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="4b076-121">Implementuje prawidłowego wylogowania z aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="4b076-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="4b076-122">**Interfejs API sieci Web**</span><span class="sxs-lookup"><span data-stu-id="4b076-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="4b076-123">Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4b076-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="4b076-124"><a id="logout-adal"></a>Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b076-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="4b076-125">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-125">Title</span></span>                   | <span data-ttu-id="4b076-126">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-127">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-127">**Component**</span></span>               | <span data-ttu-id="4b076-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b076-128">Azure AD</span></span> | 
| <span data-ttu-id="4b076-129">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-129">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-130">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-130">Build</span></span> |  
| <span data-ttu-id="4b076-131">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-131">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-132">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-132">Generic</span></span> |
| <span data-ttu-id="4b076-133">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-133">**Attributes**</span></span>              | <span data-ttu-id="4b076-134">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-134">N/A</span></span>  |
| <span data-ttu-id="4b076-135">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-135">**References**</span></span>              | <span data-ttu-id="4b076-136">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-136">N/A</span></span>  |
| <span data-ttu-id="4b076-137">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-137">**Steps**</span></span> | <span data-ttu-id="4b076-138">Jeśli aplikacja hello opiera się na token dostępu wystawiony przez usługę Azure AD, program obsługi zdarzeń wylogowania hello powinny wywoływać</span><span class="sxs-lookup"><span data-stu-id="4b076-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="4b076-139">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="4b076-140">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-140">Example</span></span>
<span data-ttu-id="4b076-141">Należy także zniszczyć sesji użytkownika, wywołując metodę Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="4b076-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="4b076-142">Następujące metody przedstawia bezpiecznej implementacji wylogowania użytkownika:</span><span class="sxs-lookup"><span data-stu-id="4b076-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="4b076-143"><a id="finite-tokens"></a>Użyj ograniczone okresy istnienia generowanych tokenach SaS</span><span class="sxs-lookup"><span data-stu-id="4b076-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="4b076-144">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-144">Title</span></span>                   | <span data-ttu-id="4b076-145">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-146">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-146">**Component**</span></span>               | <span data-ttu-id="4b076-147">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="4b076-147">IoT Device</span></span> | 
| <span data-ttu-id="4b076-148">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-148">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-149">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-149">Build</span></span> |  
| <span data-ttu-id="4b076-150">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-150">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-151">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-151">Generic</span></span> |
| <span data-ttu-id="4b076-152">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-152">**Attributes**</span></span>              | <span data-ttu-id="4b076-153">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-153">N/A</span></span>  |
| <span data-ttu-id="4b076-154">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-154">**References**</span></span>              | <span data-ttu-id="4b076-155">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-155">N/A</span></span>  |
| <span data-ttu-id="4b076-156">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-156">**Steps**</span></span> | <span data-ttu-id="4b076-157">Tokeny sygnatury dostępu współdzielonego generowane w celu uwierzytelniania tooAzure Centrum IoT powinny mieć okresu wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="4b076-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="4b076-158">Zachowaj hello SaS okresy istnienia tokenu tooa toolimit minimalna hello ilość czasu, który może być odtwarzany w przypadku naruszenia zabezpieczeń tokeny hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="4b076-159"><a id="resource-tokens"></a>Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów</span><span class="sxs-lookup"><span data-stu-id="4b076-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="4b076-160">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-160">Title</span></span>                   | <span data-ttu-id="4b076-161">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-162">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-162">**Component**</span></span>               | <span data-ttu-id="4b076-163">Dokumentów w usłudze Azure DB</span><span class="sxs-lookup"><span data-stu-id="4b076-163">Azure Document DB</span></span> | 
| <span data-ttu-id="4b076-164">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-164">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-165">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-165">Build</span></span> |  
| <span data-ttu-id="4b076-166">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-166">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-167">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-167">Generic</span></span> |
| <span data-ttu-id="4b076-168">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-168">**Attributes**</span></span>              | <span data-ttu-id="4b076-169">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-169">N/A</span></span>  |
| <span data-ttu-id="4b076-170">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-170">**References**</span></span>              | <span data-ttu-id="4b076-171">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-171">N/A</span></span>  |
| <span data-ttu-id="4b076-172">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-172">**Steps**</span></span> | <span data-ttu-id="4b076-173">Zmniejsz timespan hello z zasobów tokenu tooa minimalną wartość wymaganą.</span><span class="sxs-lookup"><span data-stu-id="4b076-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="4b076-174">Tokeny zasobów ma prawidłowy obiekt timespan domyślnej 1 godz.</span><span class="sxs-lookup"><span data-stu-id="4b076-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="4b076-175"><a id="wsfederation-logout"></a>Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS</span><span class="sxs-lookup"><span data-stu-id="4b076-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="4b076-176">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-176">Title</span></span>                   | <span data-ttu-id="4b076-177">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-178">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-178">**Component**</span></span>               | <span data-ttu-id="4b076-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="4b076-179">ADFS</span></span> | 
| <span data-ttu-id="4b076-180">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-180">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-181">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-181">Build</span></span> |  
| <span data-ttu-id="4b076-182">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-182">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-183">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-183">Generic</span></span> |
| <span data-ttu-id="4b076-184">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-184">**Attributes**</span></span>              | <span data-ttu-id="4b076-185">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-185">N/A</span></span>  |
| <span data-ttu-id="4b076-186">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-186">**References**</span></span>              | <span data-ttu-id="4b076-187">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-187">N/A</span></span>  |
| <span data-ttu-id="4b076-188">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-188">**Steps**</span></span> | <span data-ttu-id="4b076-189">Jeśli aplikacja hello używa tokenu Zabezpieczającego wydane przez usługi AD FS, program obsługi zdarzeń wylogowania hello powinny wywoływać toolog metody WSFederationAuthenticationModule.FederatedSignOut() limit hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b076-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="4b076-190">Również hello bieżącej sesji należy zniszczyć, a wartość tokenu sesji hello należy zresetować i zniweczone.</span><span class="sxs-lookup"><span data-stu-id="4b076-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-191">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="4b076-192"><a id="proper-logout"></a>Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="4b076-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="4b076-193">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-193">Title</span></span>                   | <span data-ttu-id="4b076-194">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-195">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-195">**Component**</span></span>               | <span data-ttu-id="4b076-196">Tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="4b076-196">Identity Server</span></span> | 
| <span data-ttu-id="4b076-197">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-197">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-198">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-198">Build</span></span> |  
| <span data-ttu-id="4b076-199">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-199">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-200">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-200">Generic</span></span> |
| <span data-ttu-id="4b076-201">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-201">**Attributes**</span></span>              | <span data-ttu-id="4b076-202">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-202">N/A</span></span>  |
| <span data-ttu-id="4b076-203">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-203">**References**</span></span>              | [<span data-ttu-id="4b076-204">Federacyjna IdentityServer3 wylogowaniu</span><span class="sxs-lookup"><span data-stu-id="4b076-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="4b076-205">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-205">**Steps**</span></span> | <span data-ttu-id="4b076-206">IdentityServer obsługuje hello możliwości toofederate przy pomocy dostawcy tożsamości zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="4b076-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="4b076-207">Gdy użytkownik zaloguje się poza dostawcy tożsamości nadrzędnego, w zależności od protokołu hello, może być możliwe tooreceive powiadomienie po wylogowaniu się użytkownika hello. Umożliwia on toonotify IdentityServer, które jej klientów, można również zalogują się hello użytkownika. W dokumentacji hello w sekcji odwołań hello hello szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="4b076-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="4b076-208"><a id="https-secure-cookies"></a>Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie</span><span class="sxs-lookup"><span data-stu-id="4b076-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="4b076-209">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-209">Title</span></span>                   | <span data-ttu-id="4b076-210">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-211">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-211">**Component**</span></span>               | <span data-ttu-id="4b076-212">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-212">Web Application</span></span> | 
| <span data-ttu-id="4b076-213">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-213">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-214">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-214">Build</span></span> |  
| <span data-ttu-id="4b076-215">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-215">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-216">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-216">Generic</span></span> |
| <span data-ttu-id="4b076-217">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-217">**Attributes**</span></span>              | <span data-ttu-id="4b076-218">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="4b076-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="4b076-219">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-219">**References**</span></span>              | <span data-ttu-id="4b076-220">[httpCookies — Element (schemat ustawień programu ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure właściwości](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="4b076-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="4b076-221">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-221">**Steps**</span></span> | <span data-ttu-id="4b076-222">Pliki cookie są zwykle tylko dostępny toohello domeny, dla którego zostały zakres.</span><span class="sxs-lookup"><span data-stu-id="4b076-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="4b076-223">Niestety definicji hello "domeny" nie zawierają hello protokołu, dlatego plików cookie, które są tworzone przy użyciu protokołu HTTPS są dostępne za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b076-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="4b076-224">atrybut "secure" Hello wskazuje, że przeglądarka toohello hello plik cookie powinien tylko udostępniane za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4b076-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="4b076-225">Upewnij się, że wszystkie pliki cookie ustawić przy użyciu protokołu HTTPS używa hello **bezpiecznego** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="4b076-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="4b076-226">wymaganie Hello można wymusić w pliku web.config hello przez ustawienie tootrue atrybut parametru requireSSL hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="4b076-227">Jest hello preferowane podejście, ponieważ będzie wymuszać hello **bezpiecznego** atrybutu dla wszystkich plików cookie obecne i przyszłe bez hello toomake konieczność zmiany dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="4b076-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-228">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="4b076-229">Ustawienie Hello jest wymuszane, nawet jeśli tooaccess używanych aplikacji hello jest HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b076-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="4b076-230">Użycie protokołu HTTP tooaccess hello aplikacji, hello podziałów ustawienia, które aplikacji hello ponieważ hello pliki cookie są konfigurowane przy użyciu bezpiecznego atrybutu i hello przeglądarki hello nie będzie wysyłać je kopii toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b076-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="4b076-231">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-231">Title</span></span>                   | <span data-ttu-id="4b076-232">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-233">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-233">**Component**</span></span>               | <span data-ttu-id="4b076-234">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-234">Web Application</span></span> | 
| <span data-ttu-id="4b076-235">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-235">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-236">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-236">Build</span></span> |  
| <span data-ttu-id="4b076-237">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-237">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-238">Formularze sieci Web, MVC5</span><span class="sxs-lookup"><span data-stu-id="4b076-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="4b076-239">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-239">**Attributes**</span></span>              | <span data-ttu-id="4b076-240">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="4b076-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="4b076-241">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-241">**References**</span></span>              | <span data-ttu-id="4b076-242">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-242">N/A</span></span>  |
| <span data-ttu-id="4b076-243">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-243">**Steps**</span></span> | <span data-ttu-id="4b076-244">Gdy hello aplikacji sieci web jest hello zaufania jednostek uzależnionych oraz hello IdP serwera usług AD FS, atrybut bezpiecznego tokenu FedAuth hello można skonfigurować przez ustawienie parametru requireSSL tooTrue w `system.identityModel.services` sekcji w pliku Web.config:</span><span class="sxs-lookup"><span data-stu-id="4b076-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-245">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="4b076-246"><a id="cookie-definition"></a>Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie</span><span class="sxs-lookup"><span data-stu-id="4b076-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="4b076-247">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-247">Title</span></span>                   | <span data-ttu-id="4b076-248">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-249">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-249">**Component**</span></span>               | <span data-ttu-id="4b076-250">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-250">Web Application</span></span> | 
| <span data-ttu-id="4b076-251">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-251">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-252">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-252">Build</span></span> |  
| <span data-ttu-id="4b076-253">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-253">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-254">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-254">Generic</span></span> |
| <span data-ttu-id="4b076-255">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-255">**Attributes**</span></span>              | <span data-ttu-id="4b076-256">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-256">N/A</span></span>  |
| <span data-ttu-id="4b076-257">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-257">**References**</span></span>              | [<span data-ttu-id="4b076-258">Atrybut bezpiecznego pliku Cookie</span><span class="sxs-lookup"><span data-stu-id="4b076-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="4b076-259">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-259">**Steps**</span></span> | <span data-ttu-id="4b076-260">toomitigate hello ryzyko ujawnienia informacji z atak skryptów między witrynami (XSS), nowy atrybut — httpOnly — zostało wprowadzone toocookies i jest obsługiwany przez wszystkie główne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="4b076-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="4b076-261">Atrybut Hello Określa, że plik cookie nie jest dostępny za pośrednictwem skryptu.</span><span class="sxs-lookup"><span data-stu-id="4b076-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="4b076-262">Za pomocą plików cookie HttpOnly, aplikacji sieci web zmniejsza możliwości hello poufne informacje zawarte w pliku cookie hello może być kradzieży za pomocą skryptu i wysyłane do osoby atakującej tooan witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4b076-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="4b076-263">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-263">Example</span></span>
<span data-ttu-id="4b076-264">Wszystkie aplikacje oparte na protokole HTTP, które używają plików cookie należy określić HttpOnly w definicji pliku cookie hello, implementując następujących konfiguracji w pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="4b076-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="4b076-265">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-265">Title</span></span>                   | <span data-ttu-id="4b076-266">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-267">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-267">**Component**</span></span>               | <span data-ttu-id="4b076-268">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-268">Web Application</span></span> | 
| <span data-ttu-id="4b076-269">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-269">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-270">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-270">Build</span></span> |  
| <span data-ttu-id="4b076-271">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-271">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-272">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-272">Web Forms</span></span> |
| <span data-ttu-id="4b076-273">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-273">**Attributes**</span></span>              | <span data-ttu-id="4b076-274">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-274">N/A</span></span>  |
| <span data-ttu-id="4b076-275">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-275">**References**</span></span>              | [<span data-ttu-id="4b076-276">Właściwość FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="4b076-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="4b076-277">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-277">**Steps**</span></span> | <span data-ttu-id="4b076-278">wartość właściwości parametru RequireSSL Hello jest ustawiana w hello pliku konfiguracji dla aplikacji ASP.NET przy użyciu atrybutu parametru requireSSL hello hello elementu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4b076-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="4b076-279">Można określić w pliku Web.config hello aplikacji ASP.NET czy serwera toohello plików cookie uwierzytelniania formularzy hello tooreturn wymagane przez atrybut parametru requireSSL hello ustawienia protokołu SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="4b076-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-280">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-280">Example</span></span> 
<span data-ttu-id="4b076-281">Witaj Poniższy przykładowy kod ustawia atrybut parametru requireSSL hello w pliku Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="4b076-282">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-282">Title</span></span>                   | <span data-ttu-id="4b076-283">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-284">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-284">**Component**</span></span>               | <span data-ttu-id="4b076-285">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-285">Web Application</span></span> | 
| <span data-ttu-id="4b076-286">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-286">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-287">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-287">Build</span></span> |  
| <span data-ttu-id="4b076-288">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-288">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="4b076-289">MVC5</span></span> |
| <span data-ttu-id="4b076-290">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-290">**Attributes**</span></span>              | <span data-ttu-id="4b076-291">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="4b076-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="4b076-292">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-292">**References**</span></span>              | [<span data-ttu-id="4b076-293">Windows Identity Foundation (WIF) Konfiguracja — część II</span><span class="sxs-lookup"><span data-stu-id="4b076-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="4b076-294">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-294">**Steps**</span></span> | <span data-ttu-id="4b076-295">Atrybut httpOnly tooset plików cookie FedAuth, wartość atrybutu hideFromCsript musi być ustawiona tooTrue.</span><span class="sxs-lookup"><span data-stu-id="4b076-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="4b076-296">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-296">Example</span></span>
<span data-ttu-id="4b076-297">Poniższa konfiguracja przedstawia hello prawidłowej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="4b076-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="4b076-298"><a id="csrf-asp"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4b076-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="4b076-299">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-299">Title</span></span>                   | <span data-ttu-id="4b076-300">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-301">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-301">**Component**</span></span>               | <span data-ttu-id="4b076-302">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-302">Web Application</span></span> | 
| <span data-ttu-id="4b076-303">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-303">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-304">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-304">Build</span></span> |  
| <span data-ttu-id="4b076-305">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-305">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-306">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-306">Generic</span></span> |
| <span data-ttu-id="4b076-307">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-307">**Attributes**</span></span>              | <span data-ttu-id="4b076-308">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-308">N/A</span></span>  |
| <span data-ttu-id="4b076-309">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-309">**References**</span></span>              | <span data-ttu-id="4b076-310">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-310">N/A</span></span>  |
| <span data-ttu-id="4b076-311">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-311">**Steps**</span></span> | <span data-ttu-id="4b076-312">Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń hello ustanowienie sesji innego użytkownika w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b076-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="4b076-313">Celem Hello jest toomodify lub usuń zawartość, jeśli hello docelowej witryny sieci web opiera się wyłącznie na pliki cookie sesji tooauthenticate odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="4b076-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="4b076-314">Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając tooload przeglądarki innego użytkownika adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik hello jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="4b076-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="4b076-315">Istnieje wiele sposobów toodo osoby atakującej, takich jak obsługując inna witryna sieci web który ładuje zasobu z serwera narażone hello lub pobierania hello tooclick użytkownika łącza.</span><span class="sxs-lookup"><span data-stu-id="4b076-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="4b076-316">atak powitania można zapobiec, jeśli serwer hello wysyła klientowi dodatkowe toohello token, wymaga hello tooinclude klienta tokenu we wszystkich przyszłych żądań i sprawdza, czy wszystkie przyszłych żądań obejmują token, który dotyczy toohello bieżącej sesji, takie jak przez za pomocą hello ASP.NET AntiForgeryToken lub ViewState.</span><span class="sxs-lookup"><span data-stu-id="4b076-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="4b076-317">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-317">Title</span></span>                   | <span data-ttu-id="4b076-318">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-319">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-319">**Component**</span></span>               | <span data-ttu-id="4b076-320">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-320">Web Application</span></span> | 
| <span data-ttu-id="4b076-321">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-321">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-322">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-322">Build</span></span> |  
| <span data-ttu-id="4b076-323">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-323">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="4b076-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="4b076-325">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-325">**Attributes**</span></span>              | <span data-ttu-id="4b076-326">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-326">N/A</span></span>  |
| <span data-ttu-id="4b076-327">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-327">**References**</span></span>              | [<span data-ttu-id="4b076-328">Zapobieganie XSRF/CSRF w platformie ASP.NET MVC i stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="4b076-329">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-329">**Steps**</span></span> | <span data-ttu-id="4b076-330">Formularze Anti-CSRF i ASP.NET MVC — Użyj hello `AntiForgeryToken` metody pomocniczej w widokach; ujmij `Html.AntiForgeryToken()` do postaci hello, na przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-331">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="4b076-332">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="4b076-333">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-333">Example</span></span>
<span data-ttu-id="4b076-334">Na powitania sam czasu, odwiedzający hello zapewnia Html.AntiForgeryToken() pliku cookie o nazwie __RequestVerificationToken z hello samą wartość jako hello losowych wartości ukryte przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="4b076-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="4b076-335">Następnie toovalidate przychodzące post formularza, Dodaj metodę akcji docelową toohello filtru hello [ValidateAntiForgeryToken].</span><span class="sxs-lookup"><span data-stu-id="4b076-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="4b076-336">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b076-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="4b076-337">Filtr autoryzacji, która sprawdza, czy:</span><span class="sxs-lookup"><span data-stu-id="4b076-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="4b076-338">żądanie przychodzące Hello ma pliku cookie o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="4b076-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="4b076-339">Witaj żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="4b076-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="4b076-340">Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, Żądanie hello przechodzi przez normalnego.</span><span class="sxs-lookup"><span data-stu-id="4b076-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="4b076-341">Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy".</span><span class="sxs-lookup"><span data-stu-id="4b076-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="4b076-342">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-342">Example</span></span>
<span data-ttu-id="4b076-343">Anti-CSRF i AJAX: hello tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="4b076-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="4b076-344">Jedno rozwiązanie jest toosend hello tokenów w niestandardowy nagłówek HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b076-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="4b076-345">Witaj następujący kod używa tokenów hello toogenerate składni Razor, a następnie dodanie hello tokenów tooan AJAX żądania.</span><span class="sxs-lookup"><span data-stu-id="4b076-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="4b076-346">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-346">Example</span></span>
<span data-ttu-id="4b076-347">Podczas przetwarzania żądania hello wyodrębniania nagłówek żądania hello hello tokenów.</span><span class="sxs-lookup"><span data-stu-id="4b076-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="4b076-348">Następnie wywołaj metodę AntiForgery.Validate hello toovalidate hello tokenów.</span><span class="sxs-lookup"><span data-stu-id="4b076-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="4b076-349">Witaj metodę Validate zgłasza wyjątek, jeśli hello tokenów nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="4b076-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="4b076-350">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-350">Title</span></span>                   | <span data-ttu-id="4b076-351">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-352">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-352">**Component**</span></span>               | <span data-ttu-id="4b076-353">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-353">Web Application</span></span> | 
| <span data-ttu-id="4b076-354">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-354">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-355">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-355">Build</span></span> |  
| <span data-ttu-id="4b076-356">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-356">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-357">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-357">Web Forms</span></span> |
| <span data-ttu-id="4b076-358">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-358">**Attributes**</span></span>              | <span data-ttu-id="4b076-359">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-359">N/A</span></span>  |
| <span data-ttu-id="4b076-360">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-360">**References**</span></span>              | [<span data-ttu-id="4b076-361">Podejmij korzystać z ASP.NET wbudowane funkcje tooFend poza Web ataków</span><span class="sxs-lookup"><span data-stu-id="4b076-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="4b076-362">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-362">**Steps**</span></span> | <span data-ttu-id="4b076-363">Ataki CSRF w aplikacjach na podstawie formularza sieci Web można zminimalizować przez ustawienie ViewStateUserKey tooa losowy ciąg, który jest różny dla każdego użytkownika — identyfikator użytkownika lub, lepiej jeszcze sesji identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4b076-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="4b076-364">Istnieje wiele możliwych przyczyn technicznych i społecznościowych identyfikator sesji jest znacznie lepszym rozwiązaniem, ponieważ identyfikator jest nieoczekiwane, sesji upłynie limit czasu i zmienia się na poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4b076-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-365">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-365">Example</span></span>
<span data-ttu-id="4b076-366">Oto kod hello należy toohave we wszystkich stron:</span><span class="sxs-lookup"><span data-stu-id="4b076-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="4b076-367"><a id="inactivity-lifetime"></a>Konfigurowanie sesji dla okresu istnienia aktywności</span><span class="sxs-lookup"><span data-stu-id="4b076-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="4b076-368">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-368">Title</span></span>                   | <span data-ttu-id="4b076-369">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-370">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-370">**Component**</span></span>               | <span data-ttu-id="4b076-371">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-371">Web Application</span></span> | 
| <span data-ttu-id="4b076-372">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-372">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-373">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-373">Build</span></span> |  
| <span data-ttu-id="4b076-374">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-374">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-375">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-375">Generic</span></span> |
| <span data-ttu-id="4b076-376">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-376">**Attributes**</span></span>              | <span data-ttu-id="4b076-377">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-377">N/A</span></span>  |
| <span data-ttu-id="4b076-378">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-378">**References**</span></span>              | <span data-ttu-id="4b076-379">[Właściwość HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="4b076-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="4b076-380">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-380">**Steps**</span></span> | <span data-ttu-id="4b076-381">Limit czasu sesji reprezentuje hello zdarzenie występuje, gdy użytkownik nie wykonywania dowolnych akcji w witrynie sieci web dla interwału (zdefiniowane przez serwer sieci web).</span><span class="sxs-lookup"><span data-stu-id="4b076-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="4b076-382">Witaj zdarzeń po stronie serwera, zmiany stanu hello too'invalid sesji użytkownika hello "(na przykład" nie już używać") oraz poinstruuj toodestroy serwera sieci web hello go (usunięcie wszystkich danych znajdujących się w niej).</span><span class="sxs-lookup"><span data-stu-id="4b076-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="4b076-383">Witaj Poniższy przykładowy kod ustawia hello limitu czasu sesji atrybutu too15 minut w pliku Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-384">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-384">Example</span></span>
<span data-ttu-id="4b076-385">"" Kod XML <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="4b076-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="4b076-386">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-386">Title</span></span>                   | <span data-ttu-id="4b076-387">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-388">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-388">**Component**</span></span>               | <span data-ttu-id="4b076-389">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-389">Web Application</span></span> | 
| <span data-ttu-id="4b076-390">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-390">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-391">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-391">Build</span></span> |  
| <span data-ttu-id="4b076-392">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-392">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-393">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-393">Web Forms</span></span> |
| <span data-ttu-id="4b076-394">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-394">**Attributes**</span></span>              | <span data-ttu-id="4b076-395">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-395">N/A</span></span>  |
| <span data-ttu-id="4b076-396">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-396">**References**</span></span>              | <span data-ttu-id="4b076-397">[Tworzy Element uwierzytelniania (schemat ustawień programu ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="4b076-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="4b076-398">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-398">**Steps**</span></span> | <span data-ttu-id="4b076-399">Ustaw minut hello too15 limitu czasu plików cookie biletu uwierzytelniania formularzy</span><span class="sxs-lookup"><span data-stu-id="4b076-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="4b076-400">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-400">Example</span></span>
<span data-ttu-id="4b076-401">"" Kod XML<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="4b076-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="4b076-402">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-402">Example</span></span>
<span data-ttu-id="4b076-403">Również hello wystawiony okres istnienia tokenu SAML oświadczenia usług AD FS należy ustawić too15 min, wykonując następujące polecenia programu powershell na serwerze usług AD FS hello hello:</span><span class="sxs-lookup"><span data-stu-id="4b076-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="4b076-404"><a id="proper-app-logout"></a>Implementuje prawidłowego wylogowania z aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="4b076-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="4b076-405">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-405">Title</span></span>                   | <span data-ttu-id="4b076-406">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-407">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-407">**Component**</span></span>               | <span data-ttu-id="4b076-408">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-408">Web Application</span></span> | 
| <span data-ttu-id="4b076-409">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-409">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-410">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-410">Build</span></span> |  
| <span data-ttu-id="4b076-411">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-411">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-412">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-412">Generic</span></span> |
| <span data-ttu-id="4b076-413">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-413">**Attributes**</span></span>              | <span data-ttu-id="4b076-414">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-414">N/A</span></span>  |
| <span data-ttu-id="4b076-415">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-415">**References**</span></span>              | <span data-ttu-id="4b076-416">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-416">N/A</span></span>  |
| <span data-ttu-id="4b076-417">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-417">**Steps**</span></span> | <span data-ttu-id="4b076-418">Wykonaj odpowiednie Wyloguj z aplikacji hello, gdy użytkownik naciśnie Wyloguj się przycisk.</span><span class="sxs-lookup"><span data-stu-id="4b076-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="4b076-419">Podczas wylogowania aplikacji należy zniszczyć sesji użytkownika, resetowanie oraz zniesienia wartość pliku cookie sesji, oraz resetowanie i rozpoczynającą wartość pliku cookie uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="4b076-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="4b076-420">Ponadto jeśli wiele sesji są wiązanej tooa tożsamości pojedynczego użytkownika, ich musi być zbiorczo zakończona na powitania po stronie serwera na limitu czasu lub Wyloguj.</span><span class="sxs-lookup"><span data-stu-id="4b076-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="4b076-421">Ponadto upewnij się, że wylogowania funkcje są dostępne na każdej stronie.</span><span class="sxs-lookup"><span data-stu-id="4b076-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="4b076-422"><a id="csrf-api"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4b076-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="4b076-423">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-423">Title</span></span>                   | <span data-ttu-id="4b076-424">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-425">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-425">**Component**</span></span>               | <span data-ttu-id="4b076-426">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-426">Web API</span></span> | 
| <span data-ttu-id="4b076-427">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-427">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-428">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-428">Build</span></span> |  
| <span data-ttu-id="4b076-429">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-429">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-430">Ogólny</span><span class="sxs-lookup"><span data-stu-id="4b076-430">Generic</span></span> |
| <span data-ttu-id="4b076-431">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-431">**Attributes**</span></span>              | <span data-ttu-id="4b076-432">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-432">N/A</span></span>  |
| <span data-ttu-id="4b076-433">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-433">**References**</span></span>              | <span data-ttu-id="4b076-434">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-434">N/A</span></span>  |
| <span data-ttu-id="4b076-435">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-435">**Steps**</span></span> | <span data-ttu-id="4b076-436">Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń hello ustanowienie sesji innego użytkownika w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b076-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="4b076-437">Celem Hello jest toomodify lub usuń zawartość, jeśli hello docelowej witryny sieci web opiera się wyłącznie na pliki cookie sesji tooauthenticate odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="4b076-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="4b076-438">Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając tooload przeglądarki innego użytkownika adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik hello jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="4b076-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="4b076-439">Istnieje wiele sposobów toodo osoby atakującej, takich jak obsługując inna witryna sieci web który ładuje zasobu z serwera narażone hello lub pobierania hello tooclick użytkownika łącza.</span><span class="sxs-lookup"><span data-stu-id="4b076-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="4b076-440">atak powitania można zapobiec, jeśli serwer hello wysyła klientowi dodatkowe toohello token, wymaga hello tooinclude klienta tokenu we wszystkich przyszłych żądań i sprawdza, czy wszystkie przyszłych żądań obejmują token, który dotyczy toohello bieżącej sesji, takie jak przez za pomocą hello ASP.NET AntiForgeryToken lub ViewState.</span><span class="sxs-lookup"><span data-stu-id="4b076-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="4b076-441">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-441">Title</span></span>                   | <span data-ttu-id="4b076-442">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-443">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-443">**Component**</span></span>               | <span data-ttu-id="4b076-444">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-444">Web API</span></span> | 
| <span data-ttu-id="4b076-445">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-445">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-446">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-446">Build</span></span> |  
| <span data-ttu-id="4b076-447">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-447">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="4b076-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="4b076-449">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-449">**Attributes**</span></span>              | <span data-ttu-id="4b076-450">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4b076-450">N/A</span></span>  |
| <span data-ttu-id="4b076-451">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-451">**References**</span></span>              | [<span data-ttu-id="4b076-452">Zapobieganie Cross-Site (CSRF) Fałszerstwie żądania w składniku ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4b076-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="4b076-453">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-453">**Steps**</span></span> | <span data-ttu-id="4b076-454">Anti-CSRF i AJAX: hello tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="4b076-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="4b076-455">Jedno rozwiązanie jest toosend hello tokenów w niestandardowy nagłówek HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b076-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="4b076-456">Witaj następujący kod używa tokenów hello toogenerate składni Razor, a następnie dodanie hello tokenów tooan AJAX żądania.</span><span class="sxs-lookup"><span data-stu-id="4b076-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="4b076-457">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="4b076-458">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-458">Example</span></span>
<span data-ttu-id="4b076-459">Podczas przetwarzania żądania hello wyodrębniania nagłówek żądania hello hello tokenów.</span><span class="sxs-lookup"><span data-stu-id="4b076-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="4b076-460">Następnie wywołaj metodę AntiForgery.Validate hello toovalidate hello tokenów.</span><span class="sxs-lookup"><span data-stu-id="4b076-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="4b076-461">Witaj metodę Validate zgłasza wyjątek, jeśli hello tokenów nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="4b076-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="4b076-462">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-462">Example</span></span>
<span data-ttu-id="4b076-463">Anti-CSRF i formularzy platformy ASP.NET MVC — hello użyj metody pomocnika AntiForgeryToken w widokach; na przykład umieścić Html.AntiForgeryToken() do postaci hello</span><span class="sxs-lookup"><span data-stu-id="4b076-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="4b076-464">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-464">Example</span></span>
<span data-ttu-id="4b076-465">w powyższym przykładzie Hello dane wyjściowe obejmują przypominać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4b076-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="4b076-466">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-466">Example</span></span>
<span data-ttu-id="4b076-467">Na powitania sam czasu, odwiedzający hello zapewnia Html.AntiForgeryToken() pliku cookie o nazwie __RequestVerificationToken z hello samą wartość jako hello losowych wartości ukryte przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="4b076-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="4b076-468">Następnie toovalidate przychodzące post formularza, Dodaj metodę akcji docelową toohello filtru hello [ValidateAntiForgeryToken].</span><span class="sxs-lookup"><span data-stu-id="4b076-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="4b076-469">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b076-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="4b076-470">Filtr autoryzacji, która sprawdza, czy:</span><span class="sxs-lookup"><span data-stu-id="4b076-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="4b076-471">żądanie przychodzące Hello ma pliku cookie o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="4b076-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="4b076-472">Witaj żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="4b076-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="4b076-473">Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, Żądanie hello przechodzi przez normalnego.</span><span class="sxs-lookup"><span data-stu-id="4b076-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="4b076-474">Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy".</span><span class="sxs-lookup"><span data-stu-id="4b076-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="4b076-475">Tytuł</span><span class="sxs-lookup"><span data-stu-id="4b076-475">Title</span></span>                   | <span data-ttu-id="4b076-476">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4b076-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4b076-477">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="4b076-477">**Component**</span></span>               | <span data-ttu-id="4b076-478">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b076-478">Web API</span></span> | 
| <span data-ttu-id="4b076-479">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="4b076-479">**SDL Phase**</span></span>               | <span data-ttu-id="4b076-480">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="4b076-480">Build</span></span> |  
| <span data-ttu-id="4b076-481">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="4b076-481">**Applicable Technologies**</span></span> | <span data-ttu-id="4b076-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="4b076-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="4b076-483">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="4b076-483">**Attributes**</span></span>              | <span data-ttu-id="4b076-484">Dostawca tożsamości dostawca — usługi AD FS, tożsamość — usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b076-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="4b076-485">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="4b076-485">**References**</span></span>              | [<span data-ttu-id="4b076-486">Zabezpieczanie interfejsu API sieci Web z indywidualnych kont i logowania lokalnego w składniku ASP.NET Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="4b076-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="4b076-487">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="4b076-487">**Steps**</span></span> | <span data-ttu-id="4b076-488">Jeśli hello interfejsu API sieci Web jest zabezpieczone przy użyciu protokołu OAuth 2.0, następnie oczekuje, że token elementu nośnego autoryzacji żądania nagłówek i Udziel dostępu toohello żądania tylko wtedy, gdy hello token jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="4b076-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="4b076-489">W przeciwieństwie do uwierzytelniania opartego na plikach cookie przeglądarki nie dołączaj toorequests tokenów elementu nośnego hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="4b076-490">Witaj żąda się, że klient musi tooexplicitly dołączyć tokenu elementu nośnego hello w nagłówku żądania hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="4b076-491">W związku z tym dla programu ASP.NET interfejsów API sieci Web chronionych przy użyciu protokołu OAuth 2.0, tokenów elementu nośnego są traktowane jako ochrona przed atakami CSRF.</span><span class="sxs-lookup"><span data-stu-id="4b076-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="4b076-492">Należy pamiętać, że jeśli hello MVC część aplikacji hello korzysta z uwierzytelniania formularzy (np. pliki cookie używane), tokenów zabezpieczających przed sfałszowaniem ma toobe używany przez aplikację sieci web MVC hello.</span><span class="sxs-lookup"><span data-stu-id="4b076-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="4b076-493">Przykład</span><span class="sxs-lookup"><span data-stu-id="4b076-493">Example</span></span>
<span data-ttu-id="4b076-494">Witaj interfejsu API sieci Web ma toobe poinformowany toorely tylko na tokenów elementu nośnego, a nie na pliki cookie.</span><span class="sxs-lookup"><span data-stu-id="4b076-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="4b076-495">Mogą to robić przez powitania po konfiguracji w `WebApiConfig.Register` — metoda: ' ' config kodu C Sharp. SuppressDefaultHostAuthentication(); Konfiguracja. Filters.Add (nowe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="4b076-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
