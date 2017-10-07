---
title: "Usługi Azure Active Directory B2C: Oświadczenia interfejsu API REST wymiany krok aranżacji | Dokumentacja firmy Microsoft"
description: "Temat dotyczący usługi Azure Active Directory B2C niestandardowych zasad integracji z interfejsem API"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji

Witaj Identity Framework środowisko (IEF, Internet Authentication Service), źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia hello tożsamości developer toointegrate interakcji z interfejsu API RESTful w podróży użytkownika.  

Na końcu hello tego przewodnika będzie możliwe toocreate podróży użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.

Hello IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach. Witaj exchange oświadczenia interfejsu API REST:

- Można zaprojektować krok aranżacji.
- Może wyzwolić zewnętrznego działania. Na przykład on rejestrować zdarzenie w zewnętrznej bazy danych.
- Można toofetch używana wartość i zapisz go w bazie danych użytkownika hello.

Można użyć oświadczeń hello Odebrano nowsze przepływu hello toochange wykonywania.

Można również projektować interakcji hello jako profil sprawdzania poprawności. Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C jako sprawdzanie poprawności danych wejściowych użytkownika](active-directory-b2c-rest-api-validation-custom.md).

Scenariusz Hello jest, gdy użytkownik wykona edycji profilu, chęć:

1. Wyszukiwanie hello użytkownika w systemie zewnętrznym.
2. Get hello Miasto, w którym użytkownik jest zarejestrowany.
3. Zwróć aplikację toohello atrybut jako oświadczenia.

## <a name="prerequisites"></a>Wymagania wstępne

- Toocomplete skonfigurowany dzierżawy usługi Azure AD B2C konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).
- Toointeract punkt końcowy interfejsu API REST z. W tym przewodniku zastosowano elementu webhook aplikacji prostych funkcji platformy Azure jako przykład.
- *Zalecane*: hello pełną [interfejsu API REST oświadczeń wskazówki programu exchange na potrzeby sprawdzania poprawności](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Krok 1: Przygotowanie hello funkcji interfejsu API REST

> [!NOTE]
> Instalator funkcji interfejsu API REST jest poza zakres tego artykułu hello. [Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą toolkit toocreate RESTful usług w chmurze hello.

Firma Microsoft Konfigurowanie funkcji Azure, które otrzymuje oświadczenie o nazwie `email`, a następnie zwraca hello oświadczeń `city` o wartości hello przypisane `Redmond`. przykład Hello Azure funkcja jest na [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Witaj `userMessage` oświadczenie, które hello Azure zwracana jest opcjonalna w tym kontekście i hello IEF zignoruje. Potencjalnie służy jako komunikat przekazany toohello aplikacji i przedstawione użytkownika toohello później.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Aplikacji funkcji Azure umożliwia łatwe tooget hello adres URL funkcji, identyfikatorze hello hello określonych funkcji. W tym przypadku jest adres URL hello: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Służy on do testowania.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Krok 2: Skonfiguruj hello interfejsu API RESTful oświadczeń w programie exchange jako profil techniczne w pliku TrustFrameworExtensions.xml

Techniczne profil jest hello pełnej konfiguracji programu exchange hello potrzeby z hello usługi RESTful. Otwórz plik TrustFrameworkExtensions.xml hello i dodaj następujące fragment kodu XML wewnątrz hello hello `<ClaimsProvider>` elementu.

> [!NOTE]
> W powitania po XML, dostawca RESTful `Version=1.0.0.0` jest określane jako hello protokołu. Należy wziąć pod uwagę ją jako funkcję hello, który będzie wchodzić w interakcje hello zewnętrznej usługi. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Witaj `<InputClaims>` element definiuje hello oświadczenia, które będą wysyłane hello IEF toohello REST usługi. W tym przykładzie hello zawartość oświadczenia hello `givenName` będą wysyłane z usługi REST toohello oświadczenia hello `email`.  

Witaj `<OutputClaims>` element definiuje oświadczenia hello tego hello IEF będą oczekiwać od usługi REST hello. Niezależnie od liczby hello oświadczenia, które są odbierane hello IEF używają tylko te określone w tym miejscu. W tym przykładzie oświadczenie odebrana jako `city` zostanie wywołana zamapowanych tooan IEF oświadczeń `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Krok 3: Dodaj nowe oświadczenie hello `city` toohello schematu pliku TrustFrameworkExtensions.xml

oświadczenia Hello `city` nie jest jeszcze zdefiniowana dowolne miejsce w naszym schematu. Tak, Dodaj definicję w elemencie hello `<BuildingBlocks>`. Ten element na początku hello hello TrustFrameworkExtensions.xml pliku można znaleźć.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Krok 4: Obejmują wymiana oświadczeń usługi REST hello krok aranżacji w podróży użytkownika edycji profilu w TrustFrameworkExtensions.xml

Dodaj krok toohello profilu Edycja użytkownika podróży, po hello użytkownik został uwierzytelniony (procedura aranżacji 1 – 4 w powitania po XML) i hello użytkownik udostępnił hello zaktualizowane informacje o profilu (krok 5).

> [!NOTE]
> Istnieje wiele przypadków użycia, gdzie hello wywołaniu interfejsu API REST może służyć jako etap aranżacji. Krok aranżacji jego mogą być używane jako aktualizacja systemu zewnętrznego tooan po pomyślnym zakończeniu zadania, takie jak rejestracji po raz pierwszy lub jako profil zaktualizować synchronizację informacji tookeep. W takim przypadku jest używane tooaugment hello informacjami toohello aplikacji po edycji hello profilu.

Kopiowanie hello profilu edytowania kodu XML przebieg użytkownika z hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml pliku wewnątrz hello `<UserJourneys>` elementu. Następnie wprowadzić modyfikacji hello w kroku 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Jeśli hello kolejność nie jest zgodna z wersją, upewnij się, Wstaw kod hello jako hello kroku przed hello `ClaimsExchange` typu `SendClaims`.

Witaj końcowego XML hello podróż użytkownika powinien wyglądać następująco:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Krok 5: Dodawanie oświadczeń hello `city` tooyour jednostki uzależnionej strony zasad plików dzięki hello oświadczenia są wysyłane tooyour aplikacji

Edytuj plik ProfileEdit.xml jednostki uzależnionej strony (RP) i zmodyfikuj hello `<TechnicalProfile Id="PolicyProfile">` elementu tooadd hello następujące: `<OutputClaim ClaimTypeReferenceId="city" />`.

Po dodaniu hello oświadczeń nowy profil techniczne hello wygląda następująco:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Krok 6: Przekazać zmiany i testowanie

Zastąp istniejące wersje hello hello zasad.

1.  (Opcjonalne:) Zapisz (pobierając) hello istniejącą wersję pliku rozszerzenia przed kontynuowaniem. tookeep hello początkowej złożoności niski, firma Microsoft zaleca, nie przekazuj wielu wersji hello rozszerzenia pliku.
2.  (Opcjonalne:) Zmień nazwę nowej wersji identyfikator zasad hello hello zasad edycji pliku hello zmieniając `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Przekaż hello rozszerzenia pliku.
4.  Przekaż plik RP edycji zasad hello.
5.  Użyj **Uruchom teraz** tootest hello zasad. Przejrzyj hello token, który hello IEF zwraca toohello aplikacji.

Jeśli wszystko jest poprawnie skonfigurowane, hello token uwzględni hello nowe oświadczenie `city`, z wartością hello `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Następne kroki

[Za pośrednictwem interfejsu API REST na potrzeby sprawdzania poprawności](active-directory-b2c-rest-api-validation-custom.md)

[Modyfikowanie hello profilu edycji toogather dodatkowych informacji od użytkowników](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
