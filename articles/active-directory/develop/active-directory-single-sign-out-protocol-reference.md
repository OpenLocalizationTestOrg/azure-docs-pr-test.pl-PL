---
title: "aaaAzure pojedynczy znak SAML limit protokół | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello jednego protokołu SAML Sign-Out w usłudze Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Protokół pojedynczego SAML wylogowania
Azure Active Directory (Azure AD) hello obsługuje jeden profil wylogowania SAML 2.0 sieci web przeglądarce. Pojedynczy toowork wylogowania poprawnie, hello **LogoutURL** dla aplikacji hello musi być jawnie zarejestrowana w usłudze Azure AD podczas rejestracji aplikacji. Usługi Azure AD używa hello LogoutURL tooredirect użytkowników po ich wyrejestrowany.

Ten diagram przedstawia przepływ pracy hello pojedynczy proces wylogowywania hello Azure AD.

![Pojedynczy Wyloguj przepływu pracy](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Witaj wysyła usługi w chmurze `LogoutRequest` tooindicate tooAzure AD komunikat zakończenia sesji. Witaj poniższy fragment przedstawiono przykładowe `LogoutRequest` elementu.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Witaj `LogoutRequest` tooAzure element wysyłane AD wymaga hello następujące atrybuty:

* `ID`: Identyfikuje hello wylogowania żądania. Witaj wartość `ID` nie powinny rozpoczynać się cyfrą. Typowy rozwiązaniem Hello jest tooappend **identyfikator** toohello reprezentacja ciągu identyfikatora GUID.
* `Version`: Wartość hello tego elementu zbyt**2.0**. Ta wartość jest wymagana.
* `IssueInstant`: W tym `DateTime` ciąg o wartości koordynować czasu uniwersalnego (UTC) i [obustronne formatu ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Usługi Azure AD oczekuje wartości tego typu, ale nie obsługuje wymuszania.

### Wystawcy
Witaj `Issuer` element `LogoutRequest` musi dokładnie pasować hello **ServicePrincipalNames** hello w usłudze w chmurze w usłudze Azure AD. Zazwyczaj ustawiono toohello **identyfikator URI aplikacji** określonym podczas rejestracji aplikacji.

### NameID
Witaj wartość hello `NameID` elementu musi dokładnie odpowiadać hello `NameID` hello użytkownika, który jest wylogowany.

## LogoutResponse
Azure AD wysyła `LogoutResponse` w odpowiedzi tooa `LogoutRequest` elementu. Witaj poniższy fragment przedstawiono przykładowe `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Usługi Azure AD ustawia hello `ID`, `Version` i `IssueInstant` wartości hello `LogoutResponse` elementu. Ustawia również hello `InResponseTo` toohello wartość elementu hello `ID` atrybutu hello `LogoutRequest` ujawniająca hello odpowiedzi.

### Wystawcy
Ustawia wartość tej usługi Azure AD za`https://login.microsoftonline.com/<TenantIdGUID>/` gdzie <TenantIdGUID> jest identyfikator dzierżawcy hello dzierżawcy hello Azure AD.

wartość hello tooevaluate hello `Issuer` elementu, użyj wartości hello hello **identyfikator URI aplikacji** podane podczas rejestracji aplikacji.

### Stan
Witaj używa usługi Azure AD `StatusCode` element hello `Status` elementu tooindicate hello powodzenie lub niepowodzenie wylogowania. Gdy hello wylogowania próba nie powiedzie się, hello `StatusCode` element może także zawierać niestandardowe komunikaty o błędach.
