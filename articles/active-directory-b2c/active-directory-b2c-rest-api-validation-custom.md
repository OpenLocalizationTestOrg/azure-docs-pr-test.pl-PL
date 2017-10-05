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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="4215f-103">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST usługi Azure AD B2C podróży użytkownika jako sprawdzanie poprawności danych wejściowych użytkownika</span><span class="sxs-lookup"><span data-stu-id="4215f-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="4215f-104">Tożsamość środowiska Framework (IEF) źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia deweloperowi tożsamości integracji interakcji z interfejsu API RESTful w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4215f-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="4215f-105">Na końcu tego przewodnika można utworzyć przebieg użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.</span><span class="sxs-lookup"><span data-stu-id="4215f-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="4215f-106">IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="4215f-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="4215f-107">Interakcja z interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="4215f-107">The interaction with the API:</span></span>

- <span data-ttu-id="4215f-108">Może być zaprojektowana jako exchange oświadczenia interfejsu API REST lub profil sprawdzania poprawności, które odbywa się w kroku aranżacji.</span><span class="sxs-lookup"><span data-stu-id="4215f-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="4215f-109">Zwykle sprawdza poprawność danych wejściowych od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4215f-109">Typically validates input from the user.</span></span> <span data-ttu-id="4215f-110">W przypadku odrzucenia wartość od użytkownika, użytkownik spróbować ponownie wprowadź prawidłową wartość możliwość zwraca komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4215f-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="4215f-111">Można również projektować interakcji krok aranżacji.</span><span class="sxs-lookup"><span data-stu-id="4215f-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="4215f-112">Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C krok aranżacji](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="4215f-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="4215f-113">Na przykład profil sprawdzania poprawności użyjemy podróży profilu użytkownika edycji w pliku pakietu starter ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="4215f-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="4215f-114">Możemy zweryfikować, że nazwa podana przez użytkownika w edycji profilu nie jest częścią listy wykluczeń.</span><span class="sxs-lookup"><span data-stu-id="4215f-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4215f-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4215f-115">Prerequisites</span></span>

- <span data-ttu-id="4215f-116">Dzierżawy usługi Azure AD B2C, skonfigurowany tak, aby ukończyć konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="4215f-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="4215f-117">Punkt końcowy interfejsu API REST do interakcji z.</span><span class="sxs-lookup"><span data-stu-id="4215f-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="4215f-118">W ramach tego przewodnika skonfigurowaliśmy pokaz lokacji o nazwie [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) za pomocą usługi interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4215f-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="4215f-119">Krok 1: Przygotowanie funkcji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="4215f-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="4215f-120">Instalator funkcji interfejsu API REST jest poza zakres tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4215f-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="4215f-121">[Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą zestawu narzędzi do tworzenia usługi RESTful w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4215f-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="4215f-122">Utworzyliśmy Azure funkcja, która otrzymuje oświadczenia, że klient oczekuje jako `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="4215f-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="4215f-123">Funkcja weryfikuje, czy istnieje tego oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="4215f-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="4215f-124">Dostęp można uzyskać kod pełną funkcji platformy Azure w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="4215f-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="4215f-125">Oczekuje IEF `userMessage` oświadczenie, które zwraca funkcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4215f-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="4215f-126">To oświadczenie zostanie wyświetlone jako ciąg do użytkownika w przypadku niepowodzenia weryfikacji, na przykład gdy stan 409 Konflikt są zwracane w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4215f-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="4215f-127">Krok 2: Konfigurowanie programu exchange oświadczenia interfejsu API RESTful jako profil techniczne w pliku TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="4215f-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="4215f-128">Techniczne profil jest pełną konfigurację programu exchange potrzeby z usługą RESTful.</span><span class="sxs-lookup"><span data-stu-id="4215f-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="4215f-129">Otwórz plik TrustFrameworkExtensions.xml i Dodaj następujący fragment kodu XML wewnątrz `<ClaimsProviders>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4215f-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="4215f-130">W poniższych XML dostawcy RESTful `Version=1.0.0.0` jest określane jako protokół.</span><span class="sxs-lookup"><span data-stu-id="4215f-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="4215f-131">Należy wziąć pod uwagę ją jako funkcję, która będzie współpracować z zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="4215f-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="4215f-132">`InputClaims` Element definiuje oświadczenia, które będą wysyłane do usługi REST IEF.</span><span class="sxs-lookup"><span data-stu-id="4215f-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="4215f-133">W tym przykładzie zawartość oświadczenia `givenName` będą wysyłane do usługi REST jako `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="4215f-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="4215f-134">W tym przykładzie IEF nie oczekuje oświadczeń z powrotem.</span><span class="sxs-lookup"><span data-stu-id="4215f-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="4215f-135">Zamiast tego czeka na odpowiedź z usługi REST i działania na podstawie kodów stanu, które otrzymuje.</span><span class="sxs-lookup"><span data-stu-id="4215f-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="4215f-136">Krok 3: Dołącz exchange oświadczeń usługi RESTful własnym potwierdzona profilu techniczne której chcesz sprawdzić poprawność danych wejściowych użytkownika</span><span class="sxs-lookup"><span data-stu-id="4215f-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="4215f-137">Najczęściej kroku walidacji jest w interakcji z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="4215f-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="4215f-138">Wszystkie interakcje, gdy użytkownik powinien zapewniać dane wejściowe są *własnym potwierdzone techniczne profile*.</span><span class="sxs-lookup"><span data-stu-id="4215f-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="4215f-139">W tym przykładzie dodamy weryfikacji do profilu techniczne niezależne Asserted ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="4215f-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="4215f-140">Jest to techniczne profil, który pliku zasad jednostki uzależnionej strony (RP) `Profile Edit` używa.</span><span class="sxs-lookup"><span data-stu-id="4215f-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="4215f-141">Aby dodać exchange oświadczenia do własnym potwierdzona profilu techniczne:</span><span class="sxs-lookup"><span data-stu-id="4215f-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="4215f-142">Otwórz plik TrustFrameworkBase.xml i wyszukaj `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="4215f-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="4215f-143">Sprawdź konfigurację tego profilu technicznych.</span><span class="sxs-lookup"><span data-stu-id="4215f-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="4215f-144">Sprawdź, jak zdefiniowano jako oświadczenia, które będą proszeni użytkownika (oświadczenia wejściowe) i oświadczenia, które będzie można oczekiwać od dostawcy własnym potwierdzona (oświadczeń wyjściowych) programu exchange z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="4215f-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="4215f-145">Wyszukaj `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`i zwróć uwagę, że ten profil jest wywoływany jako orchestration punkcie 6 `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="4215f-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="4215f-146">Krok 4: Przekaż i przetestować plik zasad RP edycji profilu</span><span class="sxs-lookup"><span data-stu-id="4215f-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="4215f-147">Przekaż nową wersję pliku TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="4215f-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="4215f-148">Użyj **Uruchom teraz** do testowania pliku zasad RP edycji profilu.</span><span class="sxs-lookup"><span data-stu-id="4215f-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="4215f-149">Testowanie weryfikacji udostępniając jedno z istniejących nazw (na przykład mcvinny) w **imię** pola.</span><span class="sxs-lookup"><span data-stu-id="4215f-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="4215f-150">Jeśli wszystko jest poprawnie skonfigurowane, powinien zostać wyświetlony komunikat, który powiadamia użytkownika player tag jest już używana.</span><span class="sxs-lookup"><span data-stu-id="4215f-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4215f-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4215f-151">Next steps</span></span>

[<span data-ttu-id="4215f-152">Modyfikowanie profilu rejestracji edycji i użytkownika uzyskanie dodatkowych informacji od użytkowników</span><span class="sxs-lookup"><span data-stu-id="4215f-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="4215f-153">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji</span><span class="sxs-lookup"><span data-stu-id="4215f-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
