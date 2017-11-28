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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="d0aae-103">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji</span><span class="sxs-lookup"><span data-stu-id="d0aae-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="d0aae-104">Witaj Identity Framework środowisko (IEF, Internet Authentication Service), źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia hello tożsamości developer toointegrate interakcji z interfejsu API RESTful w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0aae-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="d0aae-105">Na końcu hello tego przewodnika będzie możliwe toocreate podróży użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.</span><span class="sxs-lookup"><span data-stu-id="d0aae-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="d0aae-106">Hello IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="d0aae-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="d0aae-107">Witaj exchange oświadczenia interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="d0aae-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="d0aae-108">Można zaprojektować krok aranżacji.</span><span class="sxs-lookup"><span data-stu-id="d0aae-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="d0aae-109">Może wyzwolić zewnętrznego działania.</span><span class="sxs-lookup"><span data-stu-id="d0aae-109">Can trigger an external action.</span></span> <span data-ttu-id="d0aae-110">Na przykład on rejestrować zdarzenie w zewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d0aae-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="d0aae-111">Można toofetch używana wartość i zapisz go w bazie danych użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d0aae-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="d0aae-112">Można użyć oświadczeń hello Odebrano nowsze przepływu hello toochange wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d0aae-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="d0aae-113">Można również projektować interakcji hello jako profil sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="d0aae-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="d0aae-114">Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C jako sprawdzanie poprawności danych wejściowych użytkownika](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d0aae-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="d0aae-115">Scenariusz Hello jest, gdy użytkownik wykona edycji profilu, chęć:</span><span class="sxs-lookup"><span data-stu-id="d0aae-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="d0aae-116">Wyszukiwanie hello użytkownika w systemie zewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="d0aae-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="d0aae-117">Get hello Miasto, w którym użytkownik jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="d0aae-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="d0aae-118">Zwróć aplikację toohello atrybut jako oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d0aae-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0aae-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0aae-119">Prerequisites</span></span>

- <span data-ttu-id="d0aae-120">Toocomplete skonfigurowany dzierżawy usługi Azure AD B2C konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d0aae-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="d0aae-121">Toointeract punkt końcowy interfejsu API REST z.</span><span class="sxs-lookup"><span data-stu-id="d0aae-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="d0aae-122">W tym przewodniku zastosowano elementu webhook aplikacji prostych funkcji platformy Azure jako przykład.</span><span class="sxs-lookup"><span data-stu-id="d0aae-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="d0aae-123">*Zalecane*: hello pełną [interfejsu API REST oświadczeń wskazówki programu exchange na potrzeby sprawdzania poprawności](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d0aae-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="d0aae-124">Krok 1: Przygotowanie hello funkcji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="d0aae-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="d0aae-125">Instalator funkcji interfejsu API REST jest poza zakres tego artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="d0aae-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="d0aae-126">[Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą toolkit toocreate RESTful usług w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d0aae-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="d0aae-127">Firma Microsoft Konfigurowanie funkcji Azure, które otrzymuje oświadczenie o nazwie `email`, a następnie zwraca hello oświadczeń `city` o wartości hello przypisane `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="d0aae-128">przykład Hello Azure funkcja jest na [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="d0aae-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="d0aae-129">Witaj `userMessage` oświadczenie, które hello Azure zwracana jest opcjonalna w tym kontekście i hello IEF zignoruje.</span><span class="sxs-lookup"><span data-stu-id="d0aae-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="d0aae-130">Potencjalnie służy jako komunikat przekazany toohello aplikacji i przedstawione użytkownika toohello później.</span><span class="sxs-lookup"><span data-stu-id="d0aae-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="d0aae-131">Aplikacji funkcji Azure umożliwia łatwe tooget hello adres URL funkcji, identyfikatorze hello hello określonych funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0aae-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="d0aae-132">W tym przypadku jest adres URL hello: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="d0aae-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="d0aae-133">Służy on do testowania.</span><span class="sxs-lookup"><span data-stu-id="d0aae-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="d0aae-134">Krok 2: Skonfiguruj hello interfejsu API RESTful oświadczeń w programie exchange jako profil techniczne w pliku TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d0aae-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="d0aae-135">Techniczne profil jest hello pełnej konfiguracji programu exchange hello potrzeby z hello usługi RESTful.</span><span class="sxs-lookup"><span data-stu-id="d0aae-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="d0aae-136">Otwórz plik TrustFrameworkExtensions.xml hello i dodaj następujące fragment kodu XML wewnątrz hello hello `<ClaimsProvider>` elementu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="d0aae-137">W powitania po XML, dostawca RESTful `Version=1.0.0.0` jest określane jako hello protokołu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="d0aae-138">Należy wziąć pod uwagę ją jako funkcję hello, który będzie wchodzić w interakcje hello zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="d0aae-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="d0aae-139">Witaj `<InputClaims>` element definiuje hello oświadczenia, które będą wysyłane hello IEF toohello REST usługi.</span><span class="sxs-lookup"><span data-stu-id="d0aae-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="d0aae-140">W tym przykładzie hello zawartość oświadczenia hello `givenName` będą wysyłane z usługi REST toohello oświadczenia hello `email`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="d0aae-141">Witaj `<OutputClaims>` element definiuje oświadczenia hello tego hello IEF będą oczekiwać od usługi REST hello.</span><span class="sxs-lookup"><span data-stu-id="d0aae-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="d0aae-142">Niezależnie od liczby hello oświadczenia, które są odbierane hello IEF używają tylko te określone w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="d0aae-143">W tym przykładzie oświadczenie odebrana jako `city` zostanie wywołana zamapowanych tooan IEF oświadczeń `city`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="d0aae-144">Krok 3: Dodaj nowe oświadczenie hello `city` toohello schematu pliku TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d0aae-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="d0aae-145">oświadczenia Hello `city` nie jest jeszcze zdefiniowana dowolne miejsce w naszym schematu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="d0aae-146">Tak, Dodaj definicję w elemencie hello `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="d0aae-147">Ten element na początku hello hello TrustFrameworkExtensions.xml pliku można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="d0aae-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="d0aae-148">Krok 4: Obejmują wymiana oświadczeń usługi REST hello krok aranżacji w podróży użytkownika edycji profilu w TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d0aae-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="d0aae-149">Dodaj krok toohello profilu Edycja użytkownika podróży, po hello użytkownik został uwierzytelniony (procedura aranżacji 1 – 4 w powitania po XML) i hello użytkownik udostępnił hello zaktualizowane informacje o profilu (krok 5).</span><span class="sxs-lookup"><span data-stu-id="d0aae-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="d0aae-150">Istnieje wiele przypadków użycia, gdzie hello wywołaniu interfejsu API REST może służyć jako etap aranżacji.</span><span class="sxs-lookup"><span data-stu-id="d0aae-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="d0aae-151">Krok aranżacji jego mogą być używane jako aktualizacja systemu zewnętrznego tooan po pomyślnym zakończeniu zadania, takie jak rejestracji po raz pierwszy lub jako profil zaktualizować synchronizację informacji tookeep.</span><span class="sxs-lookup"><span data-stu-id="d0aae-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="d0aae-152">W takim przypadku jest używane tooaugment hello informacjami toohello aplikacji po edycji hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="d0aae-153">Kopiowanie hello profilu edytowania kodu XML przebieg użytkownika z hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml pliku wewnątrz hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="d0aae-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="d0aae-154">Następnie wprowadzić modyfikacji hello w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="d0aae-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="d0aae-155">Jeśli hello kolejność nie jest zgodna z wersją, upewnij się, Wstaw kod hello jako hello kroku przed hello `ClaimsExchange` typu `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="d0aae-156">Witaj końcowego XML hello podróż użytkownika powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d0aae-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="d0aae-157">Krok 5: Dodawanie oświadczeń hello `city` tooyour jednostki uzależnionej strony zasad plików dzięki hello oświadczenia są wysyłane tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="d0aae-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="d0aae-158">Edytuj plik ProfileEdit.xml jednostki uzależnionej strony (RP) i zmodyfikuj hello `<TechnicalProfile Id="PolicyProfile">` elementu tooadd hello następujące: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="d0aae-159">Po dodaniu hello oświadczeń nowy profil techniczne hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d0aae-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="d0aae-160">Krok 6: Przekazać zmiany i testowanie</span><span class="sxs-lookup"><span data-stu-id="d0aae-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="d0aae-161">Zastąp istniejące wersje hello hello zasad.</span><span class="sxs-lookup"><span data-stu-id="d0aae-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="d0aae-162">(Opcjonalne:) Zapisz (pobierając) hello istniejącą wersję pliku rozszerzenia przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="d0aae-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="d0aae-163">tookeep hello początkowej złożoności niski, firma Microsoft zaleca, nie przekazuj wielu wersji hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="d0aae-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="d0aae-164">(Opcjonalne:) Zmień nazwę nowej wersji identyfikator zasad hello hello zasad edycji pliku hello zmieniając `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="d0aae-165">Przekaż hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="d0aae-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="d0aae-166">Przekaż plik RP edycji zasad hello.</span><span class="sxs-lookup"><span data-stu-id="d0aae-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="d0aae-167">Użyj **Uruchom teraz** tootest hello zasad.</span><span class="sxs-lookup"><span data-stu-id="d0aae-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="d0aae-168">Przejrzyj hello token, który hello IEF zwraca toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0aae-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="d0aae-169">Jeśli wszystko jest poprawnie skonfigurowane, hello token uwzględni hello nowe oświadczenie `city`, z wartością hello `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="d0aae-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d0aae-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0aae-170">Next steps</span></span>

[<span data-ttu-id="d0aae-171">Za pośrednictwem interfejsu API REST na potrzeby sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="d0aae-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="d0aae-172">Modyfikowanie hello profilu edycji toogather dodatkowych informacji od użytkowników</span><span class="sxs-lookup"><span data-stu-id="d0aae-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
