---
title: aaaAzure AD metadanych Federacji | Dokumentacja firmy Microsoft
description: "W tym artykule opisano dokument metadanych usług federacyjnych hello publikującej usługi Azure Active Directory dla usług, które akceptują tokeny usługi Azure Active Directory."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="022bb-103">Metadane federacji</span><span class="sxs-lookup"><span data-stu-id="022bb-103">Federation metadata</span></span>
<span data-ttu-id="022bb-104">Azure Active Directory (Azure AD) publikuje dokument metadanych Federacji dla usług, które są skonfigurowane tokeny zabezpieczające hello tooaccept problemy z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="022bb-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="022bb-105">Witaj format dokumentu metadanych federacji jest opisana w hello [Web Services Federation Language (WS-Federation) w wersji 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), która rozszerza [metadanych dla hello języka OASIS Security Assertion Markup Language (SAML) w wersji 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="022bb-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="022bb-106">Punkty końcowe metadanych niezależny od dzierżawcy i specyficzne dla dzierżawy</span><span class="sxs-lookup"><span data-stu-id="022bb-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="022bb-107">Usługi Azure AD publikuje punktów końcowych specyficznego dla dzierżawy i niezależny od dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="022bb-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="022bb-108">Punkty końcowe specyficznego dla dzierżawy są przeznaczone dla konkretnego dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="022bb-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="022bb-109">metadane Federacji specyficznego dla dzierżawy Hello zawiera informacje na temat dzierżawy hello, w tym wystawcy specyficznego dla dzierżawy i informacje o punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="022bb-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="022bb-110">Aplikacje, które ograniczają dostęp tooa pojedynczej dzierżawy korzystanie z punktów końcowych specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="022bb-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="022bb-111">Punkty końcowe niezależny od dzierżawcy Podaj informacje, które są typowe dzierżaw usługi Azure AD tooall.</span><span class="sxs-lookup"><span data-stu-id="022bb-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="022bb-112">Te informacje dotyczą tootenants hostowanej w lokalizacji *login.microsoftonline.com* i jest współużytkowana przez dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="022bb-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="022bb-113">Niezależny od dzierżawcy punkty końcowe są zalecane dla wielodostępnych aplikacji, ponieważ nie są one powiązane z konkretnym dzierżawami.</span><span class="sxs-lookup"><span data-stu-id="022bb-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="022bb-114">Punkty końcowe metadanych Federacji</span><span class="sxs-lookup"><span data-stu-id="022bb-114">Federation metadata endpoints</span></span>
<span data-ttu-id="022bb-115">Usługi Azure AD publikuje metadanych federacji w `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="022bb-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="022bb-116">Dla **punkty końcowe specyficznego dla dzierżawy**, hello `TenantDomainName` może być jedną z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="022bb-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="022bb-117">Dzierżawy zarejestrowaną nazwę domeny usługi Azure AD, takich jak: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="022bb-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="022bb-118">niezmienne Hello dzierżawy identyfikator hello domeny, takich jak `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="022bb-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="022bb-119">Aby uzyskać **punkty końcowe niezależny od dzierżawcy**, hello `TenantDomainName` jest `common`.</span><span class="sxs-lookup"><span data-stu-id="022bb-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="022bb-120">Ten dokument zawiera tylko elementy metadanych Federacji hello, które są typowe tooall dzierżaw usługi Azure AD, które są hostowane na login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="022bb-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="022bb-121">Na przykład może być punkt końcowy specyficznego dla dzierżawy `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="022bb-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="022bb-122">punkt końcowy niezależny od dzierżawcy Hello jest [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="022bb-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="022bb-123">Dokument metadanych usług federacyjnych hello można wyświetlić, wpisując adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="022bb-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="022bb-124">Zawartość metadanych Federacji</span><span class="sxs-lookup"><span data-stu-id="022bb-124">Contents of federation Metadata</span></span>
<span data-ttu-id="022bb-125">Hello Poniższa sekcja zawiera informacje potrzebne usługi, które korzystają z tokenów hello wystawionych przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="022bb-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="022bb-126">Identyfikator jednostki</span><span class="sxs-lookup"><span data-stu-id="022bb-126">Entity ID</span></span>
<span data-ttu-id="022bb-127">Witaj `EntityDescriptor` zawiera element `EntityID` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="022bb-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="022bb-128">Witaj wartość hello `EntityID` Witaj wystawca reprezentuje atrybut, oznacza to, że zabezpieczeń hello token usługi (STS) hello wystawionego tokenu.</span><span class="sxs-lookup"><span data-stu-id="022bb-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="022bb-129">Po odebraniu tokenu jest ważne toovalidate hello wystawcy.</span><span class="sxs-lookup"><span data-stu-id="022bb-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="022bb-130">Witaj następujące metadane Pokazuje przykładowy specyficznego dla dzierżawy `EntityDescriptor` element z `EntityID` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="022bb-131">Można zastąpić hello identyfikator dzierżawcy w punkcie końcowym niezależne od dzierżawcy hello toocreate ID Twojej dzierżawy specyficznego dla dzierżawy `EntityID` wartość.</span><span class="sxs-lookup"><span data-stu-id="022bb-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="022bb-132">wartość wynikową Hello będzie można hello tak samo jak Witaj wystawca tokenów.</span><span class="sxs-lookup"><span data-stu-id="022bb-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="022bb-133">Strategia Hello umożliwia wystawcy hello toovalidate wielodostępnych aplikacji dla danej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="022bb-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="022bb-134">Witaj następujące metadane Pokazuje przykładowy niezależny od dzierżawcy `EntityID` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="022bb-135">Należy pamiętać, że hello `{tenant}` jest literałem nie symbol zastępczy.</span><span class="sxs-lookup"><span data-stu-id="022bb-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="022bb-136">Certyfikaty podpisywania tokenu</span><span class="sxs-lookup"><span data-stu-id="022bb-136">Token signing certificates</span></span>
<span data-ttu-id="022bb-137">Gdy usługa odbiera token wystawiony przez dzierżawę usługi Azure AD, hello podpisu tokenu hello musi zostać zweryfikowany przy użyciu klucza podpisywania, publikowana w hello dokument metadanych usług federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="022bb-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="022bb-138">metadane Federacji Hello zawierają hello części publicznej hello certyfikatom dzierżaw hello używane do podpisywania tokenu.</span><span class="sxs-lookup"><span data-stu-id="022bb-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="022bb-139">Bajty pierwotne certyfikatu Hello są wyświetlane w hello `KeyDescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="022bb-140">certyfikat podpisywania tokenu Hello jest prawidłowy dla podczas podpisywania tylko hello wartość hello `use` atrybutu `signing`.</span><span class="sxs-lookup"><span data-stu-id="022bb-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="022bb-141">Dokument metadanych Federacji, publikowane przez usługę Azure AD może mieć wielu kluczy podpisywania, np. Jeśli usługi Azure AD przygotowuje hello tooupdate certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="022bb-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="022bb-142">Gdy dokument metadanych usług federacyjnych zawiera więcej niż jeden certyfikat, to usługa, która jest sprawdzanie poprawności tokenów hello powinien obsługiwać wszystkie certyfikaty w dokumencie hello.</span><span class="sxs-lookup"><span data-stu-id="022bb-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="022bb-143">Witaj następujące metadane Pokazuje przykładowy `KeyDescriptor` elementu przy użyciu klucza podpisywania.</span><span class="sxs-lookup"><span data-stu-id="022bb-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

<span data-ttu-id="022bb-144">Witaj `KeyDescriptor` element jest wyświetlany w dwóch miejscach w dokument metadanych usług federacyjnych hello; w hello WS federacyjnego określonego i hello SAML określonej sekcji.</span><span class="sxs-lookup"><span data-stu-id="022bb-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="022bb-145">Certyfikaty Hello opublikowane w obydwie sekcje będzie hello w tej samej.</span><span class="sxs-lookup"><span data-stu-id="022bb-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="022bb-146">W sekcji hello WS federacyjnego określonego czytnika metadanych WS-Federation czytać hello certyfikatów z `RoleDescriptor` element z hello `SecurityTokenServiceType` typu.</span><span class="sxs-lookup"><span data-stu-id="022bb-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="022bb-147">Witaj następujące metadane Pokazuje przykładowy `RoleDescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="022bb-148">W sekcji hello specyficzne dla języka SAML czytnika metadanych WS-Federation czytać hello certyfikatów z `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="022bb-149">Witaj następujące metadane Pokazuje przykładowy `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="022bb-150">Nie ma żadnych różnic w formacie hello certyfikatów specyficznego dla dzierżawy i niezależny od dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="022bb-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="022bb-151">Adres URL punktu końcowego usługi WS-Federation</span><span class="sxs-lookup"><span data-stu-id="022bb-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="022bb-152">metadane Federacji Hello zawierają hello używanych dla jednego logowania i wylogowania w protokole WS-Federation pojedynczego adresu URL usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="022bb-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="022bb-153">Ten punkt końcowy jest wyświetlany w hello `PassiveRequestorEndpoint` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="022bb-154">Witaj następujące metadane Pokazuje przykładowy `PassiveRequestorEndpoint` elementu dla punktu końcowego specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="022bb-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="022bb-155">Dla punktu końcowego niezależny od dzierżawcy hello hello adresu URL protokołu WS-Federation pojawi się w punkcie końcowym hello WS-Federation, pokazane na powitania następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="022bb-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="022bb-156">Adres URL punktu końcowego protokołu SAML</span><span class="sxs-lookup"><span data-stu-id="022bb-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="022bb-157">metadane Federacji Hello zawierają hello adres URL, który używa usługi Azure AD dla jednego logowania i jednym wylogowania w protokole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="022bb-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="022bb-158">Te punkty końcowe są wyświetlane w hello `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="022bb-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="022bb-159">Witaj logowania i wylogowywania adresy URL są wyświetlane w hello `SingleSignOnService` i `SingleLogoutService` elementy.</span><span class="sxs-lookup"><span data-stu-id="022bb-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="022bb-160">Witaj następujące metadane Pokazuje przykładowy `PassiveResistorEndpoint` dla punktu końcowego specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="022bb-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="022bb-161">Podobnie hello punktów końcowych punkty końcowe hello wspólnej SAML 2.0 protokołu są publikowane w metadanych Federacji niezależny od dzierżawcy hello, jak pokazano w hello następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="022bb-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
