---
title: "aaaAzure pojedynczy znak SAML na protokół | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano protokołu SAML na znak pojedynczego hello w usłudze Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Jeden protokół logowania jednokrotnego SAML
W tym artykule omówiono hello SAML 2.0 uwierzytelniania żądań i odpowiedzi, które obsługuje usługi Azure Active Directory (Azure AD) dla logowania jednokrotnego.

Poniższy diagram protokołu Hello opisuje hello pojedynczy znak w sekwencji. Witaj usługi w chmurze (hello service provider) używa toopass powiązania przekierowywanie HTTP `AuthnRequest` (żądania uwierzytelniania) element tooAzure AD (hello dostawcy tożsamości). Następnie usługi Azure AD używa protokołu HTTP post powiązania toopost `Response` usługi w chmurze toohello elementu.

![Rejestracja jednokrotna przepływu pracy](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
Wyślij usługi w chmurze toorequest uwierzytelnianie użytkownika `AuthnRequest` tooAzure elementu AD. Przykładowe SAML 2.0 `AuthnRequest` może wyglądać następująco:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parametr |  | Opis |
| --- | --- | --- |
| ID |Wymagane |Ten atrybut toopopulate hello używa usługi Azure AD `InResponseTo` atrybutu hello zwrócił odpowiedź. Identyfikator nie musi rozpoczynać się od numeru, tak aby wspólnej strategii tooprepend ciągu, takich jak "id" toohello reprezentację ciągu identyfikatora GUID. Na przykład `id6c1c178c166d486687be4aaf5e482730` jest poprawnym identyfikatorem. |
| Wersja |Wymagane |To pole powinno być **2.0**. |
| IssueInstant |Wymagane |Jest to ciąg daty/godziny z wartości UTC i [obustronne formatu ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Usługi Azure AD oczekuje wartości typu DateTime tego typu, ale nie ocenę lub użyj wartości hello. |
| AssertionConsumerServiceUrl |Opcjonalne |Jeśli zostanie podana, musi on być zgodny hello `RedirectUri` hello usługi w chmurze w usłudze Azure AD. |
| ForceAuthn |Opcjonalne | Jest to wartość logiczna. Jeśli ma wartość true, oznacza to, ten użytkownik hello zostaną wymuszone toore-uwierzytelniania, nawet jeśli mają prawidłowy sesji z usługą Azure AD. |
| IsPassive |Opcjonalne |Jest to wartość logiczna określająca, czy usługi Azure AD powinna uwierzytelniać użytkowników hello w trybie dyskretnym, bez interakcji użytkownika, przy użyciu pliku cookie sesji hello, jeśli taka istnieje. Jeśli to PRAWDA, usługi Azure AD będzie podejmować tooauthenticate hello użytkownika przy użyciu pliku cookie sesji hello. |

Wszystkie inne `AuthnRequest` atrybutów, takich jak zgody, miejsce docelowe, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex i ProviderName są **ignorowane**.

Usługi Azure AD ignoruje także hello `Conditions` element `AuthnRequest`.

### Wystawcy
Witaj `Issuer` element `AuthnRequest` musi dokładnie pasować hello **ServicePrincipalNames** hello w usłudze w chmurze w usłudze Azure AD. Zazwyczaj ustawiono toohello **identyfikator URI aplikacji** określonym podczas rejestracji aplikacji.

Przykładowe fragment SAML, zawierający hello `Issuer` element wygląda następująco:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Ten element żądania format Identyfikatora nazwy określonej w odpowiedzi hello i jest opcjonalna w `AuthnRequest` tooAzure elementów wysłanych AD.

Przykładowe `NameIdPolicy` element wygląda następująco:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Jeśli `NameIDPolicy` została podana, możesz podać jego opcjonalne `Format` atrybutu. Witaj `Format` atrybut może mieć tylko jeden hello następujące wartości; wszelkie inne wartości powoduje błąd.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory powoduje wystawienie oświadczenia NameID hello identyfikatorowi parowania.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory powoduje wystawienie oświadczenia NameID hello w formacie adresu e-mail.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Ta wartość umożliwia format oświadczeń hello tooselect usługi Azure Active Directory. Usługa Azure Active Directory wystawia hello NameID identyfikatorowi parowania.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory powoduje wystawienie oświadczenia NameID hello jako wartość losowo generowany jest unikatowy toohello bieżącej operacji logowania jednokrotnego. Oznacza to, że wartość hello są tymczasowe i nie może być używane tooidentify hello uwierzytelnianie użytkownika.

Usługi Azure AD ignoruje hello `AllowCreate` atrybutu.

### RequestAuthnContext
Witaj `RequestedAuthnContext` element określa hello potrzeby metody uwierzytelniania. Jest to pozycja opcjonalna w `AuthnRequest` tooAzure elementów wysłanych AD. Usługi Azure AD obsługuje tylko jeden `AuthnContextClassRef` wartość: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Określanie zakresu
Witaj `Scoping` element, który zawiera listę dostawców tożsamości, jest opcjonalna w `AuthnRequest` tooAzure elementów wysłanych AD.

Jeśli zostanie podana, nie dołączaj hello `ProxyCount` atrybutu, `IDPListOption` lub `RequesterID` elementu, ponieważ nie są obsługiwane.

### Podpis
Nie dołączaj `Signature` element `AuthnRequest` elementów, nie obsługuje usługi Azure AD podpisanego żądania uwierzytelnienia.

### Temat
Usługi Azure AD ignoruje hello `Subject` elementu `AuthnRequest` elementów.

## Odpowiedź
Gdy żądane jednokrotnego zakończy się pomyślnie, usługi Azure AD wpisów usługi w chmurze toohello odpowiedzi. Na przykład odpowiedzi tooa pomyślne logowania jednokrotnego próby wygląda następująco:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Odpowiedź
Witaj `Response` element zawiera wynik hello hello żądania autoryzacji. Usługi Azure AD ustawia hello `ID`, `Version` i `IssueInstant` wartości hello `Response` elementu. Ustawia również hello następujące atrybuty:

* `Destination`: Podczas logowania jednokrotnego zakończy się pomyślnie, ta opcja jest ustawiona toohello `RedirectUri` dostawcy usług hello (usługi w chmurze).
* `InResponseTo`: Ta opcja jest ustawiona toohello `ID` atrybutu hello `AuthnRequest` element, który zainicjował hello odpowiedzi.

### Wystawcy
Usługi Azure AD ustawia hello `Issuer` element zbyt`https://login.microsoftonline.com/<TenantIDGUID>/` gdzie <TenantIDGUID> jest identyfikator dzierżawcy hello dzierżawcy hello Azure AD.

Na przykład przykładowa odpowiedź z elementem wystawcy może wyglądać następująco:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Stan
Witaj `Status` element umożliwia przekazywanie hello powodzenie lub Niepowodzenie logowania jednokrotnego. Obejmuje on hello `StatusCode` element, który zawiera kod lub zestaw kodów zagnieżdżone, które reprezentują hello stan żądania hello. Zawiera również hello `StatusMessage` element, który zawiera niestandardowe komunikaty o błędach wygenerowanych podczas hello logowania jednokrotnego.

<!-- TODO: Add a authentication protocol error reference -->

następujące Hello są SAML odpowiedzi tooan niepowodzeniem logowania jednokrotnego próby.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Potwierdzenia
W dodatku toohello `ID`, `IssueInstant` i `Version`, usługi Azure AD ustawia hello następujące elementy hello `Assertion` element hello odpowiedzi.

#### Wystawcy
Ta opcja jest ustawiona zbyt`https://sts.windows.net/<TenantIDGUID>/`gdzie <TenantIDGUID> jest hello identyfikator dzierżawcy dzierżawcy hello Azure AD.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Podpis
Usługi Azure AD podpisuje hello potwierdzenia w odpowiedzi tooa pomyślnego logowania jednokrotnego. Witaj `Signature` element zawiera podpis cyfrowy użyć tooauthenticate hello źródła tooverify hello integralność potwierdzenia hello hello usługi w chmurze.

toogenerate używa podpisu cyfrowego, usługi Azure AD hello klucza podpisywania w hello `IDPSSODescriptor` elementu jego dokumentu metadanych.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Temat
To ustawienie określa hello podmiotu, który podlega hello hello instrukcji w hello potwierdzenia. Zawiera on `NameID` element, który reprezentuje hello uwierzytelnionego użytkownika. Witaj `NameID` docelowe identyfikator, który jest ukierunkowanej toohello tylko dostawcy usług, który jest hello odbiorców tokenu hello jest wartość. Jest trwały — mogą być odwoływane, ale nigdy nie jest ponownie przypisywane. Możliwe jest również nieprzezroczyste, ponieważ nie ujawnia niczego o hello użytkownika i nie można użyć jako identyfikatora atrybutu zapytań.

Witaj `Method` atrybutu hello `SubjectConfirmation` element ma zawsze wartość zbyt`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Warunki
Ten element określa, że warunki, które definiują hello dopuszczalne używać potwierdzeń SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Witaj `NotBefore` i `NotOnOrAfter` atrybuty Określ interwał powitania, podczas których hello potwierdzenia jest prawidłowy.

* Witaj wartość hello `NotBefore` atrybut jest równy tooor nieco (mniej niż sekundę) później niż wartość hello `IssueInstant` atrybutu hello `Assertion` elementu. Usługi Azure AD nie bierze pod uwagę różnicę czasu między sobą i hello chmury usługi (service provider) i nie dodaje żadnych czasu toothis buforu.
* Witaj wartość hello `NotOnOrAfter` atrybut jest 70 minut później niż wartość hello hello `NotBefore` atrybutu.

#### Grupy odbiorców
Zawiera identyfikator URI, który identyfikuje określonej grupy odbiorców. Usługi Azure AD ustawia wartości hello tej wartości toohello elementu `Issuer` element hello `AuthnRequest` który zainicjował hello logowania jednokrotnego. Witaj tooevaluate `Audience` wartość, należy użyć wartości hello hello `App ID URI` , która została określona podczas rejestracji aplikacji.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Podobnie jak hello `Issuer` wartości hello `Audience` wartość musi dokładnie odpowiadać jeden hello głównych nazw usługi reprezentujące hello usługi w chmurze w usłudze Azure AD. Jednak jeśli hello wartości z hello `Issuer` element nie jest wartością identyfikatora URI hello `Audience` wartości w odpowiedzi hello jest hello `Issuer` wartość prefiks `spn:`.

#### AttributeStatement
Zawiera oświadczenia dotyczące podmiotu hello lub użytkownika. Witaj poniższy fragment podano przykładowe `AttributeStatement` elementu. wielokropka Hello wskazuje, że ten element hello może obejmować wiele atrybutów i wartości atrybutów.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Nazwa oświadczenia** : hello wartość hello `Name` atrybutu (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) to główna nazwa użytkownika hello hello uwierzytelnić użytkownika, taki jak `testuser@managedtenant.com`.
* **Oświadczenia w elemencie ObjectIdentifier** : hello wartość hello `ObjectIdentifier` atrybutu (`http://schemas.microsoft.com/identity/claims/objectidentifier`) jest hello `ObjectId` hello obiektu katalogu, który reprezentuje hello uwierzytelnić użytkownika w usłudze Azure AD. `ObjectId`Nie można modyfikować, globalnie unikatowy i ponownego użycia bezpiecznego identyfikator hello uwierzytelnianego użytkownika.

#### AuthnStatement
Ten element potwierdza, że tego podmiotu potwierdzenia hello został uwierzytelniony w szczególności sposób w określonym czasie.

* Witaj `AuthnInstant` atrybut określa czas hello użytkownika hello uwierzytelniony w usłudze Azure AD.
* Witaj `AuthnContext` element Określa kontekst uwierzytelniania hello używany tooauthenticate hello użytkownika.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```