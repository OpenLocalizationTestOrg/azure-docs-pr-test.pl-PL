---
title: "Usługi Azure Active Directory B2C: Oświadczenia interfejsu API REST wymiany jako weryfikacji | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C"
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST usługi Azure AD B2C podróży użytkownika jako sprawdzanie poprawności danych wejściowych użytkownika

Witaj Identity Framework środowisko (IEF, Internet Authentication Service), źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia hello tożsamości developer toointegrate interakcji z interfejsu API RESTful w podróży użytkownika.  

Na końcu hello tego przewodnika będzie możliwe toocreate podróży użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.

Hello IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach. Witaj interakcji z hello interfejsu API:

- Może być zaprojektowana jako exchange oświadczenia interfejsu API REST lub profil sprawdzania poprawności, które odbywa się w kroku aranżacji.
- Zwykle sprawdza poprawność danych wejściowych od użytkownika hello. W przypadku odrzucenia wartość powitania od użytkownika hello użytkownika hello spróbować ponownie tooenter prawidłową wartość z hello możliwości tooreturn komunikat o błędzie.

Można również projektować interakcji hello krok aranżacji. Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C krok aranżacji](active-directory-b2c-rest-api-step-custom.md).

Na przykład profilu weryfikacji hello użyjemy przebieg użytkownika edycji profilu hello w pliku pakietu starter hello ProfileEdit.xml.

Możemy zweryfikować tę nazwę hello, podana przez użytkownika hello w profilu hello Edycja nie jest częścią listy wykluczeń.

## <a name="prerequisites"></a>Wymagania wstępne

- Toocomplete skonfigurowany dzierżawy usługi Azure AD B2C konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).
- Toointeract punkt końcowy interfejsu API REST z. W ramach tego przewodnika skonfigurowaliśmy pokaz lokacji o nazwie [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) za pomocą usługi interfejsu API REST.

## <a name="step-1-prepare-hello-rest-api-function"></a>Krok 1: Przygotowanie hello funkcji interfejsu API REST

> [!NOTE]
> Instalator funkcji interfejsu API REST jest poza zakres tego artykułu hello. [Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą toolkit toocreate RESTful usług w chmurze hello.

Utworzyliśmy Azure funkcja, która otrzymuje oświadczenia, że klient oczekuje jako `playerTag`. Funkcja Hello sprawdza, czy istnieje tego oświadczenia. Dostęp można uzyskać kod pełną funkcji Azure hello w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Witaj IEF oczekuje hello `userMessage` oświadczeń zwraca tego hello Azure funkcji. To oświadczenie zostanie wyświetlone jako użytkownik toohello ciągu w przypadku niepowodzenia weryfikacji hello, np. gdy 409 Konflikt stanu jest zwracany w hello poprzedzających przykład.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Krok 2: Skonfiguruj hello interfejsu API RESTful oświadczeń w programie exchange jako profil techniczne w pliku TrustFrameworkExtensions.xml

Techniczne profil jest hello pełnej konfiguracji programu exchange hello potrzeby z hello usługi RESTful. Otwórz plik TrustFrameworkExtensions.xml hello i dodaj następujące fragment kodu XML wewnątrz hello hello `<ClaimsProviders>` elementu.

> [!NOTE]
> W powitania po XML, dostawca RESTful `Version=1.0.0.0` jest określane jako hello protokołu. Należy wziąć pod uwagę ją jako funkcję hello, który będzie wchodzić w interakcje hello zewnętrznej usługi. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Witaj `InputClaims` element definiuje hello oświadczenia, które będą wysyłane hello IEF toohello REST usługi. W tym przykładzie hello zawartość oświadczenia hello `givenName` będą wysyłane usługi REST toohello jako `playerTag`. W tym przykładzie powitalne IEF nie oczekuje oświadczeń ponownie. Zamiast tego czeka na odpowiedź z usługi REST hello i czynności na podstawie kodów stanu hello, które otrzymuje.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Krok 3: Dołącz wymiana oświadczeń usługi RESTful hello własnym potwierdzona profilu techniczne miejscu dane wejściowe użytkownika hello toovalidate

najbardziej popularnym zastosowaniem Hello hello sprawdzania poprawności kroku jest hello interakcji z użytkownikiem. Wszystkie interakcje gdzie użytkownik hello jest oczekiwany tooprovide dane wejściowe są *własnym potwierdzone techniczne profile*. W tym przykładzie dodamy hello weryfikacji toohello niezależne Asserted ProfileUpdate techniczne profilu. Jest hello profil technicznych, który hello jednostki uzależnionej pliku zasad firmy (RP) `Profile Edit` używa.

tooadd hello oświadczeń exchange toohello własnym potwierdzone profilu techniczne:

1. Otwórz plik TrustFrameworkBase.xml hello i wyszukaj `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Przejrzyj konfigurację hello techniczne profilu. Sprawdź, jak exchange hello z użytkownikiem hello jest zdefiniowany jako oświadczenia, które będą proszeni hello użytkownika (oświadczenia wejściowe) i oświadczenia, które oczekuje się wstecz od dostawcy własnym potwierdzona hello (dane wyjściowe oświadczenia).
3. Wyszukaj `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`i zwróć uwagę, że ten profil jest wywoływany jako orchestration punkcie 6 `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Krok 4: Przekaż i testowania pliku zasad hello profilu edycji planu odzyskiwania

1. Przekaż nową wersję pliku TrustFrameworkExtensions.xml hello hello.
2. Użyj **Uruchom teraz** tootest hello profilu Edytuj plik zasad planu odzyskiwania.
3. Testowanie poprawności hello udostępniając jedno z istniejącymi nazwami hello (na przykład mcvinny) w hello **imię** pola. Jeśli wszystko jest poprawnie skonfigurowane, powinien zostać wyświetlony komunikat, który powiadamia użytkownika hello hello player tag jest już używana.

## <a name="next-steps"></a>Następne kroki

[Modyfikowanie hello profilu edycji i użytkownika rejestracji toogather dodatkowych informacji od użytkowników](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji](active-directory-b2c-rest-api-step-custom.md)
