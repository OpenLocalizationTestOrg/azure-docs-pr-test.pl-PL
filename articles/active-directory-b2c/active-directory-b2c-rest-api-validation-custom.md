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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="8b3a8-103">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST usługi Azure AD B2C podróży użytkownika jako sprawdzanie poprawności danych wejściowych użytkownika</span><span class="sxs-lookup"><span data-stu-id="8b3a8-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="8b3a8-104">Witaj Identity Framework środowisko (IEF, Internet Authentication Service), źródłową Azure Active Directory B2C (Azure AD B2C) umożliwia hello tożsamości developer toointegrate interakcji z interfejsu API RESTful w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="8b3a8-105">Na końcu hello tego przewodnika będzie możliwe toocreate podróży użytkownika usługi Azure AD B2C, która współdziała z usług RESTful.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="8b3a8-106">Hello IEF wysyła dane w oświadczeniach i odbiera dane z powrotem w oświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="8b3a8-107">Witaj interakcji z hello interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="8b3a8-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="8b3a8-108">Może być zaprojektowana jako exchange oświadczenia interfejsu API REST lub profil sprawdzania poprawności, które odbywa się w kroku aranżacji.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="8b3a8-109">Zwykle sprawdza poprawność danych wejściowych od użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-109">Typically validates input from hello user.</span></span> <span data-ttu-id="8b3a8-110">W przypadku odrzucenia wartość powitania od użytkownika hello użytkownika hello spróbować ponownie tooenter prawidłową wartość z hello możliwości tooreturn komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="8b3a8-111">Można również projektować interakcji hello krok aranżacji.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="8b3a8-112">Aby uzyskać więcej informacji, zobacz [wskazówki: integrowanie interfejsu API REST oświadczeń wymiany w podróży użytkownika usługi Azure AD B2C krok aranżacji](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8b3a8-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="8b3a8-113">Na przykład profilu weryfikacji hello użyjemy przebieg użytkownika edycji profilu hello w pliku pakietu starter hello ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="8b3a8-114">Możemy zweryfikować tę nazwę hello, podana przez użytkownika hello w profilu hello Edycja nie jest częścią listy wykluczeń.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b3a8-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b3a8-115">Prerequisites</span></span>

- <span data-ttu-id="8b3a8-116">Toocomplete skonfigurowany dzierżawy usługi Azure AD B2C konta lokalnego konta-konta/logowania, zgodnie z opisem w [wprowadzenie](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8b3a8-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="8b3a8-117">Toointeract punkt końcowy interfejsu API REST z.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="8b3a8-118">W ramach tego przewodnika skonfigurowaliśmy pokaz lokacji o nazwie [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) za pomocą usługi interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="8b3a8-119">Krok 1: Przygotowanie hello funkcji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="8b3a8-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="8b3a8-120">Instalator funkcji interfejsu API REST jest poza zakres tego artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="8b3a8-121">[Środowisko Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) zapewnia doskonałą toolkit toocreate RESTful usług w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="8b3a8-122">Utworzyliśmy Azure funkcja, która otrzymuje oświadczenia, że klient oczekuje jako `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="8b3a8-123">Funkcja Hello sprawdza, czy istnieje tego oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="8b3a8-124">Dostęp można uzyskać kod pełną funkcji Azure hello w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="8b3a8-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="8b3a8-125">Witaj IEF oczekuje hello `userMessage` oświadczeń zwraca tego hello Azure funkcji.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="8b3a8-126">To oświadczenie zostanie wyświetlone jako użytkownik toohello ciągu w przypadku niepowodzenia weryfikacji hello, np. gdy 409 Konflikt stanu jest zwracany w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="8b3a8-127">Krok 2: Skonfiguruj hello interfejsu API RESTful oświadczeń w programie exchange jako profil techniczne w pliku TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8b3a8-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="8b3a8-128">Techniczne profil jest hello pełnej konfiguracji programu exchange hello potrzeby z hello usługi RESTful.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="8b3a8-129">Otwórz plik TrustFrameworkExtensions.xml hello i dodaj następujące fragment kodu XML wewnątrz hello hello `<ClaimsProviders>` elementu.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="8b3a8-130">W powitania po XML, dostawca RESTful `Version=1.0.0.0` jest określane jako hello protokołu.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="8b3a8-131">Należy wziąć pod uwagę ją jako funkcję hello, który będzie wchodzić w interakcje hello zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="8b3a8-132">Witaj `InputClaims` element definiuje hello oświadczenia, które będą wysyłane hello IEF toohello REST usługi.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="8b3a8-133">W tym przykładzie hello zawartość oświadczenia hello `givenName` będą wysyłane usługi REST toohello jako `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="8b3a8-134">W tym przykładzie powitalne IEF nie oczekuje oświadczeń ponownie.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="8b3a8-135">Zamiast tego czeka na odpowiedź z usługi REST hello i czynności na podstawie kodów stanu hello, które otrzymuje.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="8b3a8-136">Krok 3: Dołącz wymiana oświadczeń usługi RESTful hello własnym potwierdzona profilu techniczne miejscu dane wejściowe użytkownika hello toovalidate</span><span class="sxs-lookup"><span data-stu-id="8b3a8-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="8b3a8-137">najbardziej popularnym zastosowaniem Hello hello sprawdzania poprawności kroku jest hello interakcji z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="8b3a8-138">Wszystkie interakcje gdzie użytkownik hello jest oczekiwany tooprovide dane wejściowe są *własnym potwierdzone techniczne profile*.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="8b3a8-139">W tym przykładzie dodamy hello weryfikacji toohello niezależne Asserted ProfileUpdate techniczne profilu.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="8b3a8-140">Jest hello profil technicznych, który hello jednostki uzależnionej pliku zasad firmy (RP) `Profile Edit` używa.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="8b3a8-141">tooadd hello oświadczeń exchange toohello własnym potwierdzone profilu techniczne:</span><span class="sxs-lookup"><span data-stu-id="8b3a8-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="8b3a8-142">Otwórz plik TrustFrameworkBase.xml hello i wyszukaj `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="8b3a8-143">Przejrzyj konfigurację hello techniczne profilu.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="8b3a8-144">Sprawdź, jak exchange hello z użytkownikiem hello jest zdefiniowany jako oświadczenia, które będą proszeni hello użytkownika (oświadczenia wejściowe) i oświadczenia, które oczekuje się wstecz od dostawcy własnym potwierdzona hello (dane wyjściowe oświadczenia).</span><span class="sxs-lookup"><span data-stu-id="8b3a8-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="8b3a8-145">Wyszukaj `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`i zwróć uwagę, że ten profil jest wywoływany jako orchestration punkcie 6 `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="8b3a8-146">Krok 4: Przekaż i testowania pliku zasad hello profilu edycji planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="8b3a8-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="8b3a8-147">Przekaż nową wersję pliku TrustFrameworkExtensions.xml hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="8b3a8-148">Użyj **Uruchom teraz** tootest hello profilu Edytuj plik zasad planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="8b3a8-149">Testowanie poprawności hello udostępniając jedno z istniejącymi nazwami hello (na przykład mcvinny) w hello **imię** pola.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="8b3a8-150">Jeśli wszystko jest poprawnie skonfigurowane, powinien zostać wyświetlony komunikat, który powiadamia użytkownika hello hello player tag jest już używana.</span><span class="sxs-lookup"><span data-stu-id="8b3a8-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b3a8-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8b3a8-151">Next steps</span></span>

[<span data-ttu-id="8b3a8-152">Modyfikowanie hello profilu edycji i użytkownika rejestracji toogather dodatkowych informacji od użytkowników</span><span class="sxs-lookup"><span data-stu-id="8b3a8-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="8b3a8-153">Wskazówki: Integrowanie wymiany oświadczenia interfejsu API REST w podróży użytkownika usługi Azure AD B2C krok aranżacji</span><span class="sxs-lookup"><span data-stu-id="8b3a8-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
