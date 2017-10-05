---
title: "Azure Management - narzędzie Microsoft Threat modelowania — sesji | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń widoczne w narzędziu modelowania zagrożeń"
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
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="93ca7-103">Ramka zabezpieczeń: Zarządzanie sesjami | Artykuły</span><span class="sxs-lookup"><span data-stu-id="93ca7-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="93ca7-104">Produktów i usług</span><span class="sxs-lookup"><span data-stu-id="93ca7-104">Product/Service</span></span> | <span data-ttu-id="93ca7-105">Artykuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="93ca7-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="93ca7-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="93ca7-107">Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ca7-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="93ca7-108">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="93ca7-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="93ca7-109">Użyj ograniczone okresy istnienia generowanych tokenach SaS</span><span class="sxs-lookup"><span data-stu-id="93ca7-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="93ca7-110">**Dokumentów w usłudze Azure DB**</span><span class="sxs-lookup"><span data-stu-id="93ca7-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="93ca7-111">Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów</span><span class="sxs-lookup"><span data-stu-id="93ca7-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="93ca7-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="93ca7-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="93ca7-113">Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS</span><span class="sxs-lookup"><span data-stu-id="93ca7-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="93ca7-114">**Tożsamości serwera**</span><span class="sxs-lookup"><span data-stu-id="93ca7-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="93ca7-115">Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="93ca7-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="93ca7-116">**Aplikacja sieci Web**</span><span class="sxs-lookup"><span data-stu-id="93ca7-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="93ca7-117">Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie</span><span class="sxs-lookup"><span data-stu-id="93ca7-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="93ca7-118">Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie</span><span class="sxs-lookup"><span data-stu-id="93ca7-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="93ca7-119">Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93ca7-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="93ca7-120">Konfigurowanie sesji dla okresu istnienia aktywności</span><span class="sxs-lookup"><span data-stu-id="93ca7-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="93ca7-121">Implementuje prawidłowego wylogowania z aplikacji</span><span class="sxs-lookup"><span data-stu-id="93ca7-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="93ca7-122">**Interfejs API sieci Web**</span><span class="sxs-lookup"><span data-stu-id="93ca7-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="93ca7-123">Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93ca7-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="93ca7-124"><a id="logout-adal"></a>Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ca7-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="93ca7-125">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-125">Title</span></span>                   | <span data-ttu-id="93ca7-126">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-127">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-127">**Component**</span></span>               | <span data-ttu-id="93ca7-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ca7-128">Azure AD</span></span> | 
| <span data-ttu-id="93ca7-129">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-129">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-130">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-130">Build</span></span> |  
| <span data-ttu-id="93ca7-131">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-131">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-132">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-132">Generic</span></span> |
| <span data-ttu-id="93ca7-133">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-133">**Attributes**</span></span>              | <span data-ttu-id="93ca7-134">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-134">N/A</span></span>  |
| <span data-ttu-id="93ca7-135">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-135">**References**</span></span>              | <span data-ttu-id="93ca7-136">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-136">N/A</span></span>  |
| <span data-ttu-id="93ca7-137">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-137">**Steps**</span></span> | <span data-ttu-id="93ca7-138">Jeśli aplikacja opiera się na token dostępu wystawiony przez usługę Azure AD, powinny wywoływać wylogowania programu obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="93ca7-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="93ca7-139">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="93ca7-140">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-140">Example</span></span>
<span data-ttu-id="93ca7-141">Należy także zniszczyć sesji użytkownika, wywołując metodę Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="93ca7-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="93ca7-142">Następujące metody przedstawia bezpiecznej implementacji wylogowania użytkownika:</span><span class="sxs-lookup"><span data-stu-id="93ca7-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="93ca7-143"><a id="finite-tokens"></a>Użyj ograniczone okresy istnienia generowanych tokenach SaS</span><span class="sxs-lookup"><span data-stu-id="93ca7-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="93ca7-144">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-144">Title</span></span>                   | <span data-ttu-id="93ca7-145">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-146">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-146">**Component**</span></span>               | <span data-ttu-id="93ca7-147">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="93ca7-147">IoT Device</span></span> | 
| <span data-ttu-id="93ca7-148">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-148">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-149">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-149">Build</span></span> |  
| <span data-ttu-id="93ca7-150">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-150">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-151">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-151">Generic</span></span> |
| <span data-ttu-id="93ca7-152">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-152">**Attributes**</span></span>              | <span data-ttu-id="93ca7-153">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-153">N/A</span></span>  |
| <span data-ttu-id="93ca7-154">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-154">**References**</span></span>              | <span data-ttu-id="93ca7-155">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-155">N/A</span></span>  |
| <span data-ttu-id="93ca7-156">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-156">**Steps**</span></span> | <span data-ttu-id="93ca7-157">Tokeny sygnatury dostępu współdzielonego wygenerowane do uwierzytelniania w usłudze Azure IoT Hub powinny mieć okresu wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="93ca7-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="93ca7-158">Zachowaj okresy istnienia tokenu sygnatury dostępu współdzielonego do minimum, aby ograniczyć ilość czasu, który może być odtwarzany w przypadku naruszenia zabezpieczeń tokeny.</span><span class="sxs-lookup"><span data-stu-id="93ca7-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="93ca7-159"><a id="resource-tokens"></a>Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów</span><span class="sxs-lookup"><span data-stu-id="93ca7-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="93ca7-160">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-160">Title</span></span>                   | <span data-ttu-id="93ca7-161">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-162">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-162">**Component**</span></span>               | <span data-ttu-id="93ca7-163">Dokumentów w usłudze Azure DB</span><span class="sxs-lookup"><span data-stu-id="93ca7-163">Azure Document DB</span></span> | 
| <span data-ttu-id="93ca7-164">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-164">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-165">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-165">Build</span></span> |  
| <span data-ttu-id="93ca7-166">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-166">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-167">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-167">Generic</span></span> |
| <span data-ttu-id="93ca7-168">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-168">**Attributes**</span></span>              | <span data-ttu-id="93ca7-169">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-169">N/A</span></span>  |
| <span data-ttu-id="93ca7-170">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-170">**References**</span></span>              | <span data-ttu-id="93ca7-171">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-171">N/A</span></span>  |
| <span data-ttu-id="93ca7-172">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-172">**Steps**</span></span> | <span data-ttu-id="93ca7-173">Zmniejsz zakres czasu tokenu zasobów minimalną wartość wymaganą.</span><span class="sxs-lookup"><span data-stu-id="93ca7-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="93ca7-174">Tokeny zasobów ma prawidłowy obiekt timespan domyślnej 1 godz.</span><span class="sxs-lookup"><span data-stu-id="93ca7-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="93ca7-175"><a id="wsfederation-logout"></a>Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS</span><span class="sxs-lookup"><span data-stu-id="93ca7-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="93ca7-176">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-176">Title</span></span>                   | <span data-ttu-id="93ca7-177">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-178">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-178">**Component**</span></span>               | <span data-ttu-id="93ca7-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="93ca7-179">ADFS</span></span> | 
| <span data-ttu-id="93ca7-180">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-180">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-181">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-181">Build</span></span> |  
| <span data-ttu-id="93ca7-182">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-182">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-183">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-183">Generic</span></span> |
| <span data-ttu-id="93ca7-184">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-184">**Attributes**</span></span>              | <span data-ttu-id="93ca7-185">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-185">N/A</span></span>  |
| <span data-ttu-id="93ca7-186">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-186">**References**</span></span>              | <span data-ttu-id="93ca7-187">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-187">N/A</span></span>  |
| <span data-ttu-id="93ca7-188">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-188">**Steps**</span></span> | <span data-ttu-id="93ca7-189">Jeśli aplikacja używa tokenu Zabezpieczającego wydane przez usługi AD FS, program obsługi zdarzeń wylogowania powinien wywoływać metodę WSFederationAuthenticationModule.FederatedSignOut() się wylogować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93ca7-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="93ca7-190">Również zostać zniszczone w bieżącej sesji, a wartość tokenu sesji należy zresetować i zniweczone.</span><span class="sxs-lookup"><span data-stu-id="93ca7-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-191">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="93ca7-192"><a id="proper-logout"></a>Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="93ca7-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="93ca7-193">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-193">Title</span></span>                   | <span data-ttu-id="93ca7-194">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-195">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-195">**Component**</span></span>               | <span data-ttu-id="93ca7-196">Tożsamości serwera</span><span class="sxs-lookup"><span data-stu-id="93ca7-196">Identity Server</span></span> | 
| <span data-ttu-id="93ca7-197">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-197">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-198">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-198">Build</span></span> |  
| <span data-ttu-id="93ca7-199">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-199">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-200">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-200">Generic</span></span> |
| <span data-ttu-id="93ca7-201">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-201">**Attributes**</span></span>              | <span data-ttu-id="93ca7-202">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-202">N/A</span></span>  |
| <span data-ttu-id="93ca7-203">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-203">**References**</span></span>              | [<span data-ttu-id="93ca7-204">Federacyjna IdentityServer3 wylogowaniu</span><span class="sxs-lookup"><span data-stu-id="93ca7-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="93ca7-205">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-205">**Steps**</span></span> | <span data-ttu-id="93ca7-206">IdentityServer obsługuje możliwości utworzenia federacji z dostawców tożsamości zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="93ca7-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="93ca7-207">Gdy użytkownik zaloguje się poza dostawcy tożsamości nadrzędnego, w zależności od używanego protokołu, może być możliwe otrzymywać powiadomienia po wylogowaniu się użytkownika. Umożliwia on IdentityServer do powiadamiania klientów, ich można również wylogowanie użytkownika. Zapoznaj się z dokumentacją w sekcji odwołań dla szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="93ca7-208"><a id="https-secure-cookies"></a>Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie</span><span class="sxs-lookup"><span data-stu-id="93ca7-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="93ca7-209">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-209">Title</span></span>                   | <span data-ttu-id="93ca7-210">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-211">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-211">**Component**</span></span>               | <span data-ttu-id="93ca7-212">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-212">Web Application</span></span> | 
| <span data-ttu-id="93ca7-213">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-213">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-214">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-214">Build</span></span> |  
| <span data-ttu-id="93ca7-215">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-215">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-216">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-216">Generic</span></span> |
| <span data-ttu-id="93ca7-217">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-217">**Attributes**</span></span>              | <span data-ttu-id="93ca7-218">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="93ca7-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="93ca7-219">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-219">**References**</span></span>              | <span data-ttu-id="93ca7-220">[httpCookies — Element (schemat ustawień programu ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure właściwości](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="93ca7-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="93ca7-221">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-221">**Steps**</span></span> | <span data-ttu-id="93ca7-222">Pliki cookie są zwykle dostępne jedynie do domeny, dla którego zostały zakres.</span><span class="sxs-lookup"><span data-stu-id="93ca7-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="93ca7-223">Niestety definicji "domeny" nie zawierają protokołu, dlatego plików cookie, które są tworzone przy użyciu protokołu HTTPS są dostępne za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="93ca7-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="93ca7-224">W przeglądarce atrybutu "secure" wskazuje, czy plik cookie powinien tylko udostępniane za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="93ca7-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="93ca7-225">Upewnij się, że wszystkie pliki cookie ustawione za pośrednictwem protokołu HTTPS, użyj **bezpiecznego** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="93ca7-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="93ca7-226">To wymaganie można wymusić w pliku web.config przez ustawienie atrybutu parametru requireSSL na wartość true.</span><span class="sxs-lookup"><span data-stu-id="93ca7-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="93ca7-227">Jest to preferowane rozwiązanie, ponieważ wymuszają **bezpiecznego** atrybutu dla wszystkich plików cookie obecne i przyszłe bez konieczności zmiany dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="93ca7-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-228">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="93ca7-229">Ustawienia zaczynają obowiązywać nawet wtedy, gdy HTTP jest używany do uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="93ca7-230">Jeśli HTTP jest używany do uzyskania dostępu do aplikacji, ustawienia dzieli aplikacji, ponieważ pliki cookie są konfigurowane przy użyciu atrybutu secure i przeglądarka nie będzie wysyłać je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="93ca7-231">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-231">Title</span></span>                   | <span data-ttu-id="93ca7-232">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-233">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-233">**Component**</span></span>               | <span data-ttu-id="93ca7-234">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-234">Web Application</span></span> | 
| <span data-ttu-id="93ca7-235">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-235">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-236">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-236">Build</span></span> |  
| <span data-ttu-id="93ca7-237">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-237">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-238">Formularze sieci Web, MVC5</span><span class="sxs-lookup"><span data-stu-id="93ca7-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="93ca7-239">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-239">**Attributes**</span></span>              | <span data-ttu-id="93ca7-240">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="93ca7-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="93ca7-241">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-241">**References**</span></span>              | <span data-ttu-id="93ca7-242">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-242">N/A</span></span>  |
| <span data-ttu-id="93ca7-243">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-243">**Steps**</span></span> | <span data-ttu-id="93ca7-244">Gdy aplikacja sieci web jest uzależniona oraz rozszerzeniu IdP serwera usług AD FS, atrybut bezpiecznego tokenu FedAuth można skonfigurować przez ustawienie parametru requireSSL na wartość True w `system.identityModel.services` sekcji w pliku Web.config:</span><span class="sxs-lookup"><span data-stu-id="93ca7-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-245">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="93ca7-246"><a id="cookie-definition"></a>Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie</span><span class="sxs-lookup"><span data-stu-id="93ca7-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="93ca7-247">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-247">Title</span></span>                   | <span data-ttu-id="93ca7-248">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-249">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-249">**Component**</span></span>               | <span data-ttu-id="93ca7-250">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-250">Web Application</span></span> | 
| <span data-ttu-id="93ca7-251">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-251">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-252">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-252">Build</span></span> |  
| <span data-ttu-id="93ca7-253">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-253">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-254">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-254">Generic</span></span> |
| <span data-ttu-id="93ca7-255">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-255">**Attributes**</span></span>              | <span data-ttu-id="93ca7-256">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-256">N/A</span></span>  |
| <span data-ttu-id="93ca7-257">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-257">**References**</span></span>              | [<span data-ttu-id="93ca7-258">Atrybut bezpiecznego pliku Cookie</span><span class="sxs-lookup"><span data-stu-id="93ca7-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="93ca7-259">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-259">**Steps**</span></span> | <span data-ttu-id="93ca7-260">Aby zmniejszyć ryzyko ujawnienia informacji z atak skryptów między witrynami (XSS), nowy atrybut — httpOnly - wprowadzono w celu pliki cookie i jest obsługiwana przez wszystkie główne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="93ca7-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="93ca7-261">Ten atrybut określa, czy plik cookie nie jest dostępny za pośrednictwem skryptu.</span><span class="sxs-lookup"><span data-stu-id="93ca7-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="93ca7-262">Za pomocą plików cookie HttpOnly, aplikacji sieci web zmniejsza prawdopodobieństwo poufne dane zawarte w pliku cookie może być kradzieży za pomocą skryptu i wysyłany do witryny internetowej osoby atakującej.</span><span class="sxs-lookup"><span data-stu-id="93ca7-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="93ca7-263">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-263">Example</span></span>
<span data-ttu-id="93ca7-264">Wszystkie aplikacje oparte na protokole HTTP, które używają plików cookie należy określić HttpOnly w definicji pliku cookie, implementując następujących konfiguracji w pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="93ca7-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="93ca7-265">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-265">Title</span></span>                   | <span data-ttu-id="93ca7-266">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-267">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-267">**Component**</span></span>               | <span data-ttu-id="93ca7-268">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-268">Web Application</span></span> | 
| <span data-ttu-id="93ca7-269">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-269">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-270">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-270">Build</span></span> |  
| <span data-ttu-id="93ca7-271">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-271">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-272">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-272">Web Forms</span></span> |
| <span data-ttu-id="93ca7-273">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-273">**Attributes**</span></span>              | <span data-ttu-id="93ca7-274">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-274">N/A</span></span>  |
| <span data-ttu-id="93ca7-275">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-275">**References**</span></span>              | [<span data-ttu-id="93ca7-276">Właściwość FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="93ca7-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="93ca7-277">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-277">**Steps**</span></span> | <span data-ttu-id="93ca7-278">Wartość parametru RequireSSL właściwości jest ustawiana w pliku konfiguracji dla aplikacji ASP.NET przy użyciu atrybutu parametru requireSSL elementu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="93ca7-279">Można określić w pliku Web.config dla aplikacji ASP.NET czy SSL (Secure Sockets Layer) jest wymagany do zwrócenia pliku cookie uwierzytelniania formularzy do serwera przez ustawienie atrybutu parametru requireSSL.</span><span class="sxs-lookup"><span data-stu-id="93ca7-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-280">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-280">Example</span></span> 
<span data-ttu-id="93ca7-281">Poniższy przykład kodu ustawia atrybut parametru requireSSL w pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="93ca7-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="93ca7-282">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-282">Title</span></span>                   | <span data-ttu-id="93ca7-283">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-284">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-284">**Component**</span></span>               | <span data-ttu-id="93ca7-285">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-285">Web Application</span></span> | 
| <span data-ttu-id="93ca7-286">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-286">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-287">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-287">Build</span></span> |  
| <span data-ttu-id="93ca7-288">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-288">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="93ca7-289">MVC5</span></span> |
| <span data-ttu-id="93ca7-290">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-290">**Attributes**</span></span>              | <span data-ttu-id="93ca7-291">EnvironmentType - lokalnego programu</span><span class="sxs-lookup"><span data-stu-id="93ca7-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="93ca7-292">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-292">**References**</span></span>              | [<span data-ttu-id="93ca7-293">Windows Identity Foundation (WIF) Konfiguracja — część II</span><span class="sxs-lookup"><span data-stu-id="93ca7-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="93ca7-294">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-294">**Steps**</span></span> | <span data-ttu-id="93ca7-295">Aby ustawić atrybut httpOnly plików cookie FedAuth, wartość atrybutu hideFromCsript powinien mieć ustawioną wartość True.</span><span class="sxs-lookup"><span data-stu-id="93ca7-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="93ca7-296">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-296">Example</span></span>
<span data-ttu-id="93ca7-297">Następująca konfiguracja zawiera prawidłowej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="93ca7-297">Following configuration shows the correct configuration:</span></span>
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

## <span data-ttu-id="93ca7-298"><a id="csrf-asp"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93ca7-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="93ca7-299">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-299">Title</span></span>                   | <span data-ttu-id="93ca7-300">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-301">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-301">**Component**</span></span>               | <span data-ttu-id="93ca7-302">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-302">Web Application</span></span> | 
| <span data-ttu-id="93ca7-303">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-303">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-304">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-304">Build</span></span> |  
| <span data-ttu-id="93ca7-305">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-305">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-306">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-306">Generic</span></span> |
| <span data-ttu-id="93ca7-307">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-307">**Attributes**</span></span>              | <span data-ttu-id="93ca7-308">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-308">N/A</span></span>  |
| <span data-ttu-id="93ca7-309">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-309">**References**</span></span>              | <span data-ttu-id="93ca7-310">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-310">N/A</span></span>  |
| <span data-ttu-id="93ca7-311">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-311">**Steps**</span></span> | <span data-ttu-id="93ca7-312">Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń ustanowienie sesji innego użytkownika w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="93ca7-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="93ca7-313">Celem jest modyfikowania lub usuwania zawartości, jeśli docelowa witryna sieci web opiera się wyłącznie na pliki cookie z sesji do odebrane żądanie uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="93ca7-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="93ca7-314">Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając przeglądarki innego użytkownika, aby załadować adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="93ca7-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="93ca7-315">Istnieje wiele sposobów, atakujący może to zrobić, takich jak inna witryna sieci web, ładowaną zasobu na serwerze narażony, lub pobierania użytkownika, kliknięcie łącza.</span><span class="sxs-lookup"><span data-stu-id="93ca7-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="93ca7-316">Ataków można zapobiec, jeśli serwer wysyła dodatkowe token do klienta, wymaga od klienta do dołączenia token wszystkich przyszłych żądań i sprawdza, czy wszystkich przyszłych żądań zawierać token, który odnoszą się do bieżącej sesji, takie jak przy użyciu platformy ASP.NET AntiForgeryToken lub ViewState.</span><span class="sxs-lookup"><span data-stu-id="93ca7-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="93ca7-317">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-317">Title</span></span>                   | <span data-ttu-id="93ca7-318">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-319">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-319">**Component**</span></span>               | <span data-ttu-id="93ca7-320">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-320">Web Application</span></span> | 
| <span data-ttu-id="93ca7-321">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-321">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-322">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-322">Build</span></span> |  
| <span data-ttu-id="93ca7-323">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-323">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="93ca7-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="93ca7-325">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-325">**Attributes**</span></span>              | <span data-ttu-id="93ca7-326">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-326">N/A</span></span>  |
| <span data-ttu-id="93ca7-327">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-327">**References**</span></span>              | [<span data-ttu-id="93ca7-328">Zapobieganie XSRF/CSRF w platformie ASP.NET MVC i stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="93ca7-329">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-329">**Steps**</span></span> | <span data-ttu-id="93ca7-330">Użyj Anti-CSRF i formularzy platformy ASP.NET MVC — `AntiForgeryToken` metody pomocniczej w widokach; ujmij `Html.AntiForgeryToken()` w formularzu, na przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-331">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="93ca7-332">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="93ca7-333">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-333">Example</span></span>
<span data-ttu-id="93ca7-334">W tym samym czasie Html.AntiForgeryToken() zapewnia obiekt odwiedzający pliku cookie o nazwie __RequestVerificationToken z taką samą wartość jak losowych wartości ukryte przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="93ca7-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="93ca7-335">Następnie można sprawdzić poprawności przychodzącego post formularza, Dodaj filtr [ValidateAntiForgeryToken] do docelowego metody akcji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="93ca7-336">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="93ca7-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="93ca7-337">Filtr autoryzacji, która sprawdza, czy:</span><span class="sxs-lookup"><span data-stu-id="93ca7-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="93ca7-338">Żądanie przychodzące ma pliku cookie o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="93ca7-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="93ca7-339">Żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="93ca7-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="93ca7-340">Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, żądanie przechodzi przez normalnego.</span><span class="sxs-lookup"><span data-stu-id="93ca7-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="93ca7-341">Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy".</span><span class="sxs-lookup"><span data-stu-id="93ca7-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="93ca7-342">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-342">Example</span></span>
<span data-ttu-id="93ca7-343">Anti-CSRF i AJAX: tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="93ca7-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="93ca7-344">Rozwiązanie polega na wysyłanie tokenów w niestandardowy nagłówek HTTP.</span><span class="sxs-lookup"><span data-stu-id="93ca7-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="93ca7-345">Poniższy kod używa składni Razor do generowania tokenów, a następnie dodaje tokenów na żądanie AJAX.</span><span class="sxs-lookup"><span data-stu-id="93ca7-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="93ca7-346">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-346">Example</span></span>
<span data-ttu-id="93ca7-347">Podczas przetwarzania żądania, Wyodrębnij tokenów w nagłówku żądania.</span><span class="sxs-lookup"><span data-stu-id="93ca7-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="93ca7-348">Następnie wywołaj metodę AntiForgery.Validate do weryfikacji tokenów.</span><span class="sxs-lookup"><span data-stu-id="93ca7-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="93ca7-349">Metoda weryfikacji zgłasza wyjątek, jeśli tokenów nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="93ca7-349">The Validate method throws an exception if the tokens are not valid.</span></span>
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

| <span data-ttu-id="93ca7-350">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-350">Title</span></span>                   | <span data-ttu-id="93ca7-351">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-352">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-352">**Component**</span></span>               | <span data-ttu-id="93ca7-353">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-353">Web Application</span></span> | 
| <span data-ttu-id="93ca7-354">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-354">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-355">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-355">Build</span></span> |  
| <span data-ttu-id="93ca7-356">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-356">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-357">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-357">Web Forms</span></span> |
| <span data-ttu-id="93ca7-358">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-358">**Attributes**</span></span>              | <span data-ttu-id="93ca7-359">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-359">N/A</span></span>  |
| <span data-ttu-id="93ca7-360">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-360">**References**</span></span>              | [<span data-ttu-id="93ca7-361">Korzystać z funkcji wbudowanych ASP.NET w celu zapobieżenia poza atakami z sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="93ca7-362">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-362">**Steps**</span></span> | <span data-ttu-id="93ca7-363">Ataki CSRF w aplikacjach na podstawie formularza sieci Web można zminimalizować przez ustawienie ViewStateUserKey losowy ciąg, który jest różny dla każdego użytkownika — identyfikator użytkownika lub jeszcze lepiej identyfikator sesji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="93ca7-364">Istnieje wiele możliwych przyczyn technicznych i społecznościowych identyfikator sesji jest znacznie lepszym rozwiązaniem, ponieważ identyfikator jest nieoczekiwane, sesji upłynie limit czasu i zmienia się na poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="93ca7-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-365">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-365">Example</span></span>
<span data-ttu-id="93ca7-366">Oto kod, który musi być w wszystkie strony:</span><span class="sxs-lookup"><span data-stu-id="93ca7-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="93ca7-367"><a id="inactivity-lifetime"></a>Konfigurowanie sesji dla okresu istnienia aktywności</span><span class="sxs-lookup"><span data-stu-id="93ca7-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="93ca7-368">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-368">Title</span></span>                   | <span data-ttu-id="93ca7-369">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-370">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-370">**Component**</span></span>               | <span data-ttu-id="93ca7-371">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-371">Web Application</span></span> | 
| <span data-ttu-id="93ca7-372">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-372">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-373">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-373">Build</span></span> |  
| <span data-ttu-id="93ca7-374">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-374">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-375">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-375">Generic</span></span> |
| <span data-ttu-id="93ca7-376">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-376">**Attributes**</span></span>              | <span data-ttu-id="93ca7-377">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-377">N/A</span></span>  |
| <span data-ttu-id="93ca7-378">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-378">**References**</span></span>              | <span data-ttu-id="93ca7-379">[Właściwość HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="93ca7-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="93ca7-380">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-380">**Steps**</span></span> | <span data-ttu-id="93ca7-381">Limit czasu sesji reprezentuje zdarzenie występuje, gdy użytkownik nie wykonywania dowolnych akcji w witrynie sieci web dla interwału (zdefiniowane przez serwer sieci web).</span><span class="sxs-lookup"><span data-stu-id="93ca7-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="93ca7-382">Zdarzenia po stronie serwera, Zmień stan sesji użytkownika do "nieprawidłowe" (na przykład "nie już używać") i serwer sieci web do zniszczenia (usunięcie wszystkich danych znajdujących się w niej).</span><span class="sxs-lookup"><span data-stu-id="93ca7-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="93ca7-383">Poniższy przykład kodu ustawia atrybut limitu czasu sesji do 15 minut, w pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="93ca7-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-384">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-384">Example</span></span>
<span data-ttu-id="93ca7-385">"" Kod XML <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="93ca7-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="93ca7-386">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-386">Title</span></span>                   | <span data-ttu-id="93ca7-387">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-388">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-388">**Component**</span></span>               | <span data-ttu-id="93ca7-389">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-389">Web Application</span></span> | 
| <span data-ttu-id="93ca7-390">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-390">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-391">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-391">Build</span></span> |  
| <span data-ttu-id="93ca7-392">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-392">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-393">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-393">Web Forms</span></span> |
| <span data-ttu-id="93ca7-394">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-394">**Attributes**</span></span>              | <span data-ttu-id="93ca7-395">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-395">N/A</span></span>  |
| <span data-ttu-id="93ca7-396">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-396">**References**</span></span>              | <span data-ttu-id="93ca7-397">[Tworzy Element uwierzytelniania (schemat ustawień programu ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="93ca7-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="93ca7-398">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-398">**Steps**</span></span> | <span data-ttu-id="93ca7-399">Ustaw limit czasu plików cookie biletu uwierzytelniania formularzy do 15 minut</span><span class="sxs-lookup"><span data-stu-id="93ca7-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="93ca7-400">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-400">Example</span></span>
<span data-ttu-id="93ca7-401">"" Kod XML<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="93ca7-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="93ca7-402">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-402">Example</span></span>
<span data-ttu-id="93ca7-403">Również usług AD FS wystawiony SAML oświadczeń okres istnienia tokenu powinien być ustawiony na 15 minut, wykonując następujące polecenia programu powershell na serwerze usług AD FS:</span><span class="sxs-lookup"><span data-stu-id="93ca7-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="93ca7-404"><a id="proper-app-logout"></a>Implementuje prawidłowego wylogowania z aplikacji</span><span class="sxs-lookup"><span data-stu-id="93ca7-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="93ca7-405">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-405">Title</span></span>                   | <span data-ttu-id="93ca7-406">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-407">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-407">**Component**</span></span>               | <span data-ttu-id="93ca7-408">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-408">Web Application</span></span> | 
| <span data-ttu-id="93ca7-409">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-409">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-410">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-410">Build</span></span> |  
| <span data-ttu-id="93ca7-411">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-411">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-412">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-412">Generic</span></span> |
| <span data-ttu-id="93ca7-413">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-413">**Attributes**</span></span>              | <span data-ttu-id="93ca7-414">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-414">N/A</span></span>  |
| <span data-ttu-id="93ca7-415">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-415">**References**</span></span>              | <span data-ttu-id="93ca7-416">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-416">N/A</span></span>  |
| <span data-ttu-id="93ca7-417">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-417">**Steps**</span></span> | <span data-ttu-id="93ca7-418">Wykonaj odpowiednie Wyloguj z aplikacji, gdy użytkownik naciśnie Wyloguj się przycisk.</span><span class="sxs-lookup"><span data-stu-id="93ca7-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="93ca7-419">Podczas wylogowania aplikacji należy zniszczyć sesji użytkownika, resetowanie oraz zniesienia wartość pliku cookie sesji, oraz resetowanie i rozpoczynającą wartość pliku cookie uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="93ca7-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="93ca7-420">Ponadto jeśli wiele sesji są powiązane z tożsamością pojedynczego użytkownika, one musi być zbiorczo zakończona po stronie serwera na limitu czasu lub Wyloguj.</span><span class="sxs-lookup"><span data-stu-id="93ca7-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="93ca7-421">Ponadto upewnij się, że wylogowania funkcje są dostępne na każdej stronie.</span><span class="sxs-lookup"><span data-stu-id="93ca7-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="93ca7-422"><a id="csrf-api"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93ca7-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="93ca7-423">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-423">Title</span></span>                   | <span data-ttu-id="93ca7-424">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-425">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-425">**Component**</span></span>               | <span data-ttu-id="93ca7-426">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-426">Web API</span></span> | 
| <span data-ttu-id="93ca7-427">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-427">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-428">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-428">Build</span></span> |  
| <span data-ttu-id="93ca7-429">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-429">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-430">Ogólny</span><span class="sxs-lookup"><span data-stu-id="93ca7-430">Generic</span></span> |
| <span data-ttu-id="93ca7-431">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-431">**Attributes**</span></span>              | <span data-ttu-id="93ca7-432">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-432">N/A</span></span>  |
| <span data-ttu-id="93ca7-433">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-433">**References**</span></span>              | <span data-ttu-id="93ca7-434">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-434">N/A</span></span>  |
| <span data-ttu-id="93ca7-435">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-435">**Steps**</span></span> | <span data-ttu-id="93ca7-436">Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń ustanowienie sesji innego użytkownika w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="93ca7-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="93ca7-437">Celem jest modyfikowania lub usuwania zawartości, jeśli docelowa witryna sieci web opiera się wyłącznie na pliki cookie z sesji do odebrane żądanie uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="93ca7-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="93ca7-438">Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając przeglądarki innego użytkownika, aby załadować adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="93ca7-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="93ca7-439">Istnieje wiele sposobów, atakujący może to zrobić, takich jak inna witryna sieci web, ładowaną zasobu na serwerze narażony, lub pobierania użytkownika, kliknięcie łącza.</span><span class="sxs-lookup"><span data-stu-id="93ca7-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="93ca7-440">Ataków można zapobiec, jeśli serwer wysyła dodatkowe token do klienta, wymaga od klienta do dołączenia token wszystkich przyszłych żądań i sprawdza, czy wszystkich przyszłych żądań zawierać token, który odnoszą się do bieżącej sesji, takie jak przy użyciu platformy ASP.NET AntiForgeryToken lub ViewState.</span><span class="sxs-lookup"><span data-stu-id="93ca7-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="93ca7-441">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-441">Title</span></span>                   | <span data-ttu-id="93ca7-442">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-443">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-443">**Component**</span></span>               | <span data-ttu-id="93ca7-444">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-444">Web API</span></span> | 
| <span data-ttu-id="93ca7-445">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-445">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-446">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-446">Build</span></span> |  
| <span data-ttu-id="93ca7-447">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-447">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="93ca7-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="93ca7-449">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-449">**Attributes**</span></span>              | <span data-ttu-id="93ca7-450">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="93ca7-450">N/A</span></span>  |
| <span data-ttu-id="93ca7-451">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-451">**References**</span></span>              | [<span data-ttu-id="93ca7-452">Zapobieganie Cross-Site (CSRF) Fałszerstwie żądania w składniku ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="93ca7-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="93ca7-453">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-453">**Steps**</span></span> | <span data-ttu-id="93ca7-454">Anti-CSRF i AJAX: tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="93ca7-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="93ca7-455">Rozwiązanie polega na wysyłanie tokenów w niestandardowy nagłówek HTTP.</span><span class="sxs-lookup"><span data-stu-id="93ca7-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="93ca7-456">Poniższy kod używa składni Razor do generowania tokenów, a następnie dodaje tokenów na żądanie AJAX.</span><span class="sxs-lookup"><span data-stu-id="93ca7-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="93ca7-457">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="93ca7-458">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-458">Example</span></span>
<span data-ttu-id="93ca7-459">Podczas przetwarzania żądania, Wyodrębnij tokenów w nagłówku żądania.</span><span class="sxs-lookup"><span data-stu-id="93ca7-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="93ca7-460">Następnie wywołaj metodę AntiForgery.Validate do weryfikacji tokenów.</span><span class="sxs-lookup"><span data-stu-id="93ca7-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="93ca7-461">Metoda weryfikacji zgłasza wyjątek, jeśli tokenów nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="93ca7-461">The Validate method throws an exception if the tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="93ca7-462">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-462">Example</span></span>
<span data-ttu-id="93ca7-463">Anti-CSRF i formularzy platformy ASP.NET MVC — użyj metody pomocnika AntiForgeryToken widoków; na przykład umieścić Html.AntiForgeryToken() w formularzu</span><span class="sxs-lookup"><span data-stu-id="93ca7-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="93ca7-464">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-464">Example</span></span>
<span data-ttu-id="93ca7-465">W powyższym przykładzie dane wyjściowe obejmują postać zbliżoną do następującej:</span><span class="sxs-lookup"><span data-stu-id="93ca7-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="93ca7-466">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-466">Example</span></span>
<span data-ttu-id="93ca7-467">W tym samym czasie Html.AntiForgeryToken() zapewnia obiekt odwiedzający pliku cookie o nazwie __RequestVerificationToken z taką samą wartość jak losowych wartości ukryte przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="93ca7-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="93ca7-468">Następnie można sprawdzić poprawności przychodzącego post formularza, Dodaj filtr [ValidateAntiForgeryToken] do docelowego metody akcji.</span><span class="sxs-lookup"><span data-stu-id="93ca7-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="93ca7-469">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="93ca7-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="93ca7-470">Filtr autoryzacji, która sprawdza, czy:</span><span class="sxs-lookup"><span data-stu-id="93ca7-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="93ca7-471">Żądanie przychodzące ma pliku cookie o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="93ca7-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="93ca7-472">Żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="93ca7-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="93ca7-473">Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, żądanie przechodzi przez normalnego.</span><span class="sxs-lookup"><span data-stu-id="93ca7-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="93ca7-474">Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy".</span><span class="sxs-lookup"><span data-stu-id="93ca7-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="93ca7-475">Tytuł</span><span class="sxs-lookup"><span data-stu-id="93ca7-475">Title</span></span>                   | <span data-ttu-id="93ca7-476">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="93ca7-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="93ca7-477">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="93ca7-477">**Component**</span></span>               | <span data-ttu-id="93ca7-478">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="93ca7-478">Web API</span></span> | 
| <span data-ttu-id="93ca7-479">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="93ca7-479">**SDL Phase**</span></span>               | <span data-ttu-id="93ca7-480">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93ca7-480">Build</span></span> |  
| <span data-ttu-id="93ca7-481">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="93ca7-481">**Applicable Technologies**</span></span> | <span data-ttu-id="93ca7-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="93ca7-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="93ca7-483">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="93ca7-483">**Attributes**</span></span>              | <span data-ttu-id="93ca7-484">Dostawca tożsamości dostawca — usługi AD FS, tożsamość — usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ca7-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="93ca7-485">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="93ca7-485">**References**</span></span>              | [<span data-ttu-id="93ca7-486">Zabezpieczanie interfejsu API sieci Web z indywidualnych kont i logowania lokalnego w składniku ASP.NET Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="93ca7-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="93ca7-487">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="93ca7-487">**Steps**</span></span> | <span data-ttu-id="93ca7-488">Jeśli interfejs API sieci Web jest zabezpieczone przy użyciu protokołu OAuth 2.0, następnie je oczekuje tokenu elementu nośnego w nagłówku żądania autoryzacji i nieograniczony dostęp do żądania tylko wtedy, gdy token jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="93ca7-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="93ca7-489">W przeciwieństwie do uwierzytelniania opartego na plikach cookie przeglądarki nie dołączyć do żądania tokenów elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="93ca7-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="93ca7-490">Klienta należy Dołącz w sposób jawny tokenu elementu nośnego w nagłówku żądania.</span><span class="sxs-lookup"><span data-stu-id="93ca7-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="93ca7-491">W związku z tym dla programu ASP.NET interfejsów API sieci Web chronionych przy użyciu protokołu OAuth 2.0, tokenów elementu nośnego są traktowane jako ochrona przed atakami CSRF.</span><span class="sxs-lookup"><span data-stu-id="93ca7-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="93ca7-492">Należy pamiętać, że jeśli część aplikacji MVC korzysta z uwierzytelniania formularzy (np. pliki cookie używane), tokenów zabezpieczających przed sfałszowaniem musi być używany przez aplikację sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="93ca7-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="93ca7-493">Przykład</span><span class="sxs-lookup"><span data-stu-id="93ca7-493">Example</span></span>
<span data-ttu-id="93ca7-494">Interfejs API sieci Web musi mieć świadomość, aby polegać wyłącznie na tokenów elementu nośnego i pliki cookie nie w.</span><span class="sxs-lookup"><span data-stu-id="93ca7-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="93ca7-495">Mogą to robić przez następującą konfigurację w `WebApiConfig.Register` — metoda: ' ' config kodu C Sharp. SuppressDefaultHostAuthentication(); Konfiguracja. Filters.Add (nowe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="93ca7-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.