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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="ebcdd-103">Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebcdd-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ebcdd-104">W tym artykule przedstawiono sposób włączenia logowania użytkowników z określonych organizacji usługi Azure Active Directory (Azure AD) za pośrednictwem [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebcdd-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ebcdd-105">Prerequisites</span></span>

<span data-ttu-id="ebcdd-106">Wykonaj kroki [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="ebcdd-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-107">These steps include:</span></span>

1. <span data-ttu-id="ebcdd-108">Tworzenie usługi Azure Active Directory B2C dzierżawy (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="ebcdd-109">Tworzenie aplikacji usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="ebcdd-110">Rejestrowanie dwie aplikacje aparat zasad.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="ebcdd-111">Konfigurowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-111">Setting up keys.</span></span>
5. <span data-ttu-id="ebcdd-112">Ustawianie początkowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="ebcdd-113">Utwórz aplikację usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebcdd-113">Create an Azure AD app</span></span>

<span data-ttu-id="ebcdd-114">Aby włączyć logowanie użytkowników z określonej usługi Azure AD w organizacji, należy zarejestrować aplikację w organizacyjnej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="ebcdd-115">Używamy "contoso.com" dla organizacji dzierżawy usługi Azure AD i "fabrikamb2c.onmicrosoft.com" jako dzierżawy usługi Azure AD B2C w poniższych instrukcjach.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="ebcdd-116">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="ebcdd-117">Na górnym pasku wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-117">On the top bar, select your account.</span></span> <span data-ttu-id="ebcdd-118">Z **katalogu** wybierz organizacyjnej dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="ebcdd-119">Wybierz **więcej usług** w okienku po lewej stronie, a następnie wyszukaj "Rejestracji aplikacji".</span><span class="sxs-lookup"><span data-stu-id="ebcdd-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="ebcdd-120">Wybierz **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="ebcdd-121">Wprowadź nazwę dla aplikacji (na przykład `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="ebcdd-122">Wybierz **aplikacji sieci Web / interfejs API** typu aplikacja.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="ebcdd-123">Aby uzyskać **adres URL logowania**, wprowadź następujący adres URL, gdzie `yourtenant` zastępuje nazwę dzierżawy usługi Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="ebcdd-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="ebcdd-124">Zapisz identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-124">Save the application ID.</span></span>
1. <span data-ttu-id="ebcdd-125">Wybierz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-125">Select the newly created application.</span></span>
1. <span data-ttu-id="ebcdd-126">W obszarze **ustawienia** bloku, wybierz opcję **klucze**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="ebcdd-127">Utwórz nowy klucz i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-127">Create a new key, and save it.</span></span> <span data-ttu-id="ebcdd-128">Zostanie użyty w krokach w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="ebcdd-129">Dodawanie klucza usługi Azure AD do usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ebcdd-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="ebcdd-130">Wystarczy przechowywać klucz aplikacji contoso.com w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="ebcdd-131">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-131">To do this:</span></span>
1. <span data-ttu-id="ebcdd-132">Przejdź do dzierżawy usługi Azure AD B2C i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości** > **klucze zasad**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="ebcdd-133">Wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-133">Select **+Add**.</span></span>
1. <span data-ttu-id="ebcdd-134">Wybierz lub wprowadź następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-134">Select or enter these options:</span></span>
   * <span data-ttu-id="ebcdd-135">Wybierz **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-135">Select **Manual**.</span></span>
   * <span data-ttu-id="ebcdd-136">Aby uzyskać **nazwa**, wybierz nazwę, która odpowiada nazwa dzierżawy usługi Azure AD (na przykład `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="ebcdd-137">Prefiks `B2C_1A_` jest automatycznie dodawany do nazwy klucza.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="ebcdd-138">Wklej swój klucz aplikacji w **klucz tajny** pole.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="ebcdd-139">Wybierz **podpisu**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-139">Select **Signature**.</span></span>
1. <span data-ttu-id="ebcdd-140">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-140">Select **Create**.</span></span>
1. <span data-ttu-id="ebcdd-141">Upewnij się, że utworzono klucz `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="ebcdd-142">Dodawanie dostawcy oświadczeń w zasadach podstawowej</span><span class="sxs-lookup"><span data-stu-id="ebcdd-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="ebcdd-143">Użytkownikom na logowanie się przy użyciu usługi Azure AD, należy zdefiniować usługi Azure AD jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="ebcdd-144">Innymi słowy należy określić punkt końcowy usługi Azure AD B2C będzie komunikować się z.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="ebcdd-145">Punkt końcowy udostępni zestaw oświadczeń, które są używane przez usługę Azure AD B2C, aby sprawdzić, czy określony użytkownik jest uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="ebcdd-146">Można zdefiniować usługi Azure AD jako dostawcy oświadczeń, przez dodanie usługi Azure AD do `<ClaimsProvider>` węzeł w pliku rozszerzenie zasad:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="ebcdd-147">Otwórz plik rozszerzenia (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="ebcdd-148">Znajdź `<ClaimsProviders>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="ebcdd-149">Jeśli nie istnieje, dodaj ją w obszarze węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="ebcdd-150">Dodaj nową `<ClaimsProvider>` węzła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="ebcdd-151">W obszarze `<ClaimsProvider>` węzła, zaktualizuj wartość `<Domain>` do unikatową wartość, która może służyć do odróżnienia go od innych dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="ebcdd-152">W obszarze `<ClaimsProvider>` węzła, zaktualizuj wartość `<DisplayName>` przyjazną nazwę dla dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="ebcdd-153">Ta wartość nie jest obecnie używana.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="ebcdd-154">Aktualizuj profil techniczne</span><span class="sxs-lookup"><span data-stu-id="ebcdd-154">Update the technical profile</span></span>

<span data-ttu-id="ebcdd-155">Aby uzyskać token z punktem końcowym usługi Azure AD, musisz zdefiniować protokołów, które usługi Azure AD B2C należy używać do komunikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="ebcdd-156">Jest to realizowane wewnątrz `<TechnicalProfile>` elementu `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="ebcdd-157">Aktualizacja Identyfikatora `<TechnicalProfile>` węzła.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="ebcdd-158">Ten identyfikator służy do odwoływania się do tego profilu techniczne z innymi częściami zasad.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="ebcdd-159">Zaktualizuj wartość `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="ebcdd-160">Ta wartość będzie wyświetlana na przycisk logowania na ekranie logowania.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="ebcdd-161">Zaktualizuj wartość `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="ebcdd-162">Usługi Azure AD używa protokołu OpenID Connect, dlatego upewnij się, że wartość `<Protocol>` jest `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="ebcdd-163">Musisz zaktualizować `<Metadata>` sekcji w pliku XML określonego wcześniej aby odzwierciedlić ustawień konfiguracyjnych dla konkretnej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="ebcdd-164">W pliku XML zaktualizuj wartości metadanych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="ebcdd-165">Ustaw `<Item Key="METADATA">` do `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, gdzie `yourAzureADtenant` jest nazwa dzierżawy usługi Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="ebcdd-166">Otwórz przeglądarkę i przejdź do `METADATA` adres URL, które zostało zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="ebcdd-167">W przeglądarce wyszukaj obiekt "Wystawca" i skopiuj jej wartość.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="ebcdd-168">Powinien wyglądać podobnie do następującej: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="ebcdd-169">Wklej wartość `<Item Key="ProviderName">` w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="ebcdd-170">Ustaw `<Item Key="client_id">` do Identyfikatora aplikacji z rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="ebcdd-171">Ustaw `<Item Key="IdTokenAudience">` do Identyfikatora aplikacji z rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="ebcdd-172">Upewnij się, że `<Item Key="response_types">` ma ustawioną wartość `id_token`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="ebcdd-173">Upewnij się, że `<Item Key="UsePolicyInRedirectUri">` ma ustawioną wartość `false`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="ebcdd-174">Musisz także połączyć klucz tajny usługi Azure AD, który został zarejestrowany w dzierżawie usługi Azure AD B2C do usługi Azure AD `<ClaimsProvider>` informacji:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="ebcdd-175">W `<CryptographicKeys>` sekcji w poprzednim pliku XML, zaktualizuj wartość `StorageReferenceId` Identyfikator odwołania klucz tajny, który zdefiniowano (na przykład `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="ebcdd-176">Przekaż plik rozszerzenia do weryfikacji</span><span class="sxs-lookup"><span data-stu-id="ebcdd-176">Upload the extension file for verification</span></span>

<span data-ttu-id="ebcdd-177">Przez teraz zgodnie z zasadami został skonfigurowany tak, aby usługi Azure AD B2C potrafi do komunikowania się z katalogiem Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="ebcdd-178">Spróbuj przekazać plik rozszerzenia zasad tylko w celu potwierdzenia, że wszystkie problemy nie ma do tej pory.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="ebcdd-179">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-179">To do so:</span></span>

1. <span data-ttu-id="ebcdd-180">Otwórz **wszystkie zasady** bloku w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="ebcdd-181">Sprawdź **zastąpić zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="ebcdd-182">Przekaż plik rozszerzenia (TrustFrameworkExtensions.xml) i upewnij się, że nie wystąpi niepowodzenie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="ebcdd-183">Rejestrowanie dostawcy oświadczeń usługi Azure AD do podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="ebcdd-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="ebcdd-184">Teraz należy dodać dostawcy tożsamości usługi Azure AD do jednego z podróże użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="ebcdd-185">W tym momencie Konfigurowanie dostawcy tożsamości, ale nie jest dostępna w żadnym ekrany konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="ebcdd-186">Aby było to możliwe, firma Microsoft będzie utworzyć kopię istniejącej przebieg użytkownika szablonu, a następnie zmodyfikować go, aby miała ona również dostawcy tożsamości usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="ebcdd-187">Otwórz plik bazowy tej zasady (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="ebcdd-188">Znajdź `<UserJourneys>` element i skopiuj cały `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="ebcdd-189">Otwórz plik rozszerzenia (na przykład TrustFrameworkExtensions.xml) i Znajdź `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="ebcdd-190">Jeśli element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="ebcdd-191">Wklej całą `<UserJourney>` węzła, który został skopiowany jako element podrzędny `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="ebcdd-192">Zmień nazwę Identyfikatora nowy przebieg użytkownika (na przykład zmienić nazwę jako `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="ebcdd-193">Ekran "button"</span><span class="sxs-lookup"><span data-stu-id="ebcdd-193">Display the "button"</span></span>

<span data-ttu-id="ebcdd-194">`<ClaimsProviderSelection>` Element jest odpowiednikiem przycisk dostawcy tożsamości na ekranie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="ebcdd-195">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla usługi Azure AD, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="ebcdd-196">Aby dodać ten element:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-196">To add this element:</span></span>

1. <span data-ttu-id="ebcdd-197">Znajdź `<OrchestrationStep>` węzła, który zawiera `Order="1"` w podróży użytkownika, który został właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="ebcdd-198">Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="ebcdd-199">Ustaw `TargetClaimsExchangeId` odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="ebcdd-200">Zaleca się następujące tej samej Konwencji, co inne osoby:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="ebcdd-201">Połącz przycisku akcji</span><span class="sxs-lookup"><span data-stu-id="ebcdd-201">Link the button to an action</span></span>

<span data-ttu-id="ebcdd-202">Teraz, gdy masz przycisku w miejscu, należy połączyć je z akcją.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="ebcdd-203">Akcja, w tym przypadku jest dla usługi Azure AD B2C do komunikowania się z usługą Azure AD otrzymujących token.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="ebcdd-204">Połączyć przycisku akcji przez łączenie techniczne profilu dla dostawcy oświadczeń usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="ebcdd-205">Znajdź `<OrchestrationStep>` zawierającą `Order="2"` w `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="ebcdd-206">Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="ebcdd-207">Aktualizacja `Id` taką samą wartość jak `TargetClaimsExchangeId` w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="ebcdd-208">Aktualizacja `TechnicalProfileReferenceId` dla identyfikatora profilu techniczne utworzonego wcześniej (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="ebcdd-209">Przekaż plik rozszerzenia zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="ebcdd-209">Upload the updated extension file</span></span>

<span data-ttu-id="ebcdd-210">Po zakończeniu modyfikowania pliku rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-210">You are done modifying the extension file.</span></span> <span data-ttu-id="ebcdd-211">Zapisz go.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-211">Save it.</span></span> <span data-ttu-id="ebcdd-212">Przekaż plik i upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="ebcdd-213">Zaktualizuj plik planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ebcdd-213">Update the RP file</span></span>

<span data-ttu-id="ebcdd-214">Należy teraz zaktualizować jednostki uzależnionej pliku strony (RP), który inicjuje przebieg użytkownika, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="ebcdd-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="ebcdd-215">Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym i zmień jego nazwę (na przykład, zmień jego nazwę na SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="ebcdd-216">Otwórz nowy plik i aktualizacji `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` unikatowe wartości (na przykład SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="ebcdd-217">Są to nazwa zasady (na przykład B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="ebcdd-218">Modyfikowanie `ReferenceId` atrybutu w `<DefaultUserJourney>` odpowiadające identyfikator nowego użytkownika podróży utworzony (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="ebcdd-219">Zapisz zmiany i przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ebcdd-220">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ebcdd-220">Troubleshooting</span></span>

<span data-ttu-id="ebcdd-221">Testowanie zasad niestandardowych, które przekazanym właśnie otwierając jego bloku i klikając pozycję **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="ebcdd-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="ebcdd-222">Do diagnozowania problemów, przeczytaj o [Rozwiązywanie problemów z](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebcdd-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebcdd-223">Next steps</span></span>

<span data-ttu-id="ebcdd-224">Przekazywania informacji pozwalających na [ AADB2CPreview@microsoft.com ](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ebcdd-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
