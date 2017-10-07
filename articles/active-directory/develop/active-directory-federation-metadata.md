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
# <a name="federation-metadata"></a>Metadane federacji
Azure Active Directory (Azure AD) publikuje dokument metadanych Federacji dla usług, które są skonfigurowane tokeny zabezpieczające hello tooaccept problemy z usługą Azure AD. Witaj format dokumentu metadanych federacji jest opisana w hello [Web Services Federation Language (WS-Federation) w wersji 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), która rozszerza [metadanych dla hello języka OASIS Security Assertion Markup Language (SAML) w wersji 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Punkty końcowe metadanych niezależny od dzierżawcy i specyficzne dla dzierżawy
Usługi Azure AD publikuje punktów końcowych specyficznego dla dzierżawy i niezależny od dzierżawcy.

Punkty końcowe specyficznego dla dzierżawy są przeznaczone dla konkretnego dzierżawy. metadane Federacji specyficznego dla dzierżawy Hello zawiera informacje na temat dzierżawy hello, w tym wystawcy specyficznego dla dzierżawy i informacje o punkcie końcowym. Aplikacje, które ograniczają dostęp tooa pojedynczej dzierżawy korzystanie z punktów końcowych specyficznego dla dzierżawy.

Punkty końcowe niezależny od dzierżawcy Podaj informacje, które są typowe dzierżaw usługi Azure AD tooall. Te informacje dotyczą tootenants hostowanej w lokalizacji *login.microsoftonline.com* i jest współużytkowana przez dzierżawców. Niezależny od dzierżawcy punkty końcowe są zalecane dla wielodostępnych aplikacji, ponieważ nie są one powiązane z konkretnym dzierżawami.

## <a name="federation-metadata-endpoints"></a>Punkty końcowe metadanych Federacji
Usługi Azure AD publikuje metadanych federacji w `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Dla **punkty końcowe specyficznego dla dzierżawy**, hello `TenantDomainName` może być jedną z hello następujące typy:

* Dzierżawy zarejestrowaną nazwę domeny usługi Azure AD, takich jak: `contoso.onmicrosoft.com`.
* niezmienne Hello dzierżawy identyfikator hello domeny, takich jak `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Aby uzyskać **punkty końcowe niezależny od dzierżawcy**, hello `TenantDomainName` jest `common`. Ten dokument zawiera tylko elementy metadanych Federacji hello, które są typowe tooall dzierżaw usługi Azure AD, które są hostowane na login.microsoftonline.com.

Na przykład może być punkt końcowy specyficznego dla dzierżawy `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. punkt końcowy niezależny od dzierżawcy Hello jest [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Dokument metadanych usług federacyjnych hello można wyświetlić, wpisując adres URL w przeglądarce.

## <a name="contents-of-federation-metadata"></a>Zawartość metadanych Federacji
Hello Poniższa sekcja zawiera informacje potrzebne usługi, które korzystają z tokenów hello wystawionych przez usługę Azure AD.

### <a name="entity-id"></a>Identyfikator jednostki
Witaj `EntityDescriptor` zawiera element `EntityID` atrybutu. Witaj wartość hello `EntityID` Witaj wystawca reprezentuje atrybut, oznacza to, że zabezpieczeń hello token usługi (STS) hello wystawionego tokenu. Po odebraniu tokenu jest ważne toovalidate hello wystawcy.

Witaj następujące metadane Pokazuje przykładowy specyficznego dla dzierżawy `EntityDescriptor` element z `EntityID` elementu.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Można zastąpić hello identyfikator dzierżawcy w punkcie końcowym niezależne od dzierżawcy hello toocreate ID Twojej dzierżawy specyficznego dla dzierżawy `EntityID` wartość. wartość wynikową Hello będzie można hello tak samo jak Witaj wystawca tokenów. Strategia Hello umożliwia wystawcy hello toovalidate wielodostępnych aplikacji dla danej dzierżawy.

Witaj następujące metadane Pokazuje przykładowy niezależny od dzierżawcy `EntityID` elementu. Należy pamiętać, że hello `{tenant}` jest literałem nie symbol zastępczy.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certyfikaty podpisywania tokenu
Gdy usługa odbiera token wystawiony przez dzierżawę usługi Azure AD, hello podpisu tokenu hello musi zostać zweryfikowany przy użyciu klucza podpisywania, publikowana w hello dokument metadanych usług federacyjnych. metadane Federacji Hello zawierają hello części publicznej hello certyfikatom dzierżaw hello używane do podpisywania tokenu. Bajty pierwotne certyfikatu Hello są wyświetlane w hello `KeyDescriptor` elementu. certyfikat podpisywania tokenu Hello jest prawidłowy dla podczas podpisywania tylko hello wartość hello `use` atrybutu `signing`.

Dokument metadanych Federacji, publikowane przez usługę Azure AD może mieć wielu kluczy podpisywania, np. Jeśli usługi Azure AD przygotowuje hello tooupdate certyfikat podpisywania. Gdy dokument metadanych usług federacyjnych zawiera więcej niż jeden certyfikat, to usługa, która jest sprawdzanie poprawności tokenów hello powinien obsługiwać wszystkie certyfikaty w dokumencie hello.

Witaj następujące metadane Pokazuje przykładowy `KeyDescriptor` elementu przy użyciu klucza podpisywania.

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

Witaj `KeyDescriptor` element jest wyświetlany w dwóch miejscach w dokument metadanych usług federacyjnych hello; w hello WS federacyjnego określonego i hello SAML określonej sekcji. Certyfikaty Hello opublikowane w obydwie sekcje będzie hello w tej samej.

W sekcji hello WS federacyjnego określonego czytnika metadanych WS-Federation czytać hello certyfikatów z `RoleDescriptor` element z hello `SecurityTokenServiceType` typu.

Witaj następujące metadane Pokazuje przykładowy `RoleDescriptor` elementu.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

W sekcji hello specyficzne dla języka SAML czytnika metadanych WS-Federation czytać hello certyfikatów z `IDPSSODescriptor` elementu.

Witaj następujące metadane Pokazuje przykładowy `IDPSSODescriptor` elementu.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Nie ma żadnych różnic w formacie hello certyfikatów specyficznego dla dzierżawy i niezależny od dzierżawcy.

### <a name="ws-federation-endpoint-url"></a>Adres URL punktu końcowego usługi WS-Federation
metadane Federacji Hello zawierają hello używanych dla jednego logowania i wylogowania w protokole WS-Federation pojedynczego adresu URL usługi Azure AD. Ten punkt końcowy jest wyświetlany w hello `PassiveRequestorEndpoint` elementu.

Witaj następujące metadane Pokazuje przykładowy `PassiveRequestorEndpoint` elementu dla punktu końcowego specyficznego dla dzierżawy.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Dla punktu końcowego niezależny od dzierżawcy hello hello adresu URL protokołu WS-Federation pojawi się w punkcie końcowym hello WS-Federation, pokazane na powitania następujące przykładowe.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>Adres URL punktu końcowego protokołu SAML
metadane Federacji Hello zawierają hello adres URL, który używa usługi Azure AD dla jednego logowania i jednym wylogowania w protokole SAML 2.0. Te punkty końcowe są wyświetlane w hello `IDPSSODescriptor` elementu.

Witaj logowania i wylogowywania adresy URL są wyświetlane w hello `SingleSignOnService` i `SingleLogoutService` elementy.

Witaj następujące metadane Pokazuje przykładowy `PassiveResistorEndpoint` dla punktu końcowego specyficznego dla dzierżawy.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Podobnie hello punktów końcowych punkty końcowe hello wspólnej SAML 2.0 protokołu są publikowane w metadanych Federacji niezależny od dzierżawcy hello, jak pokazano w hello następujące przykładowe.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
