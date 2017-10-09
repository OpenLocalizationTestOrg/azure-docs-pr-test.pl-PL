---
title: "Usługa Azure Active Directory B2C: Dodawanie dostawcy usługi Azure AD za pomocą niestandardowych zasad | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o zasadach niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="2bf37-103">Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bf37-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2bf37-104">W tym artykule opisano sposób tooenable logowania użytkowników z określonych organizacji usługi Azure Active Directory (Azure AD) przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2bf37-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bf37-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2bf37-105">Prerequisites</span></span>

<span data-ttu-id="2bf37-106">Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bf37-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="2bf37-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="2bf37-107">These steps include:</span></span>

1. <span data-ttu-id="2bf37-108">Tworzenie usługi Azure Active Directory B2C dzierżawy (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="2bf37-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="2bf37-109">Tworzenie aplikacji usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2bf37-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="2bf37-110">Rejestrowanie dwie aplikacje aparat zasad.</span><span class="sxs-lookup"><span data-stu-id="2bf37-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="2bf37-111">Konfigurowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="2bf37-111">Setting up keys.</span></span>
5. <span data-ttu-id="2bf37-112">Konfigurowanie hello początkowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="2bf37-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="2bf37-113">Utwórz aplikację usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bf37-113">Create an Azure AD app</span></span>

<span data-ttu-id="2bf37-114">tooenable logowania użytkowników z określonej usługi Azure AD w organizacji, należy tooregister aplikacji w ramach dzierżawy hello Azure AD w organizacji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="2bf37-115">Używamy "contoso.com" dla dzierżawcy hello organizacyjnego usługi Azure AD i "fabrikamb2c.onmicrosoft.com" jako dzierżawy hello Azure AD B2C w hello, postępując zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="2bf37-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="2bf37-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2bf37-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2bf37-117">Na górnym pasku hello wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="2bf37-117">On hello top bar, select your account.</span></span> <span data-ttu-id="2bf37-118">Z hello **katalogu** wybierz dzierżawy hello Azure AD w organizacji, w którym ma tooregister aplikacji (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="2bf37-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="2bf37-119">Wybierz **więcej usług** w okienku po lewej stronie powitania i wyszukaj "Rejestracji aplikacji".</span><span class="sxs-lookup"><span data-stu-id="2bf37-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="2bf37-120">Wybierz **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="2bf37-121">Wprowadź nazwę dla aplikacji (na przykład `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="2bf37-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="2bf37-122">Wybierz **aplikacji sieci Web / interfejs API** hello typu aplikacja.</span><span class="sxs-lookup"><span data-stu-id="2bf37-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="2bf37-123">Dla **adres URL logowania**, wprowadź hello następującego adresu URL, gdzie `yourtenant` zastępuje nazwę hello dzierżawy usługi Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="2bf37-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="2bf37-124">Zapisz identyfikator hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-124">Save hello application ID.</span></span>
1. <span data-ttu-id="2bf37-125">Wybierz nowo utworzony hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="2bf37-126">W obszarze hello **ustawienia** bloku, wybierz opcję **klucze**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="2bf37-127">Utwórz nowy klucz i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="2bf37-127">Create a new key, and save it.</span></span> <span data-ttu-id="2bf37-128">W krokach hello w następnej sekcji hello będą używać go.</span><span class="sxs-lookup"><span data-stu-id="2bf37-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="2bf37-129">Dodawanie klucza tooAzure hello Azure AD AD B2C</span><span class="sxs-lookup"><span data-stu-id="2bf37-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="2bf37-130">Należy klucz aplikacji contoso.com hello toostore w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2bf37-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="2bf37-131">toodo to:</span><span class="sxs-lookup"><span data-stu-id="2bf37-131">toodo this:</span></span>
1. <span data-ttu-id="2bf37-132">Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości** > **zasad kluczy**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="2bf37-133">Wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-133">Select **+Add**.</span></span>
1. <span data-ttu-id="2bf37-134">Wybierz lub wprowadź następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="2bf37-134">Select or enter these options:</span></span>
   * <span data-ttu-id="2bf37-135">Wybierz **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-135">Select **Manual**.</span></span>
   * <span data-ttu-id="2bf37-136">Aby uzyskać **nazwa**, wybierz nazwę, która odpowiada nazwa dzierżawy usługi Azure AD (na przykład `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="2bf37-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="2bf37-137">Prefiks Hello `B2C_1A_` zostanie automatycznie dodana nazwę toohello klucza.</span><span class="sxs-lookup"><span data-stu-id="2bf37-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="2bf37-138">Wklej klucz aplikacji hello **klucz tajny** pole.</span><span class="sxs-lookup"><span data-stu-id="2bf37-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="2bf37-139">Wybierz **podpisu**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-139">Select **Signature**.</span></span>
1. <span data-ttu-id="2bf37-140">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-140">Select **Create**.</span></span>
1. <span data-ttu-id="2bf37-141">Upewnij się, że utworzono klucz hello `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="2bf37-142">Dodawanie dostawcy oświadczeń w zasadach podstawowej</span><span class="sxs-lookup"><span data-stu-id="2bf37-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="2bf37-143">Jeśli chcesz toosign użytkowników za pomocą usługi Azure AD, należy toodefine usługi Azure AD jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2bf37-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="2bf37-144">Innymi słowy należy toospecify punktu końcowego usługi Azure AD B2C będzie komunikować się z.</span><span class="sxs-lookup"><span data-stu-id="2bf37-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="2bf37-145">punkt końcowy Hello zapewni zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2bf37-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="2bf37-146">Można zdefiniować usługi Azure AD jako dostawcy oświadczeń, dodając toohello usługi Azure AD `<ClaimsProvider>` węzeł w hello rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="2bf37-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="2bf37-147">Otwórz plik rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="2bf37-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="2bf37-148">Znajdź hello `<ClaimsProviders>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="2bf37-149">Jeśli nie istnieje, dodaj ją w obszarze węzła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="2bf37-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="2bf37-150">Dodaj nową `<ClaimsProvider>` węzła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2bf37-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. <span data-ttu-id="2bf37-151">W obszarze hello `<ClaimsProvider>` węzła, wartość hello aktualizacji `<Domain>` tooa unikatową wartość, które mogą być używane toodistinguish go od innych dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2bf37-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="2bf37-152">W obszarze hello `<ClaimsProvider>` węzła, wartość hello aktualizacji `<DisplayName>` tooa przyjazną nazwę hello dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2bf37-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="2bf37-153">Ta wartość nie jest obecnie używana.</span><span class="sxs-lookup"><span data-stu-id="2bf37-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="2bf37-154">Aktualizuj profil techniczne hello</span><span class="sxs-lookup"><span data-stu-id="2bf37-154">Update hello technical profile</span></span>

<span data-ttu-id="2bf37-155">tooget tokenu z punktu końcowego usługi Azure AD hello należy protokołów hello toodefine usługi Azure AD B2C należy używać toocommunicate z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bf37-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="2bf37-156">Jest to realizowane wewnątrz hello `<TechnicalProfile>` elementu `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="2bf37-157">Aktualizacja Identyfikatora hello hello `<TechnicalProfile>` węzła.</span><span class="sxs-lookup"><span data-stu-id="2bf37-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="2bf37-158">Ten identyfikator jest używane toorefer toothis techniczne profil z innymi częściami hello zasad.</span><span class="sxs-lookup"><span data-stu-id="2bf37-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="2bf37-159">Zaktualizuj wartość hello `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="2bf37-160">Ta wartość będzie wyświetlana na powitania przycisk Zarejestruj się na ekranie logowania.</span><span class="sxs-lookup"><span data-stu-id="2bf37-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="2bf37-161">Zaktualizuj wartość hello `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="2bf37-162">Protokołu OpenID Connect hello używa usługi Azure AD, dlatego upewnij się, ta wartość hello dla `<Protocol>` jest `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="2bf37-163">Należy tooupdate hello `<Metadata>` sekcji w pliku XML hello określonego tooearlier tooreflect hello konfigurację ustawień dla konkretnej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bf37-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="2bf37-164">W pliku XML hello zaktualizuj wartości metadanych hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2bf37-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="2bf37-165">Ustaw `<Item Key="METADATA">` za`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, gdzie `yourAzureADtenant` jest nazwa dzierżawy usługi Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="2bf37-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="2bf37-166">Otwórz toohello Twojego przeglądarki, a następnie przejść `METADATA` adres URL, które zostało zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="2bf37-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="2bf37-167">W przeglądarce hello wyszukiwania dla obiektu "Wystawca" hello i skopiuj jej wartość.</span><span class="sxs-lookup"><span data-stu-id="2bf37-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="2bf37-168">Powinien wyglądać podobnie jak poniżej hello: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="2bf37-169">Wklej wartość hello `<Item Key="ProviderName">` hello pliku XML.</span><span class="sxs-lookup"><span data-stu-id="2bf37-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="2bf37-170">Ustaw `<Item Key="client_id">` toohello identyfikator aplikacji hello rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="2bf37-171">Ustaw `<Item Key="IdTokenAudience">` toohello identyfikator aplikacji hello rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="2bf37-172">Upewnij się, że `<Item Key="response_types">` ustawiono zbyt`id_token`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="2bf37-173">Upewnij się, że `<Item Key="UsePolicyInRedirectUri">` ustawiono zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="2bf37-174">Należy również hasło hello Azure AD toolink zarejestrowanych w Twojej usługi Azure AD B2C toohello dzierżawy usługi Azure AD `<ClaimsProvider>` informacji:</span><span class="sxs-lookup"><span data-stu-id="2bf37-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="2bf37-175">W hello `<CryptographicKeys>` sekcji hello poprzedzających pliku XML, zaktualizuj wartość hello `StorageReferenceId` toohello Identyfikator odwołania hello klucz tajny, który zdefiniowano (na przykład `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="2bf37-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="2bf37-176">Przekaż plik rozszerzenia hello do weryfikacji</span><span class="sxs-lookup"><span data-stu-id="2bf37-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="2bf37-177">Chwili skonfigurowano zasad, aby usługi Azure AD B2C znała jak toocommunicate z katalogiem Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bf37-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="2bf37-178">Spróbuj przekazać plik rozszerzenia hello z Twojej tooconfirm tylko zasady czy problemów nie ma do tej pory.</span><span class="sxs-lookup"><span data-stu-id="2bf37-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="2bf37-179">toodo tak:</span><span class="sxs-lookup"><span data-stu-id="2bf37-179">toodo so:</span></span>

1. <span data-ttu-id="2bf37-180">Otwórz hello **wszystkie zasady** bloku w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2bf37-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="2bf37-181">Sprawdź hello **zastąpić hello zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="2bf37-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="2bf37-182">Przekaż plik rozszerzenia hello (TrustFrameworkExtensions.xml) i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2bf37-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="2bf37-183">Zarejestruj hello Azure AD oświadczeń dostawcy tooa użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="2bf37-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="2bf37-184">Teraz należy tooadd tooone dostawcy tożsamości usługi Azure AD hello podróży z użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2bf37-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="2bf37-185">W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym hello konta-konta/logowania ekranów.</span><span class="sxs-lookup"><span data-stu-id="2bf37-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="2bf37-186">toomake dostępne, firma Microsoft utworzy duplikatem istniejącej przebieg użytkownika szablonu i następnie zmodyfikować go, aby miała ona również dostawcy tożsamości hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2bf37-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="2bf37-187">Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="2bf37-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="2bf37-188">Znajdź hello `<UserJourneys>` hello elementu i skopiuj cały `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="2bf37-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="2bf37-189">Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="2bf37-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2bf37-190">Jeśli hello element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="2bf37-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="2bf37-191">Wklej hello cały `<UserJourney>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="2bf37-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="2bf37-192">Zmień nazwę Identyfikatora hello hello nowego użytkownika podróży (na przykład zmienić nazwę jako `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="2bf37-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2bf37-193">Wyświetl hello "button"</span><span class="sxs-lookup"><span data-stu-id="2bf37-193">Display hello "button"</span></span>

<span data-ttu-id="2bf37-194">Witaj `<ClaimsProviderSelection>` element jest przycisk dostawcy tożsamości analogiczne tooan na ekranie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="2bf37-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="2bf37-195">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla usługi Azure AD, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2bf37-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="2bf37-196">tooadd tego elementu:</span><span class="sxs-lookup"><span data-stu-id="2bf37-196">tooadd this element:</span></span>

1. <span data-ttu-id="2bf37-197">Znajdź hello `<OrchestrationStep>` węzła, który zawiera `Order="1"` w podróży użytkownika hello, który został właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="2bf37-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="2bf37-198">Dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2bf37-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="2bf37-199">Ustaw `TargetClaimsExchangeId` tooan odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="2bf37-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="2bf37-200">Zaleca się następujące hello sam Konwencji jako inne:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="2bf37-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2bf37-201">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="2bf37-201">Link hello button tooan action</span></span>

<span data-ttu-id="2bf37-202">Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji.</span><span class="sxs-lookup"><span data-stu-id="2bf37-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="2bf37-203">Akcja Hello jest dla usługi Azure AD B2C toocommunicate z usługi Azure AD tooreceive w takim przypadku tokenu.</span><span class="sxs-lookup"><span data-stu-id="2bf37-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="2bf37-204">Łącze hello tooan Akcja przycisku przez łączenie hello techniczne profilu dla dostawcy oświadczeń usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2bf37-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="2bf37-205">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="2bf37-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="2bf37-206">Dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2bf37-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="2bf37-207">Aktualizacja `Id` toohello samą wartość jak `TargetClaimsExchangeId` w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="2bf37-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="2bf37-208">Aktualizacja `TechnicalProfileReferenceId` toohello identyfikator hello techniczne profilu utworzonego wcześniej (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="2bf37-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="2bf37-209">Przekaż hello zaktualizowane rozszerzenie pliku</span><span class="sxs-lookup"><span data-stu-id="2bf37-209">Upload hello updated extension file</span></span>

<span data-ttu-id="2bf37-210">Po zakończeniu modyfikowania hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="2bf37-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="2bf37-211">Zapisz go.</span><span class="sxs-lookup"><span data-stu-id="2bf37-211">Save it.</span></span> <span data-ttu-id="2bf37-212">Następnie przekaż plik hello i upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="2bf37-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="2bf37-213">Zaktualizuj plik RP hello</span><span class="sxs-lookup"><span data-stu-id="2bf37-213">Update hello RP file</span></span>

<span data-ttu-id="2bf37-214">Teraz należy tooupdate hello jednostki uzależnionej strony (RP) pliku, który inicjuje przebieg użytkownika hello, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="2bf37-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="2bf37-215">Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym i zmień jego nazwę (na przykład, zmień jego nazwę tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="2bf37-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="2bf37-216">Nowy plik i aktualizacji hello hello Otwórz `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` unikatowe wartości (na przykład SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="2bf37-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="2bf37-217">To będzie nazwa hello zasad (na przykład B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="2bf37-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="2bf37-218">Modyfikowanie hello `ReferenceId` atrybutu w `<DefaultUserJourney>` toomatch identyfikator hello hello nowy przebieg użytkownika utworzony (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="2bf37-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="2bf37-219">Zapisz zmiany i przekaż plik hello.</span><span class="sxs-lookup"><span data-stu-id="2bf37-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2bf37-220">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="2bf37-220">Troubleshooting</span></span>

<span data-ttu-id="2bf37-221">Testowanie hello niestandardowych zasad, które przekazanym właśnie otwierając jego bloku i klikając pozycję **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="2bf37-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="2bf37-222">toodiagnose problemów, przeczytaj o [Rozwiązywanie problemów z](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2bf37-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bf37-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bf37-223">Next steps</span></span>

<span data-ttu-id="2bf37-224">Wyrazić swoją opinię za[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2bf37-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
