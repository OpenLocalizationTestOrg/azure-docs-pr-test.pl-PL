---
title: "aaaSigning przerzucania klucza w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono hello podpisywania Przerzucanie klucza najlepsze rozwiązania dotyczące usługi Azure Active Directory"
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
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="67b34-103">Podpisywanie przerzucania kluczy w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67b34-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="67b34-104">W tym temacie opisano, co należy tooknow o hello kluczy publicznych, które są używane w tokenach zabezpieczających toosign usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67b34-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="67b34-105">Jest ważne toonote, że te przerzucania kluczy w regularnych odstępach czasu i w razie zagrożenia, może być przerzuceniem natychmiast.</span><span class="sxs-lookup"><span data-stu-id="67b34-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="67b34-106">Wszystkie aplikacje, które używają usługi Azure AD powinna być stanie tooprogrammatically dojście hello Przerzucanie klucza procesu lub ustanowić proces okresowej ręczne przerzucania.</span><span class="sxs-lookup"><span data-stu-id="67b34-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="67b34-107">Kontynuuj czytanie toounderstand, jak działa hello klucze, jak tooassess hello wpływ hello przerzucania tooyour aplikacji i jak tooupdate aplikacji lub ustanawiania okresowe przerzucania ręczne Przerzucanie klucza toohandle procesu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="67b34-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="67b34-108">Omówienie kluczy podpisywania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="67b34-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="67b34-109">Usługi Azure AD wykorzystuje kryptografię klucza publicznego w oparciu branżowych standardów tooestablish zaufania między sobą i hello aplikacje, które go używają.</span><span class="sxs-lookup"><span data-stu-id="67b34-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="67b34-110">W praktyce działa to hello w następujący sposób: klucz podpisujący, który składa się z pary kluczy publicznych i prywatnych używa usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67b34-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="67b34-111">Po zalogowaniu użytkownika tooan aplikacji, która używa usługi Azure AD do uwierzytelniania usługi Azure AD tworzy token zabezpieczający, który zawiera informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="67b34-112">Token ten jest podpisany przez usługę Azure AD przy użyciu jego klucz prywatny, przed wysłaniem wstecz toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="67b34-113">tooverify, który hello token jest prawidłowy i faktycznie zdalnych z usługi Azure AD, aplikacja hello zweryfikować podpisu tokenu hello przy użyciu klucza publicznego hello udostępnianych przez usługi Azure AD, który jest zawarty w dzierżawie powitalnych [OpenID Connect dokument](http://openid.net/specs/openid-connect-discovery-1_0.html) lub SAML/WS-Fed [dokument metadanych usług federacyjnych](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="67b34-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="67b34-114">Ze względów bezpieczeństwa klucza przedstawia w regularnych odstępach czasu, a w przypadku hello awaryjnego podpisywania usługi Azure AD może być przerzuceniem natychmiast.</span><span class="sxs-lookup"><span data-stu-id="67b34-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="67b34-115">Każda aplikacja, która integruje się z usługą Azure AD powinna być przygotowana toohandle zdarzeń przerzucania klucza nie niezależnie od tego, jak często występuje.</span><span class="sxs-lookup"><span data-stu-id="67b34-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="67b34-116">Jeśli nie, a aplikacja próbuje toouse hello wygasłe tooverify klucza podpisu tokenu, hello logowania żądanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="67b34-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="67b34-117">Istnieje więcej niż jeden prawidłowy klucz dostępnych w dokumencie odnajdywania OpenID Connect hello i hello dokument metadanych usług federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="67b34-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="67b34-118">Aplikacja powinna być przygotowana toouse klawiszy hello określone w hello dokumentu, ponieważ jeden klucz mogła zostać wycofana wkrótce innego mogą być zastąpienia i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="67b34-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="67b34-119">Jak tooassess, jeśli będzie mieć wpływ na aplikację i jakie toodo informacji na ten temat</span><span class="sxs-lookup"><span data-stu-id="67b34-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="67b34-120">Jak aplikacja obsługuje Przerzucanie klucza zależy od zmienne, takie jak typ hello aplikacji lub użyto jakiego protokołu tożsamości i biblioteki.</span><span class="sxs-lookup"><span data-stu-id="67b34-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="67b34-121">Poniższe rozdziały zawierają Hello oceny, czy hello najbardziej typowych aplikacji ma wpływ na powitania przerzucania kluczy i wytyczne dotyczące sposobu tooupdate hello automatycznego przerzucania toosupport aplikacji lub ręcznie zaktualizować hello klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="67b34-122">Aplikacja Native client aplikacji dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="67b34-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="67b34-123">Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="67b34-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="67b34-124">Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="67b34-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="67b34-125">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="67b34-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="67b34-126">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="67b34-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="67b34-127">Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="67b34-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="67b34-128">Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="67b34-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="67b34-129">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="67b34-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="67b34-130">Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="67b34-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="67b34-131">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="67b34-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="67b34-132">Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2010, o 2008 przy użyciu programu Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="67b34-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="67b34-133">Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu dowolnego inne biblioteki lub ręcznie implementacją hello obsługiwane protokoły</span><span class="sxs-lookup"><span data-stu-id="67b34-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="67b34-134">Niniejsze wskazówki **nie** dotyczy:</span><span class="sxs-lookup"><span data-stu-id="67b34-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="67b34-135">Aplikacje dodane z usługi Azure AD galerii aplikacji (w tym niestandardowe) mają oddzielne wytyczne z kluczami toosigning zakresie.</span><span class="sxs-lookup"><span data-stu-id="67b34-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="67b34-136">Więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="67b34-137">Lokalne aplikacje opublikowane za pośrednictwem serwera proxy aplikacji nie ma tooworry klucze podpisywania.</span><span class="sxs-lookup"><span data-stu-id="67b34-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="67b34-138"><a name="nativeclient"></a>Aplikacja Native client aplikacji dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="67b34-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="67b34-139">Aplikacje, które uzyskują dostęp tylko do zasobów (tj.</span><span class="sxs-lookup"><span data-stu-id="67b34-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="67b34-140">Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekazują toohello właściciela zasobów.</span><span class="sxs-lookup"><span data-stu-id="67b34-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="67b34-141">Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują hello token i dlatego nie ma potrzeby tooensure, który jest poprawnie podpisany.</span><span class="sxs-lookup"><span data-stu-id="67b34-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="67b34-142">Aplikacje klienckie natywnego, czy desktop lub mobile, do tej kategorii i w związku z tym nie dotyczy hello przerzucania.</span><span class="sxs-lookup"><span data-stu-id="67b34-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="67b34-143"><a name="webclient"></a>Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="67b34-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="67b34-144">Aplikacje, które uzyskują dostęp tylko do zasobów (tj.</span><span class="sxs-lookup"><span data-stu-id="67b34-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="67b34-145">Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekazują toohello właściciela zasobów.</span><span class="sxs-lookup"><span data-stu-id="67b34-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="67b34-146">Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują hello token i dlatego nie ma potrzeby tooensure, który jest poprawnie podpisany.</span><span class="sxs-lookup"><span data-stu-id="67b34-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="67b34-147">Aplikacje sieci Web i interfejsów API używanym hello przepływu tylko do aplikacji sieci web (poświadczenia klienta / certyfikatu klienta), do tej kategorii i w związku z tym nie dotyczy hello przerzucania.</span><span class="sxs-lookup"><span data-stu-id="67b34-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="67b34-148"><a name="appservices"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="67b34-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="67b34-149">Usługa Azure App Service Authentication / automatycznie funkcjonalność autoryzacji (EasyAuth) Przerzucanie klucza toohandle niezbędne logiki hello ma już.</span><span class="sxs-lookup"><span data-stu-id="67b34-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="67b34-150"><a name="owin"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="67b34-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="67b34-151">Jeśli aplikacja używa hello .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowanie pośredniczące, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="67b34-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="67b34-152">Można potwierdzić, że aplikacja używa żadnego z nich polega na wyszukiwaniu żadnego z następujących fragmentów w pliku Startup.cs lub Startup.Auth.cs aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="67b34-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="67b34-153"><a name="owincore"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="67b34-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="67b34-154">Jeśli aplikacja używa hello .NET Core OWIN OpenID Connect lub JwtBearerAuthentication oprogramowanie pośredniczące, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="67b34-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="67b34-155">Można potwierdzić, że aplikacja używa żadnego z nich polega na wyszukiwaniu żadnego z następujących fragmentów w pliku Startup.cs lub Startup.Auth.cs aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="67b34-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="67b34-156"><a name="passport"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="67b34-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="67b34-157">Jeśli aplikacja używa modułu passport-ad Node.js hello, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="67b34-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="67b34-158">Sprawdź, czy aplikacja usługi passport-ad przez wyszukiwanie hello następującego fragmentu kodu w aplikacji app.js</span><span class="sxs-lookup"><span data-stu-id="67b34-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="67b34-159"><a name="vs2015"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="67b34-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="67b34-160">Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2015 lub Visual Studio 2017 i wybrano **konta służbowego i pracy** z hello **Zmień uwierzytelnianie** menu ono już ma Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="67b34-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="67b34-161">Tę logikę osadzone w oprogramowaniu pośredniczącym OWIN OpenID Connect hello, pobiera i przechowuje klucze hello z hello OpenID Connect dokument i okresowo odświeża je.</span><span class="sxs-lookup"><span data-stu-id="67b34-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="67b34-162">Uwierzytelniania tooyour rozwiązanie zostało dodane ręcznie, aplikacja może nie mieć hello logiki niezbędne przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="67b34-163">Konieczne będzie toowrite ją samodzielnie lub hello wykonaj kroki opisane w temacie [aplikacji sieci Web / interfejsów API przy użyciu innych biblioteki lub ręcznie implementacją hello obsługiwane protokoły.](#other).</span><span class="sxs-lookup"><span data-stu-id="67b34-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="67b34-164"><a name="vs2013"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="67b34-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="67b34-165">Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2013 i wybrano **konta organizacyjne** z hello **Zmień uwierzytelnianie** menu ma już potrzeby hello Logika toohandle klucza przerzucania automatycznie.</span><span class="sxs-lookup"><span data-stu-id="67b34-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="67b34-166">Istotą takiej logiki przechowuje unikatowy identyfikator organizacji i hello podpisywania kluczowych informacji w dwóch tabelach bazy danych skojarzony z projektem hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="67b34-167">Parametry połączenia hello hello bazy danych można znaleźć w pliku Web.config hello projektu.</span><span class="sxs-lookup"><span data-stu-id="67b34-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="67b34-168">Uwierzytelniania tooyour rozwiązanie zostało dodane ręcznie, aplikacja może nie mieć hello logiki niezbędne przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="67b34-169">Konieczne będzie toowrite ją samodzielnie lub hello wykonaj kroki opisane w temacie [aplikacji sieci Web / interfejsów API przy użyciu innych biblioteki lub ręcznie implementacją hello obsługiwane protokoły.](#other).</span><span class="sxs-lookup"><span data-stu-id="67b34-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="67b34-170">następujące kroki Hello pomoże Ci Sprawdź, czy logiki hello działa prawidłowo w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="67b34-171">W programie Visual Studio 2013, otwórz rozwiązanie hello, a następnie kliknij na powitania **Eksploratora serwera** karty w oknie prawym hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="67b34-172">Rozwiń węzeł **połączenia danych**, **połączenia DefaultConnection**, a następnie **tabel**.</span><span class="sxs-lookup"><span data-stu-id="67b34-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="67b34-173">Zlokalizuj hello **IssuingAuthorityKeys** tabeli, kliknij go prawym przyciskiem myszy, a następnie kliknij przycisk **Pokaż dane tabeli**.</span><span class="sxs-lookup"><span data-stu-id="67b34-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="67b34-174">W hello **IssuingAuthorityKeys** tabeli, będzie istnieć co najmniej jeden wiersz, co odpowiada wartości odcisku palca toohello hello klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="67b34-175">Usuń wszystkie wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="67b34-176">Kliknij prawym przyciskiem myszy hello **dzierżaw** tabeli, a następnie kliknij przycisk **Pokaż dane tabeli**.</span><span class="sxs-lookup"><span data-stu-id="67b34-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="67b34-177">W hello **dzierżawców** tabeli, będzie istnieć co najmniej jeden wiersz, co odpowiada identyfikator dzierżawy unikatowy katalog tooa.</span><span class="sxs-lookup"><span data-stu-id="67b34-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="67b34-178">Usuń wszystkie wiersze w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-178">Delete any rows in hello table.</span></span> <span data-ttu-id="67b34-179">Jeśli nie usuniesz hello wierszy w obu hello **dzierżawców** tabeli i **IssuingAuthorityKeys** tabeli, wystąpi błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="67b34-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="67b34-180">Tworzenie i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-180">Build and run hello application.</span></span> <span data-ttu-id="67b34-181">Po zarejestrowaniu się na koncie tooyour, można zatrzymać aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="67b34-182">Zwraca toohello **Eksploratora serwera** i przyjrzyj się wartości hello hello **IssuingAuthorityKeys** i **dzierżawców** tabeli.</span><span class="sxs-lookup"><span data-stu-id="67b34-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="67b34-183">Można zauważyć, że zostały one automatycznie zapełnienia hello odpowiednich informacji z hello dokument metadanych usług federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="67b34-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="67b34-184"><a name="vs2013"></a>Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="67b34-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="67b34-185">Jeśli utworzono aplikacji interfejsu API sieci web w programie Visual Studio 2013, przy użyciu szablonu interfejsu API sieci Web hello, a następnie wybrać **konta organizacyjne** z hello **Zmień uwierzytelnianie** menu, możesz już mieć hello niezbędne logikę w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="67b34-186">Jeśli ręcznie skonfigurowano uwierzytelnianie, wykonaj instrukcje hello poniżej toolearn jak tooconfigure Twojego tooautomatically interfejsu API sieci Web zaktualizować informacje klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="67b34-187">Hello poniższy fragment kodu pokazano, jak hello najnowsze kluczy z dokument metadanych usług federacyjnych hello tooget, a następnie użyj hello [programu obsługi tokenów JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="67b34-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="67b34-188">fragment kodu Hello przyjęto założenie, użyje własne buforowanie mechanizm utrwalanie przyszłych toovalidate klucza hello tokenów z usługi Azure AD, czy jest w bazy danych, w pliku konfiguracji lub w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="67b34-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
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

### <span data-ttu-id="67b34-189"><a name="vs2012"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="67b34-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="67b34-190">Jeśli aplikacja został utworzony w programie Visual Studio 2012, prawdopodobnie użyto hello tożsamości i tooconfigure narzędzia dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="67b34-191">Jest również prawdopodobne, że używasz hello [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="67b34-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="67b34-192">Witaj VINR jest odpowiedzialny za konserwację informacji o zaufanych dostawców tożsamości (Azure AD) i hello klucze toovalidate tokeny wystawione przez nich.</span><span class="sxs-lookup"><span data-stu-id="67b34-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="67b34-193">Witaj VINR ułatwia też łatwo tooautomatically aktualizacji hello klucza informacje przechowywane w pliku Web.config pobierając hello najnowsze dokument metadanych usług federacyjnych skojarzone z katalogiem sprawdzania, czy konfiguracja hello jest najnowsza wersja hello nieaktualny dokument i aktualizowania hello toouse hello nowy klucz aplikacji odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="67b34-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="67b34-194">Jeśli utworzono aplikację za pomocą przykłady kodu hello lub wskazówki z dokumentacją dostarczoną przez firmę Microsoft hello logiki Przerzucanie klucza jest już uwzględniony w projekcie.</span><span class="sxs-lookup"><span data-stu-id="67b34-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="67b34-195">Można zauważyć, że poniższy kod hello już istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="67b34-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="67b34-196">Jeśli aplikacja nie ma już tę logikę, wykonaj kroki hello poniżej tooadd i tooverify, który działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="67b34-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="67b34-197">W **Eksploratora rozwiązań**, Dodaj toohello odwołanie **System.IdentityModel** zestawu dla hello odpowiedni projekt.</span><span class="sxs-lookup"><span data-stu-id="67b34-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="67b34-198">Otwórz hello **Global.asax.cs** i dodaj następujące hello dyrektyw using:</span><span class="sxs-lookup"><span data-stu-id="67b34-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="67b34-199">Dodaj następujące metody toohello hello **Global.asax.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="67b34-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="67b34-200">Wywołanie hello **RefreshValidationSettings()** metoda hello **Application_Start()** metody w **Global.asax.cs** pokazany:</span><span class="sxs-lookup"><span data-stu-id="67b34-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="67b34-201">Po wykonaniu tych kroków hello najnowsze informacje z hello dokument metadanych usług federacyjnych, w tym klucze najnowszą hello zostaną zaktualizowane pliku Web.config aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="67b34-202">Ta aktualizacja nastąpi za każdym razem, gdy puli aplikacji jest odtwarzana w usługach IIS; Domyślnie usługi IIS jest ustawienie aplikacji toorecycle co 29 godzin.</span><span class="sxs-lookup"><span data-stu-id="67b34-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="67b34-203">Wykonaj kroki hello poniżej tooverify, czy działa hello logiki przerzucania klucza.</span><span class="sxs-lookup"><span data-stu-id="67b34-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="67b34-204">Po upewnieniu się, że aplikacja korzysta z kodu hello powyżej, otwórz hello **Web.config** pliku i przechodzić toohello  **<issuerNameRegistry>**  bloku, w szczególności wyszukiwanie powitania po kilku wierszy:</span><span class="sxs-lookup"><span data-stu-id="67b34-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="67b34-205">W hello  **<add thumbprint=””>**  Zmień ustawienie wartości odcisku palca hello przez zamianę dowolny znak inny.</span><span class="sxs-lookup"><span data-stu-id="67b34-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="67b34-206">Zapisz hello **Web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="67b34-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="67b34-207">Tworzenie aplikacji hello, a następnie ją uruchom.</span><span class="sxs-lookup"><span data-stu-id="67b34-207">Build hello application, and then run it.</span></span> <span data-ttu-id="67b34-208">Jeśli można ukończyć procesu logowania hello, aplikacja jest pomyślnie aktualizowanie klucza hello pobierając hello wymaganych informacji z dokument metadanych usług federacyjnych w Twoim katalogu.</span><span class="sxs-lookup"><span data-stu-id="67b34-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="67b34-209">Jeśli występują problemy dotyczące logowania, upewnij się, hello zmian w aplikacji są poprawne, odczytując hello [dodanie jednokrotne tooYour aplikacji sieci Web przy użyciu usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tematu lub pobieranie i zapoznanie się powitania po przykładowym kodzie: [ Chmury wielodostępne aplikacji dla usługi Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="67b34-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="67b34-210"><a name="vs2010"></a>Aplikacje sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2008 lub 2010 i .NET 3.5 w wersji 1.0 systemu Windows Identity Foundation (WIF)</span><span class="sxs-lookup"><span data-stu-id="67b34-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="67b34-211">Jeśli utworzono aplikację na WIF v1.0 nie ma nie podana mechanizmu odświeżania tooautomatically toouse konfiguracji aplikacji nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="67b34-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="67b34-212">*Najprostszym sposobem* użyj narzędzi FedUtil hello objęte hello WIF zestaw SDK, który można pobrać najnowszą wersję dokumentu metadanych hello i zaktualizowanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="67b34-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="67b34-213">Aktualizacja Twojego too.NET aplikacji 4.5, w tym hello najnowszej wersji WIF znajduje się w przestrzeni nazw systemu hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="67b34-214">Następnie można użyć hello [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform aktualizacje automatyczne konfiguracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="67b34-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="67b34-215">Wykonaj ręcznie przerzucania zgodnie z instrukcjami hello na końcu hello Niniejsze wytyczne.</span><span class="sxs-lookup"><span data-stu-id="67b34-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="67b34-216">Instrukcje toouse hello FedUtil tooupdate konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="67b34-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="67b34-217">Sprawdź, czy masz hello WIF 1.0 SDK zainstalowany na komputerze deweloperskim dla programu Visual Studio 2008 lub 2010.</span><span class="sxs-lookup"><span data-stu-id="67b34-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="67b34-218">Możesz [go pobrać stąd](https://www.microsoft.com/en-us/download/details.aspx?id=4451) Jeśli nie został jeszcze zainstalowany go.</span><span class="sxs-lookup"><span data-stu-id="67b34-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="67b34-219">W programie Visual Studio Otwórz rozwiązanie hello, a następnie kliknij prawym przyciskiem myszy projekt dotyczy hello i wybierz **aktualizacji metadanych Federacji**.</span><span class="sxs-lookup"><span data-stu-id="67b34-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="67b34-220">Jeśli ta opcja nie jest dostępna, FedUtil i/lub hello WIF 1.0 SDK nie został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="67b34-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="67b34-221">W wierszu hello wybierz **aktualizacji** toobegin aktualizowania metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="67b34-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="67b34-222">Jeśli masz środowisko serwera toohello dostępu do których aplikacja hello jest obsługiwana, można używać w FedUtil [harmonogram aktualizacji automatycznych metadanych](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="67b34-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="67b34-223">Kliknij przycisk **Zakończ** proces aktualizacji hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="67b34-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="67b34-224"><a name="other"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu dowolnego inne biblioteki lub ręcznie implementacją hello obsługiwane protokoły</span><span class="sxs-lookup"><span data-stu-id="67b34-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="67b34-225">Jeśli używasz niektóre inne biblioteki lub ręcznie zaimplementowana żadnego hello obsługiwanych protokołów, będziesz potrzebować tooreview hello biblioteki lub tooensure Twojego wdrożenia, który hello klucza jest pobierana z hello OpenID Connect dokument lub hello Dokument metadanych usług federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="67b34-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="67b34-226">Jednym ze sposobów toocheck dla tego jest toodo w kodzie lub kod biblioteki hello Wyszukaj wszystkie wywołania tooeither hello OpenID dokument lub hello dokument metadanych usług federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="67b34-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="67b34-227">Jeśli klucz jest magazynowana gdzieś lub zapisane na stałe w aplikacji, możesz ręcznie pobrać klucz hello i zaktualizuj odpowiednio przez wykonuje ręczne przerzucania zgodnie z instrukcjami hello na końcu hello Niniejsze wytyczne.</span><span class="sxs-lookup"><span data-stu-id="67b34-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="67b34-228">**Zdecydowanie zaleca się, że zwiększenia Twojej aplikacji toosupport automatycznego przerzucania** przy użyciu dowolnego hello zbliża konspektu w tym artykule tooavoid przyszłych zakłóceń i obciążenie, jeśli usługi Azure AD zwiększa jego przerzucania okresach lub ma awaryjnego przerzucania poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="67b34-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="67b34-229">Jak tootest Twojego toodetermine aplikacji, jeśli będzie mieć wpływ na</span><span class="sxs-lookup"><span data-stu-id="67b34-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="67b34-230">Można sprawdzić, czy aplikacja obsługuje automatyczne Przerzucanie klucza, pobierając hello skryptów i instrukcjami hello w [to repozytorium GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="67b34-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="67b34-231">Jak tooperform ręczne przerzucania, jeśli użytkownik aplikacji nie obsługuje automatycznego przerzucania</span><span class="sxs-lookup"><span data-stu-id="67b34-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="67b34-232">Jeśli aplikacja obsługuje **nie** obsługują automatyczne przerzucanie, w związku z tym należy tooestablish procesu, który okresowo podpisywania monitory usługi Azure AD kluczy i wykonuje ręczne przerzucania.</span><span class="sxs-lookup"><span data-stu-id="67b34-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="67b34-233">[To repozytorium GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) zawiera instrukcje i skrypty toodo to.</span><span class="sxs-lookup"><span data-stu-id="67b34-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

