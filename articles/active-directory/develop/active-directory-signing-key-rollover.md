---
title: "Podpisywanie przerzucania kluczy w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono podpisywania Przerzucanie klucza najlepsze rozwiązania dotyczące usługi Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="d5bb7-103">Podpisywanie przerzucania kluczy w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5bb7-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="d5bb7-104">W tym temacie opisano, co należy wiedzieć o kluczy publicznych, które są używane w usłudze Azure Active Directory (Azure AD) do podpisywania tokenów zabezpieczających.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="d5bb7-105">Należy pamiętać, że te przerzucania kluczy w regularnych odstępach czasu i w razie zagrożenia, może być przerzuceniem natychmiast.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="d5bb7-106">Wszystkie aplikacje, które używają usługi Azure AD powinno być możliwe do programowego obsługuje procesu Przerzucanie klucza lub ustanowić proces okresowej ręczne przerzucania.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="d5bb7-107">Materiały, aby zrozumieć, jak działają kluczy ocenić wpływ Przerzucanie aplikacji oraz sposobu aktualizacji aplikacji lub ustanawiania proces okresowej przerzucania ręcznej obsługi Przerzucanie klucza, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="d5bb7-108">Omówienie kluczy podpisywania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5bb7-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="d5bb7-109">Usługi Azure AD używa oparte na standardach branżowych kryptografii klucza publicznego, aby ustanowić zaufanie między sobą i aplikacje, które go używają.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="d5bb7-110">W praktyce, to działa w następujący sposób: klucz podpisujący, który składa się z pary kluczy publicznych i prywatnych używa usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="d5bb7-111">Po zalogowaniu się do aplikacji, która używa usługi Azure AD do uwierzytelniania usługi Azure AD tworzy token zabezpieczający, który zawiera informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="d5bb7-112">Token ten jest podpisany przez usługę Azure AD przy użyciu jego klucz prywatny, przed wysłaniem do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="d5bb7-113">Aby sprawdzić, czy token jest prawidłowy i faktycznie zdalnych z usługi Azure AD, aplikacja musi zweryfikować podpisu tokenu przy użyciu klucza publicznego udostępnianych przez usługi Azure AD, który jest zawarty w dzierżawie programu [OpenID Connect dokument](http://openid.net/specs/openid-connect-discovery-1_0.html) lub SAML/WS-Fed [dokument metadanych usług federacyjnych](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="d5bb7-114">Ze względów bezpieczeństwa klucza przedstawia w regularnych odstępach czasu i, w przypadku wystąpienia sytuacji awaryjnych podpisywania Azure AD może być przerzuceniem natychmiast.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="d5bb7-115">Każda aplikacja, która integruje się z usługą Azure AD powinna być przygotowana do obsługi zdarzenia przerzucania kluczy niezależnie od tego, jak często występuje.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="d5bb7-116">Jeśli nie, a aplikacja próbuje użyć wygasły klucz można zweryfikować podpisu tokenu, żądanie logowania nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="d5bb7-117">Istnieje więcej niż jeden prawidłowy klucz dostępnych w dokumencie odnajdywania OpenID Connect i dokument metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="d5bb7-118">Aplikacja powinna być przygotowane pod kątem używania dowolnych kluczy określona w dokumencie, ponieważ jeden klucz mogła zostać wycofana wkrótce, innego może się zastąpienia itd.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="d5bb7-119">Ocenia, czy aplikacja będzie mieć wpływ na sposób i co należy zrobić informacji na ten temat</span><span class="sxs-lookup"><span data-stu-id="d5bb7-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="d5bb7-120">Jak aplikacja obsługuje Przerzucanie klucza zależy od zmienne, takie jak typ aplikacji lub użyto jakiego protokołu tożsamości i biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="d5bb7-121">W poniższych rozdziałach oceny, czy najbardziej typowych aplikacji ma wpływ na Przerzucanie klucza i zawierają wskazówki dotyczące aktualizacji aplikacji do obsługi automatycznego przerzucania lub ręcznie zaktualizować klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="d5bb7-122">Aplikacja Native client aplikacji dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="d5bb7-123">Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="d5bb7-124">Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="d5bb7-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="d5bb7-125">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="d5bb7-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="d5bb7-126">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="d5bb7-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="d5bb7-127">Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="d5bb7-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="d5bb7-128">Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="d5bb7-129">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5bb7-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="d5bb7-130">Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5bb7-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="d5bb7-131">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d5bb7-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="d5bb7-132">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2010, o 2008 przy użyciu programu Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="d5bb7-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="d5bb7-133">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu innych bibliotek lub ręcznego wykonania dowolnego z obsługiwanych protokołów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="d5bb7-134">Niniejsze wskazówki **nie** dotyczy:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="d5bb7-135">Aplikacje dodane z usługi Azure AD galerii aplikacji (w tym niestandardowe) mają oddzielne wytyczne w odniesieniu do kluczy podpisywania.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="d5bb7-136">Więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="d5bb7-137">Lokalnego nie trzeba martwić kluczy podpisywania aplikacji opublikowanych przy użyciu serwera proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="d5bb7-138"><a name="nativeclient"></a>Aplikacja Native client aplikacji dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="d5bb7-139">Aplikacje, które uzyskują dostęp tylko do zasobów (tj.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="d5bb7-140">Program Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekaż ją wzdłuż do właściciela zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="d5bb7-141">Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują token i dlatego nie trzeba upewnić się, że jest poprawnie podpisany.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="d5bb7-142">Aplikacje klienckie natywnego, czy desktop lub mobile, do tej kategorii, jak i w związku z tym nie dotyczy Przerzucanie.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="d5bb7-143"><a name="webclient"></a>Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="d5bb7-144">Aplikacje, które uzyskują dostęp tylko do zasobów (tj.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="d5bb7-145">Program Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekaż ją wzdłuż do właściciela zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="d5bb7-146">Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują token i dlatego nie trzeba upewnić się, że jest poprawnie podpisany.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="d5bb7-147">Aplikacje sieci Web i interfejsów API używanym przepływu tylko do aplikacji sieci web (poświadczenia klienta / certyfikatu klienta), do tej kategorii i w związku z tym nie dotyczy przerzucania.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="d5bb7-148"><a name="appservices"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="d5bb7-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="d5bb7-149">Usługa Azure App Service Authentication / funkcje autoryzacji (EasyAuth) ma już logikę niezbędną do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="d5bb7-150"><a name="owin"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="d5bb7-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="d5bb7-151">Jeśli aplikacja używa .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowanie pośredniczące, już logikę niezbędną do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d5bb7-152">Można potwierdzić, że aplikacja używa któregoś z powyższych, wyszukując dowolne poniższe fragmenty kodu w pliku Startup.cs lub Startup.Auth.cs aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5bb7-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="d5bb7-153"><a name="owincore"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="d5bb7-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="d5bb7-154">Jeśli aplikacja używa oprogramowania pośredniczącego .NET Core OWIN OpenID Connect lub JwtBearerAuthentication, jest już konieczne logiki do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d5bb7-155">Można potwierdzić, że aplikacja używa któregoś z powyższych, wyszukując dowolne poniższe fragmenty kodu w pliku Startup.cs lub Startup.Auth.cs aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5bb7-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="d5bb7-156"><a name="passport"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="d5bb7-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="d5bb7-157">Jeśli aplikacja używa modułu passport-ad Node.js, jest już konieczne logiki do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d5bb7-158">Sprawdź, czy aplikacja usługi passport-ad przez wyszukiwanie następujący fragment kodu w aplikacji app.js</span><span class="sxs-lookup"><span data-stu-id="d5bb7-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="d5bb7-159"><a name="vs2015"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="d5bb7-160">Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2015 lub Visual Studio 2017 i wybrano **konta służbowego i pracy** z **Zmień uwierzytelnianie** menu, jest już Logika niezbędne do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="d5bb7-161">Tę logikę osadzone w pośredniczącym OWIN OpenID Connect pobiera i przechowuje klucze z OpenID Connect dokument i okresowo odświeża je.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="d5bb7-162">Ręcznie dodane uwierzytelniania do rozwiązania, aplikacja może nie mieć logiki niezbędne przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="d5bb7-163">Musisz zapisać samodzielnie lub postępuj zgodnie z instrukcjami [aplikacji sieci Web / interfejsów API przy użyciu innych bibliotek lub ręcznego wykonania dowolnego z obsługiwanych protokołów.](#other).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="d5bb7-164"><a name="vs2013"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5bb7-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="d5bb7-165">Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2013 i wybrano **konta organizacyjne** z **Zmień uwierzytelnianie** menu, jest już konieczne logiki do obsługi automatycznego przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="d5bb7-166">Istotą takiej logiki przechowuje unikatowy identyfikator organizacji i podpisywania kluczowych informacji w dwóch tabelach bazy danych skojarzony z projektem.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="d5bb7-167">Parametry połączenia dla bazy danych można znaleźć w pliku Web.config dla projektu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="d5bb7-168">Ręcznie dodane uwierzytelniania do rozwiązania, aplikacja może nie mieć logiki niezbędne przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="d5bb7-169">Musisz zapisać samodzielnie lub postępuj zgodnie z instrukcjami [aplikacji sieci Web / interfejsów API przy użyciu innych bibliotek lub ręcznego wykonania dowolnego z obsługiwanych protokołów.](#other).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="d5bb7-170">Poniższe kroki pomoże Ci zweryfikować, że logika działa prawidłowo w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="d5bb7-171">W programie Visual Studio 2013, otwórz rozwiązanie, a następnie kliknij na **Eksploratora serwera** karty w prawym okienku.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="d5bb7-172">Rozwiń węzeł **połączenia danych**, **połączenia DefaultConnection**, a następnie **tabel**.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="d5bb7-173">Zlokalizuj **IssuingAuthorityKeys** tabeli, kliknij go prawym przyciskiem myszy, a następnie kliknij przycisk **Pokaż dane tabeli**.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="d5bb7-174">W **IssuingAuthorityKeys** tabeli, będzie istnieć co najmniej jeden wiersz, który odpowiada wartości odcisku palca dla klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="d5bb7-175">Usuń wszystkie wiersze w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="d5bb7-176">Kliknij prawym przyciskiem myszy **dzierżawców** tabeli, a następnie kliknij przycisk **Pokaż dane tabeli**.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="d5bb7-177">W **dzierżawców** tabeli, będzie istnieć co najmniej jeden wiersz, co odpowiada identyfikator dzierżawy unikatowego katalogu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="d5bb7-178">Usuń wszystkie wiersze w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-178">Delete any rows in the table.</span></span> <span data-ttu-id="d5bb7-179">Jeśli nie usuniesz wierszy w obu **dzierżawców** tabeli i **IssuingAuthorityKeys** tabeli, wystąpi błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="d5bb7-180">Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-180">Build and run the application.</span></span> <span data-ttu-id="d5bb7-181">Po zarejestrowaniu na koncie, można zatrzymać aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="d5bb7-182">Wróć do **Eksploratora serwera** i przyjrzyj się wartości w **IssuingAuthorityKeys** i **dzierżawców** tabeli.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="d5bb7-183">Można zauważyć, że zostały one automatycznie zapełnienia odpowiednie informacje z dokumentu metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="d5bb7-184"><a name="vs2013"></a>Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5bb7-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="d5bb7-185">Jeśli utworzono aplikacji interfejsu API sieci web w programie Visual Studio 2013, przy użyciu szablonu interfejsu API sieci Web, a następnie wybrać **konta organizacyjne** z **Zmień uwierzytelnianie** menu, zostały już ma logikę w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="d5bb7-186">Jeśli ręcznie skonfigurowano uwierzytelnianie, postępuj zgodnie z instrukcjami poniżej, aby dowiedzieć się, jak skonfigurować interfejs API sieci Web można automatycznie zaktualizować informacje o jego kluczu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="d5bb7-187">Poniższy fragment kodu pokazano, jak pobrać najnowsze kluczy z dokumentu metadanych Federacji, a następnie użyj [programu obsługi tokenów JWT](https://msdn.microsoft.com/library/dn205065.aspx) do sprawdzania poprawności tokenu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="d5bb7-188">Fragment kodu zakłada, że korzystasz z własnego mechanizm buforowania dla przechowywanie klucza do sprawdzania poprawności tokenów przyszłych z usługi Azure AD, czy należeć bazy danych, w pliku konfiguracji lub w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="d5bb7-189"><a name="vs2012"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d5bb7-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="d5bb7-190">Jeśli aplikacja został utworzony w programie Visual Studio 2012, prawdopodobnie używany tożsamości i dostępu do narzędzia do konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="d5bb7-191">Jest także prawdopodobne, że używasz [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="d5bb7-192">VINR jest odpowiedzialny za konserwację klucze używany do sprawdzania poprawności tokenów wystawionych przez nich i informacji o zaufanych dostawców tożsamości (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="d5bb7-193">VINR ułatwia także można automatycznie zaktualizować informacje o kluczu przechowywane w pliku Web.config przez pobieranie najnowszych dokumentu metadanych Federacji skojarzone z katalogiem, sprawdzania, czy konfiguracja jest nieaktualna z najnowszą wersję dokumentu i aktualizowanie aplikacji do użycia nowego klucza zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="d5bb7-194">Jeśli utworzono aplikację za pomocą przykłady i wskazówki z dokumentacją dostarczoną przez firmę Microsoft, logiki Przerzucanie klucza jest już uwzględniony w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="d5bb7-195">Można zauważyć, że kod poniżej już istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="d5bb7-196">Jeśli aplikacja nie ma już tę logikę, wykonaj następujące czynności, aby dodać go i sprawdź, czy działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="d5bb7-197">W **Eksploratora rozwiązań**, Dodaj odwołanie do **System.IdentityModel** zestawu dla odpowiedniego projektu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="d5bb7-198">Otwórz **Global.asax.cs** pliku i dodaj następującą dyrektyw using:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="d5bb7-199">Dodaj następującą metodę do **Global.asax.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="d5bb7-200">Wywołanie **RefreshValidationSettings()** metody w **Application_Start()** metody w **Global.asax.cs** pokazany:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="d5bb7-201">Po wykonaniu tych kroków pliku Web.config aplikacji zostaną zaktualizowane przy użyciu najnowszych informacji z dokumentu metadanych Federacji, w tym klucze najnowszą.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="d5bb7-202">Ta aktualizacja nastąpi za każdym razem, gdy puli aplikacji jest odtwarzana w usługach IIS; Domyślnie usługi IIS ustawiono odtwarzać aplikacje co 29 godzin.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="d5bb7-203">Wykonaj poniższe kroki, aby zweryfikować logiki przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="d5bb7-204">Po upewnieniu się, że aplikacja korzysta z kodu powyżej, otwórz **Web.config** pliku, a następnie przejdź do  **<issuerNameRegistry>**  bloku, w szczególności szukasz następujących kilka wierszy:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="d5bb7-205">W  **<add thumbprint=””>**  Zmień ustawienie wartości odcisku palca przez zamianę dowolny znak inny.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="d5bb7-206">Zapisz **Web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="d5bb7-207">Tworzenie aplikacji, a następnie uruchom go.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-207">Build the application, and then run it.</span></span> <span data-ttu-id="d5bb7-208">Jeśli można ukończyć procesu logowania, aplikacja jest pomyślnie aktualizowanie klucza pobierając wymaganych informacji z dokument metadanych usług federacyjnych w Twoim katalogu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="d5bb7-209">Jeśli występują problemy dotyczące logowania, upewnij się, zmiany w aplikacji są poprawne, odczytując [Dodawanie logowania jednokrotnego w sieci Web aplikacji używanie usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tematu lub pobieranie i zapoznanie się poniższy przykładowy kod: [ Chmury wielodostępne aplikacji dla usługi Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="d5bb7-210"><a name="vs2010"></a>Aplikacje sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2008 lub 2010 i .NET 3.5 w wersji 1.0 systemu Windows Identity Foundation (WIF)</span><span class="sxs-lookup"><span data-stu-id="d5bb7-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="d5bb7-211">Jeśli utworzono aplikację na 1.0 WIF nie istnieje mechanizm podany na automatyczne odświeżanie konfiguracji aplikacji do użycia nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="d5bb7-212">*Najprostszym sposobem* użyj narzędzi FedUtil dołączony WIF zestawu SDK, który można pobrać najnowszą wersję dokumentu metadanych i zaktualizowanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="d5bb7-213">Aktualizowanie aplikacji .NET 4.5, który zawiera najnowszą wersję programu WIF znajduje się w przestrzeni nazw systemu.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="d5bb7-214">Następnie można użyć [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) do wykonywania automatycznych aktualizacji konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="d5bb7-215">Wykonaj ręcznie przerzucania zgodnie z instrukcjami znajdującymi się na końcu niniejszego dokumentu wskazówki.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="d5bb7-216">Instrukcje dotyczące korzystania z FedUtil o zaktualizowanie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d5bb7-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="d5bb7-217">Sprawdź, czy masz 1.0 WIF SDK zainstalowany na komputerze deweloperskim dla programu Visual Studio 2008 lub 2010.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="d5bb7-218">Możesz [go pobrać stąd](https://www.microsoft.com/en-us/download/details.aspx?id=4451) Jeśli nie został jeszcze zainstalowany go.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="d5bb7-219">W programie Visual Studio Otwórz rozwiązanie, a następnie kliknij prawym przyciskiem myszy odpowiednie projektu i wybierz **aktualizacji metadanych Federacji**.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="d5bb7-220">Jeśli ta opcja nie jest dostępna, FedUtil i/lub 1.0 WIF zestawu SDK nie została zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="d5bb7-221">W wierszu, wybierz **aktualizacji** do rozpoczęcia aktualizowania metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="d5bb7-222">Jeśli masz dostęp do środowiska serwera, gdzie jest hostowana aplikacja można używać w FedUtil [harmonogram aktualizacji automatycznych metadanych](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5bb7-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="d5bb7-223">Kliknij przycisk **Zakończ** aby ukończyć proces aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="d5bb7-224"><a name="other"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu innych bibliotek lub ręcznego wykonania dowolnego z obsługiwanych protokołów</span><span class="sxs-lookup"><span data-stu-id="d5bb7-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="d5bb7-225">Jeśli używasz niektóre inne biblioteki lub ręcznie zaimplementowana dowolną z obsługiwanych protokołów, należy sprawdzić w bibliotece lub implementacji, aby upewnić się, że klucz jest pobierana z metadanych Federacji lub dokument odnajdywania OpenID Connect dokument.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="d5bb7-226">Jednym ze sposobów sprawdzenia tego jest przeprowadzenie wyszukiwania w kodzie lub kod biblioteki wszelkie wywołania limit dokumencie odnajdywania OpenID lub dokument metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="d5bb7-227">Jeśli klucz jest magazynowana gdzieś lub zapisane na stałe w aplikacji, możesz ręcznie pobrać klucz i odpowiednio przez wykonuje ręczne przerzucania zgodnie z instrukcjami znajdującymi się na końcu niniejszego dokumentu wskazówki dotyczące aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="d5bb7-228">**Zdecydowanie zaleca się, że ulepszanie aplikacji do obsługi automatycznego przerzucania** przy użyciu dowolnej z metod konspektu w tym artykule Aby uniknąć zakłócenia w przyszłości i koszty usługi Azure AD ma nagłych lub zwiększa jego okresach przerzucania Przerzucanie poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="d5bb7-229">Jak przetestować aplikację, aby określić, czy będzie miała wpływ</span><span class="sxs-lookup"><span data-stu-id="d5bb7-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="d5bb7-230">Można sprawdzić, czy aplikacja obsługuje automatyczne Przerzucanie klucza, pobierając skrypty i instrukcje podane w następujących [to repozytorium GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="d5bb7-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="d5bb7-231">Jak wykonać przerzucania ręczne, jeśli użytkownik aplikacji nie obsługuje automatycznego przerzucania</span><span class="sxs-lookup"><span data-stu-id="d5bb7-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="d5bb7-232">Jeśli aplikacja obsługuje **nie** obsługują automatyczne przerzucanie, należy ustanowić proces, który okresowo podpisywania monitory usługi Azure AD kluczy i odpowiednio wykonuje ręczne przerzucania.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="d5bb7-233">[To repozytorium GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) zawiera skrypty oraz instrukcje, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="d5bb7-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

