---
title: "Metadanych Federacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano dokument metadanych Federacji, który publikuje usługi Azure Active Directory dla usług, które akceptują tokeny usługi Azure Active Directory."
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="c5e7c-103">Metadane federacji</span><span class="sxs-lookup"><span data-stu-id="c5e7c-103">Federation metadata</span></span>
<span data-ttu-id="c5e7c-104">Azure Active Directory (Azure AD) publikuje dokument metadanych usług federacyjnych usługi skonfigurowanego do akceptowania na usługa Azure AD wystawia tokeny zabezpieczające.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="c5e7c-105">Format dokumentu metadanych federacji jest opisany w [Web Services Federation Language (WS-Federation) w wersji 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), która rozszerza [metadane języka OASIS Security Assertion Markup Language (SAML) 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="c5e7c-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="c5e7c-106">Punkty końcowe metadanych niezależny od dzierżawcy i specyficzne dla dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c5e7c-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="c5e7c-107">Usługi Azure AD publikuje punktów końcowych specyficznego dla dzierżawy i niezależny od dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="c5e7c-108">Punkty końcowe specyficznego dla dzierżawy są przeznaczone dla konkretnego dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="c5e7c-109">Metadane Federacji specyficznego dla dzierżawy zawierają informacje o dzierżawie, w tym informacje specyficzne dla dzierżawy wystawcy i punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="c5e7c-110">Aplikacje, które ograniczają dostęp do pojedynczej dzierżawy korzystanie z punktów końcowych specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="c5e7c-111">Punkty końcowe niezależny od dzierżawcy Podaj informacje, które są wspólne dla dzierżaw wszystkie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="c5e7c-112">Te informacje dotyczą hostowanej w lokalizacji dzierżawcy *login.microsoftonline.com* i jest współużytkowana przez dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="c5e7c-113">Niezależny od dzierżawcy punkty końcowe są zalecane dla wielodostępnych aplikacji, ponieważ nie są one powiązane z konkretnym dzierżawami.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="c5e7c-114">Punkty końcowe metadanych Federacji</span><span class="sxs-lookup"><span data-stu-id="c5e7c-114">Federation metadata endpoints</span></span>
<span data-ttu-id="c5e7c-115">Usługi Azure AD publikuje metadanych federacji w `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="c5e7c-116">Aby uzyskać **punkty końcowe specyficznego dla dzierżawy**, `TenantDomainName` może być jedną z następujących typów:</span><span class="sxs-lookup"><span data-stu-id="c5e7c-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="c5e7c-117">Dzierżawy zarejestrowaną nazwę domeny usługi Azure AD, takich jak: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="c5e7c-118">Niezmienne dzierżawy identyfikator domeny, takie jak `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="c5e7c-119">Aby uzyskać **punkty końcowe niezależny od dzierżawcy**, `TenantDomainName` jest `common`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="c5e7c-120">Ten dokument zawiera listę elementów metadanych Federacji, które są wspólne dla wszystkich dzierżaw usługi Azure AD, które są hostowane na login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="c5e7c-121">Na przykład może być punkt końcowy specyficznego dla dzierżawy `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="c5e7c-122">Punkt końcowy niezależny od dzierżawcy jest [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="c5e7c-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="c5e7c-123">Dokument metadanych usług federacyjnych można wyświetlić, wpisując adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="c5e7c-124">Zawartość metadanych Federacji</span><span class="sxs-lookup"><span data-stu-id="c5e7c-124">Contents of federation Metadata</span></span>
<span data-ttu-id="c5e7c-125">W poniższej sekcji przedstawiono informacje wymagane przez usługi, które korzystają z tokenów wystawiony przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="c5e7c-126">Identyfikator jednostki</span><span class="sxs-lookup"><span data-stu-id="c5e7c-126">Entity ID</span></span>
<span data-ttu-id="c5e7c-127">`EntityDescriptor` Zawiera element `EntityID` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="c5e7c-128">Wartość `EntityID` atrybut reprezentuje wystawcy, oznacza to, że usługa tokenu zabezpieczającego (STS) która wystawiła token.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="c5e7c-129">Należy zweryfikować wystawca po odebraniu tokenu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="c5e7c-130">Następujące metadane Pokazuje przykładowy specyficznego dla dzierżawy `EntityDescriptor` element z `EntityID` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="c5e7c-131">Identyfikator dzierżawcy w punkcie końcowym niezależne od dzierżawcy można zastąpić swój identyfikator dzierżawy, aby utworzyć konkretny dzierżawy `EntityID` wartość.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="c5e7c-132">Wartość wynikową będzie taka sama jak wystawcy tokenów.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="c5e7c-133">Strategia umożliwia aplikacji wielodostępnych do sprawdzania poprawności wystawcy dla danej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="c5e7c-134">Następujące metadane Pokazuje przykładowy niezależny od dzierżawcy `EntityID` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="c5e7c-135">Należy pamiętać, że `{tenant}` jest literałem nie symbol zastępczy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="c5e7c-136">Certyfikaty podpisywania tokenu</span><span class="sxs-lookup"><span data-stu-id="c5e7c-136">Token signing certificates</span></span>
<span data-ttu-id="c5e7c-137">Gdy usługa odbiera token wystawiony przez dzierżawę usługi Azure AD, podpisu tokenu musi zostać zweryfikowany przy użyciu klucza podpisywania, publikowana w dokumencie metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="c5e7c-138">Metadane Federacji zawierają publicznej części o certyfikatach używanych przez dzierżawców do podpisywania tokenu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="c5e7c-139">Bajty pierwotne certyfikatu są wyświetlane w `KeyDescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="c5e7c-140">Certyfikat podpisywania tokenu jest nieprawidłowy na potrzeby podpisywania tylko wtedy, gdy wartość `use` atrybutu `signing`.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="c5e7c-141">Dokument metadanych Federacji, publikowane przez usługę Azure AD może mieć wielu kluczy podpisywania, np. gdy przygotowuje usługi Azure AD można zaktualizować certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="c5e7c-142">Gdy dokument metadanych usług federacyjnych zawiera więcej niż jeden certyfikat, to usługa, która jest sprawdzanie poprawności tokenów powinien obsługiwać wszystkie certyfikaty w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="c5e7c-143">Następujące metadane Pokazuje przykładowy `KeyDescriptor` elementu przy użyciu klucza podpisywania.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="c5e7c-144">`KeyDescriptor` Element jest wyświetlany w dwóch miejscach w dokumencie metadanych federacji; w sekcji WS federacyjnego określonego i sekcja specyficzne dla języka SAML.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="c5e7c-145">Certyfikaty opublikowane w obydwie sekcje będzie taka sama.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="c5e7c-146">W sekcji WS federacyjnego określonego czytnika metadanych WS-Federation czytać certyfikatów z `RoleDescriptor` element z `SecurityTokenServiceType` typu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="c5e7c-147">Następujące metadane Pokazuje przykładowy `RoleDescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="c5e7c-148">W sekcji specyficzne dla języka SAML czytnika metadanych WS-Federation czytać certyfikatów z `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="c5e7c-149">Następujące metadane Pokazuje przykładowy `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="c5e7c-150">Nie ma żadnych różnic w formacie certyfikaty specyficznego dla dzierżawy i niezależny od dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="c5e7c-151">Adres URL punktu końcowego usługi WS-Federation</span><span class="sxs-lookup"><span data-stu-id="c5e7c-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="c5e7c-152">Metadane Federacji zawierają adres URL, który jest używa usługi Azure AD dla jednego logowania i jednym wylogowania w protokole WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="c5e7c-153">Ten punkt końcowy jest wyświetlany w `PassiveRequestorEndpoint` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="c5e7c-154">Następujące metadane Pokazuje przykładowy `PassiveRequestorEndpoint` elementu dla punktu końcowego specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="c5e7c-155">Dla punktu końcowego niezależny od dzierżawcy adres URL protokołu WS-Federation pojawia się w punktu końcowego usługi WS-Federation, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="c5e7c-156">Adres URL punktu końcowego protokołu SAML</span><span class="sxs-lookup"><span data-stu-id="c5e7c-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="c5e7c-157">Metadane Federacji zawierają adres URL, który używa usługi Azure AD dla jednego logowania i jednym wylogowania w protokole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="c5e7c-158">Te punkty końcowe są wyświetlane w `IDPSSODescriptor` elementu.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="c5e7c-159">Adresy URL logowania i wylogowywania są wyświetlane w `SingleSignOnService` i `SingleLogoutService` elementy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="c5e7c-160">Następujące metadane Pokazuje przykładowy `PassiveResistorEndpoint` dla punktu końcowego specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="c5e7c-161">Podobnie punktów końcowych dla typowych punktów końcowych protokołu SAML 2.0, które są publikowane w metadanych Federacji niezależny od dzierżawcy, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c5e7c-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
