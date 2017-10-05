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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="b5159-103">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji</span><span class="sxs-lookup"><span data-stu-id="b5159-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="b5159-104">Tożsamość środowiska Framework (IEF) źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia deweloperowi tożsamości integracji interakcji z interfejsu API RESTful w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5159-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="b5159-105">Na końcu tego przewodnika można utworzyć przebieg użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.</span><span class="sxs-lookup"><span data-stu-id="b5159-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="b5159-106">IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="b5159-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="b5159-107">Wymiana oświadczenia interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="b5159-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="b5159-108">Można zaprojektować krok aranżacji.</span><span class="sxs-lookup"><span data-stu-id="b5159-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="b5159-109">Może wyzwolić zewnętrznego działania.</span><span class="sxs-lookup"><span data-stu-id="b5159-109">Can trigger an external action.</span></span> <span data-ttu-id="b5159-110">Na przykład on rejestrować zdarzenie w zewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5159-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="b5159-111">Umożliwia pobieranie wartości, a następnie zapisać ją w bazie danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5159-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="b5159-112">Odebrano oświadczeń można użyć później, aby zmienić sposób wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b5159-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="b5159-113">Można również projektować interakcji jako profil sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="b5159-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="b5159-114">Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C jako sprawdzanie poprawności danych wejściowych użytkownika](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b5159-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="b5159-115">Scenariusz jest, gdy użytkownik wykona edycji profilu, chęć:</span><span class="sxs-lookup"><span data-stu-id="b5159-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="b5159-116">Wyszukiwanie użytkownika w systemie zewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="b5159-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="b5159-117">Pobierz miasto, w którym użytkownik jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="b5159-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="b5159-118">Zwróć tego atrybutu w aplikacji jako oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b5159-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5159-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5159-119">Prerequisites</span></span>

- <span data-ttu-id="b5159-120">Dzierżawy usługi Azure AD B2C, skonfigurowany tak, aby ukończyć konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b5159-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="b5159-121">Punkt końcowy interfejsu API REST do interakcji z.</span><span class="sxs-lookup"><span data-stu-id="b5159-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="b5159-122">W tym przewodniku zastosowano elementu webhook aplikacji prostych funkcji platformy Azure jako przykład.</span><span class="sxs-lookup"><span data-stu-id="b5159-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="b5159-123">*Zalecane*: zakończenie [interfejsu API REST oświadczeń wskazówki programu exchange na potrzeby sprawdzania poprawności](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b5159-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="b5159-124">Krok 1: Przygotowanie funkcji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b5159-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="b5159-125">Instalator funkcji interfejsu API REST jest poza zakres tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5159-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="b5159-126">[Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą zestawu narzędzi do tworzenia usługi RESTful w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b5159-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="b5159-127">Firma Microsoft Konfigurowanie funkcji Azure, które otrzymuje oświadczenie o nazwie `email`, a następnie zwraca oświadczenia `city` z przypisaną wartością `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="b5159-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="b5159-128">Przykład funkcji platformy Azure jest na [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="b5159-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="b5159-129">`userMessage` Oświadczenie, które zwraca funkcja Azure jest opcjonalna w tym kontekście i IEF zignoruje.</span><span class="sxs-lookup"><span data-stu-id="b5159-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="b5159-130">Może potencjalnie używać go jako wiadomości do aplikacji i użytkownik widzi później.</span><span class="sxs-lookup"><span data-stu-id="b5159-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="b5159-131">Aplikacja Azure funkcji można łatwo uzyskać adres URL funkcji, która zawiera identyfikator określoną funkcję.</span><span class="sxs-lookup"><span data-stu-id="b5159-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="b5159-132">W tym przypadku jest adres URL: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="b5159-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="b5159-133">Służy on do testowania.</span><span class="sxs-lookup"><span data-stu-id="b5159-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="b5159-134">Krok 2: Konfigurowanie programu exchange oświadczenia interfejsu API RESTful jako profil techniczne w pliku TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b5159-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="b5159-135">Techniczne profil jest pełną konfigurację programu exchange potrzeby z usługą RESTful.</span><span class="sxs-lookup"><span data-stu-id="b5159-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="b5159-136">Otwórz plik TrustFrameworkExtensions.xml i Dodaj następujący fragment kodu XML wewnątrz `<ClaimsProvider>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b5159-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="b5159-137">W poniższych XML dostawcy RESTful `Version=1.0.0.0` jest określane jako protokół.</span><span class="sxs-lookup"><span data-stu-id="b5159-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="b5159-138">Należy wziąć pod uwagę ją jako funkcję, która będzie współpracować z zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="b5159-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="b5159-139">`<InputClaims>` Element definiuje oświadczenia, które będą wysyłane do usługi REST IEF.</span><span class="sxs-lookup"><span data-stu-id="b5159-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="b5159-140">W tym przykładzie zawartość oświadczenia `givenName` będą wysyłane do usługi REST jako oświadczenie `email`.</span><span class="sxs-lookup"><span data-stu-id="b5159-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="b5159-141">`<OutputClaims>` Element definiuje oświadczenia, które IEF będą oczekiwać od usługi REST.</span><span class="sxs-lookup"><span data-stu-id="b5159-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="b5159-142">Niezależnie od liczby oświadczenia, które są odbierane IEF będzie używać tylko te określone w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="b5159-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="b5159-143">W tym przykładzie oświadczenie odebrana jako `city` zostaną zmapowane do IEF oświadczeń o nazwie `city`.</span><span class="sxs-lookup"><span data-stu-id="b5159-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="b5159-144">Krok 3: Dodaj nowe oświadczenie `city` do schematu pliku TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b5159-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="b5159-145">Oświadczenie `city` nie jest jeszcze zdefiniowana dowolne miejsce w naszym schematu.</span><span class="sxs-lookup"><span data-stu-id="b5159-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="b5159-146">Tak, Dodaj definicję wewnątrz elementu `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="b5159-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="b5159-147">Ten element na początku pliku TrustFrameworkExtensions.xml można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="b5159-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="b5159-148">Krok 4: Obejmują wymiana oświadczeń usługi REST aranżacji krok w podróży użytkownika edycji profilu w TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b5159-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="b5159-149">Dodaj krok do podróży profilu użytkownika edycji, po użytkownik został uwierzytelniony (procedura aranżacji 1 – 4 w następujących XML) i użytkownik udostępnił informacje zaktualizowany profil (krok 5).</span><span class="sxs-lookup"><span data-stu-id="b5159-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="b5159-150">Istnieje wiele przypadków użycia, gdy wywołanie interfejsu API REST może służyć jako etap aranżacji.</span><span class="sxs-lookup"><span data-stu-id="b5159-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="b5159-151">Krok aranżacji może służyć jako aktualizacji do systemu zewnętrznego po pomyślnym zakończeniu zadania, takie jak rejestracji po raz pierwszy lub aktualizacji profilu, aby zachować synchronizację informacji.</span><span class="sxs-lookup"><span data-stu-id="b5159-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="b5159-152">W takim przypadku służy rozszerzyć informacje podane w aplikacji po edycji profilu.</span><span class="sxs-lookup"><span data-stu-id="b5159-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="b5159-153">Kopia profilu Edytuj przebieg XML kod użytkownika z pliku TrustFrameworkBase.xml do pliku TrustFrameworkExtensions.xml wewnątrz `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b5159-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="b5159-154">Następnie wprowadź zmiany w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="b5159-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="b5159-155">Jeśli kolejność nie jest zgodna z wersją, upewnij się, Wstaw kod jako kroku przed `ClaimsExchange` typu `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="b5159-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="b5159-156">Końcowe XML podróży użytkownika powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b5159-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="b5159-157">Krok 5: Dodaj oświadczenie `city` Twojego jednostki uzależnionej zasady plików, oświadczenia są wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="b5159-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="b5159-158">Edytuj plik ProfileEdit.xml jednostki uzależnionej strony (RP) i zmodyfikuj `<TechnicalProfile Id="PolicyProfile">` elementu do dodania następujących: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="b5159-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="b5159-159">Po dodaniu nowego oświadczenia profilu techniczna wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b5159-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="b5159-160">Krok 6: Przekazać zmiany i testowanie</span><span class="sxs-lookup"><span data-stu-id="b5159-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="b5159-161">Zastąp istniejące wersje zasad.</span><span class="sxs-lookup"><span data-stu-id="b5159-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="b5159-162">(Opcjonalne:) Zapisz (pobierając) istniejącą wersję pliku rozszerzenia przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="b5159-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="b5159-163">Aby zachować początkowej złożoności niski, firma Microsoft zaleca, nie przekazuj wielu wersji pliku rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b5159-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="b5159-164">(Opcjonalne:) Zmień nazwę nowej wersji identyfikator zasad dla pliku edycji zasad, zmieniając `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="b5159-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="b5159-165">Przekaż plik rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b5159-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="b5159-166">Przekaż plik RP edycji zasady.</span><span class="sxs-lookup"><span data-stu-id="b5159-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="b5159-167">Użyj **Uruchom teraz** do testowania zasad.</span><span class="sxs-lookup"><span data-stu-id="b5159-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="b5159-168">Przejrzyj token, który IEF zwraca do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5159-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="b5159-169">Jeśli wszystko jest poprawnie skonfigurowane, token uwzględni nowe oświadczenie `city`, z wartością `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="b5159-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b5159-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5159-170">Next steps</span></span>

[<span data-ttu-id="b5159-171">Za pośrednictwem interfejsu API REST na potrzeby sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="b5159-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="b5159-172">Modyfikowanie edycji profilu uzyskanie dodatkowych informacji od użytkowników</span><span class="sxs-lookup"><span data-stu-id="b5159-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
