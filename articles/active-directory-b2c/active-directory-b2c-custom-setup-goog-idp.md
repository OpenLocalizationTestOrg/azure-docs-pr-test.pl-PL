---
title: "Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych"
description: "Przykładowe przy użyciu usługi Google + jako dostawca tożsamości za pomocą protokołu OAuth2"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="080e9-103">Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="080e9-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="080e9-104">W tym przewodniku opisano sposób włączenia logowania użytkowników z konta Google + za pośrednictwem [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="080e9-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="080e9-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="080e9-105">Prerequisites</span></span>

<span data-ttu-id="080e9-106">Wykonaj kroki [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="080e9-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="080e9-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="080e9-107">These steps include:</span></span>

1.  <span data-ttu-id="080e9-108">Tworzenie aplikacji konto Google +.</span><span class="sxs-lookup"><span data-stu-id="080e9-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="080e9-109">Dodawanie klucza aplikacji konto Google + do usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="080e9-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="080e9-110">Dodawanie dostawcy oświadczeń dla zasad</span><span class="sxs-lookup"><span data-stu-id="080e9-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="080e9-111">Rejestrowanie Google + konto dostawcy oświadczeń wobec przebieg użytkownika</span><span class="sxs-lookup"><span data-stu-id="080e9-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="080e9-112">Przesyłanie zasad do usługi Azure AD B2C dzierżawy i przetestować go</span><span class="sxs-lookup"><span data-stu-id="080e9-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="080e9-113">Tworzenie aplikacji konto Google +</span><span class="sxs-lookup"><span data-stu-id="080e9-113">Create a Google+ account application</span></span>
<span data-ttu-id="080e9-114">Aby użyć Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy do utworzenia aplikacji Google + i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="080e9-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="080e9-115">Możesz zarejestrować Google + aplikacją w tym miejscu: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="080e9-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="080e9-116">Przejdź do [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.</span><span class="sxs-lookup"><span data-stu-id="080e9-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="080e9-117">Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="080e9-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="080e9-118">Polecenie **menu projekty**.</span><span class="sxs-lookup"><span data-stu-id="080e9-118">Click on the **Projects menu**.</span></span>

    ![Google + konto — wybierz projekt](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="080e9-120">Polecenie  **+**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="080e9-120">Click on the **+** button.</span></span>

    ![Google + konto — Utwórz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="080e9-122">Wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="080e9-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google + konto — nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="080e9-124">Poczekaj, aż projekt jest gotowy i kliknij na **menu projekty**.</span><span class="sxs-lookup"><span data-stu-id="080e9-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Google + konto - Zaczekaj, aż nowego projektu jest gotowe do użycia.](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="080e9-126">Kliknij nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="080e9-126">Click on your project name.</span></span>

    ![Google + konto — wybierz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="080e9-128">Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="080e9-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="080e9-129">Kliknij przycisk **ekranu zgoda OAuth** u góry.</span><span class="sxs-lookup"><span data-stu-id="080e9-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Google + konto — Ustaw OAuth zgody ekranu](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="080e9-131">Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="080e9-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google + - poświadczeń aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="080e9-133">Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="080e9-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - Utwórz nowe poświadczenia aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="080e9-135">W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="080e9-135">Under **Application type**, select **Web application**.</span></span>

    ![Google + — Wybieranie typu aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="080e9-137">Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **autoryzowanych przekierowania URI** pola.</span><span class="sxs-lookup"><span data-stu-id="080e9-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="080e9-138">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="080e9-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="080e9-139">**{Dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="080e9-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="080e9-140">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="080e9-140">Click **Create**.</span></span>

    ![Google + - zapewniają autoryzację JavaScript źródeł i Przekierowanie URI](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="080e9-142">Skopiuj wartości z **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="080e9-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="080e9-143">Potrzebne do skonfigurowania Google + funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="080e9-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="080e9-144">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="080e9-144">**Client secret** is an important security credential.</span></span>

    ![Google + - skopiowanie wartości klucza tajnego identyfikator i klienta klienta](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="080e9-146">Dodaj klucz aplikacji konto Google + do usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="080e9-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="080e9-147">Federacja z konta Google + wymaga klucz tajny klienta konta Google + do relacji zaufania usługi Azure AD B2C w imieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="080e9-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="080e9-148">Należy przechowywać klucz tajny aplikacji Google + w dzierżawie usługi Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="080e9-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="080e9-149">Przejdź do dzierżawy usługi Azure AD B2C i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**</span><span class="sxs-lookup"><span data-stu-id="080e9-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="080e9-150">Wybierz **zasad kluczy** Aby wyświetlić dostępne w Twojej dzierżawie kluczy.</span><span class="sxs-lookup"><span data-stu-id="080e9-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="080e9-151">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="080e9-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="080e9-152">Aby uzyskać **opcje**, użyj **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="080e9-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="080e9-153">Aby uzyskać **nazwa**, użyj `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="080e9-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="080e9-154">Prefiks `B2C_1A_` mogą być dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="080e9-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="080e9-155">W **klucz tajny** wprowadź klucz tajny aplikacji firmy Microsoft z https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="080e9-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="080e9-156">Aby uzyskać **użycie klucza**, użyj **podpisu**.</span><span class="sxs-lookup"><span data-stu-id="080e9-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="080e9-157">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="080e9-157">Click **Create**</span></span>
9.  <span data-ttu-id="080e9-158">Upewnij się, że utworzono klucz `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="080e9-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="080e9-159">Dodawanie dostawcy oświadczeń w zasadach rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="080e9-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="080e9-160">Użytkownikom na logowanie się przy użyciu konta Google +, należy określić konto Google + jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="080e9-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="080e9-161">Innymi słowy należy określić punkt końcowy, który komunikuje się usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="080e9-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="080e9-162">Punkt końcowy zawiera zestaw oświadczeń, które są używane przez usługę Azure AD B2C, aby sprawdzić, czy określony użytkownik jest uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="080e9-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="080e9-163">Zdefiniuj konto Google + jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="080e9-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="080e9-164">Otwórz plik zasad rozszerzenia (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="080e9-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="080e9-165">Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.</span><span class="sxs-lookup"><span data-stu-id="080e9-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="080e9-166">Znajdź `<ClaimsProviders>` sekcji</span><span class="sxs-lookup"><span data-stu-id="080e9-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="080e9-167">Dodaj następujący fragment kodu XML w obszarze `ClaimsProviders` elementu i zastępowanie `client_id` wartość przy użyciu usługi Google + konto aplikacji Identyfikatora klienta przed zapisaniem pliku.</span><span class="sxs-lookup"><span data-stu-id="080e9-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="080e9-168">Zarejestruj Google + konto dostawcy oświadczeń wobec Zarejestruj się lub zaloguj w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="080e9-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="080e9-169">Dostawca tożsamości nie został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="080e9-169">The identity provider has been set up.</span></span>  <span data-ttu-id="080e9-170">Jednak nie jest dostępna w żadnym ekrany konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="080e9-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="080e9-171">Dodawanie dostawcy tożsamości konta Google + do użytkownika `SignUpOrSignIn` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="080e9-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="080e9-172">Aby było to możliwe, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="080e9-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="080e9-173">Następnie dodaj dostawcy tożsamości konta Google +:</span><span class="sxs-lookup"><span data-stu-id="080e9-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="080e9-174">Jeśli został skopiowany `<UserJourneys>` elementu z pliku podstawowego zasad do pliku rozszerzenie (TrustFrameworkExtensions.xml), możesz przejść do tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="080e9-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="080e9-175">Otwórz plik bazowy tej zasady (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="080e9-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="080e9-176">Znajdź `<UserJourneys>` element i skopiuj cała zawartość `<UserJourneys>` węzła.</span><span class="sxs-lookup"><span data-stu-id="080e9-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="080e9-177">Otwórz plik rozszerzenia (na przykład TrustFrameworkExtensions.xml) i Znajdź `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="080e9-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="080e9-178">Jeśli element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="080e9-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="080e9-179">Wklej całą zawartość `<UserJournesy>` węzła, który został skopiowany jako element podrzędny `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="080e9-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="080e9-180">Wyświetlany przycisk</span><span class="sxs-lookup"><span data-stu-id="080e9-180">Display the button</span></span>
<span data-ttu-id="080e9-181">`<ClaimsProviderSelections>` Element definiuje listę opcje wyboru dostawcy oświadczeń i ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="080e9-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="080e9-182">`<ClaimsProviderSelection>`element jest odpowiednikiem przycisku dostawcy tożsamości na stronie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="080e9-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="080e9-183">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta Google + nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie.</span><span class="sxs-lookup"><span data-stu-id="080e9-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="080e9-184">Aby dodać ten element:</span><span class="sxs-lookup"><span data-stu-id="080e9-184">To add this element:</span></span>

1.  <span data-ttu-id="080e9-185">Znajdź `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="080e9-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="080e9-186">Zlokalizuj `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="080e9-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="080e9-187">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="080e9-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="080e9-188">Połącz przycisku akcji</span><span class="sxs-lookup"><span data-stu-id="080e9-188">Link the button to an action</span></span>
<span data-ttu-id="080e9-189">Teraz, gdy masz przycisku w miejscu, należy połączyć je z akcją.</span><span class="sxs-lookup"><span data-stu-id="080e9-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="080e9-190">Akcja, w tym przypadku jest dla usługi Azure AD B2C do komunikowania się z konta Google + otrzymujących token.</span><span class="sxs-lookup"><span data-stu-id="080e9-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="080e9-191">Znajdź `<OrchestrationStep>` zawierającą `Order="2"` w `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="080e9-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="080e9-192">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="080e9-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="080e9-193">Upewnij się, `Id` ma taką samą wartość jak `TargetClaimsExchangeId` w poprzedniej sekcji</span><span class="sxs-lookup"><span data-stu-id="080e9-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="080e9-194">Upewnij się, `TechnicalProfileReferenceId` ustawiony identyfikator techniczne profilu utworzonego wcześniej (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="080e9-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="080e9-195">Przekaż zasady dla Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="080e9-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="080e9-196">W [portalu Azure](https://portal.azure.com), przejdź do [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), a następnie otwórz **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="080e9-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="080e9-197">Wybierz **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="080e9-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="080e9-198">Otwórz **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="080e9-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="080e9-199">Wybierz **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="080e9-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="080e9-200">Sprawdź **zastąpić zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="080e9-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="080e9-201">**Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji</span><span class="sxs-lookup"><span data-stu-id="080e9-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="080e9-202">Testowanie zasad niestandardowych przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="080e9-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="080e9-203">Otwórz **ustawienia usługi Azure AD B2C** i przejdź do **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="080e9-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="080e9-204">**Uruchom teraz** wymaga co najmniej jednej aplikacji można preregistered dla dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="080e9-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="080e9-205">Aby dowiedzieć się, jak zarejestrować aplikacji, zapoznaj się z usługi Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="080e9-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="080e9-206">Otwórz **B2C_1A_signup_signin**, jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="080e9-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="080e9-207">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="080e9-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="080e9-208">Można będzie zalogować się przy użyciu konta Google +.</span><span class="sxs-lookup"><span data-stu-id="080e9-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="080e9-209">[Opcjonalnie] Zarejestruj Google + konto dostawcy oświadczeń do edycji profilu użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="080e9-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="080e9-210">Można również dodać dostawcy tożsamości konta Google + do użytkownika `ProfileEdit` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="080e9-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="080e9-211">Aby było to możliwe, możemy Powtórz ostatnie dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="080e9-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="080e9-212">Wyświetlany przycisk</span><span class="sxs-lookup"><span data-stu-id="080e9-212">Display the button</span></span>
1.  <span data-ttu-id="080e9-213">Otwórz plik rozszerzenia zasad (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="080e9-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="080e9-214">Znajdź `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="080e9-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="080e9-215">Zlokalizuj `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="080e9-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="080e9-216">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="080e9-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="080e9-217">Połącz przycisku akcji</span><span class="sxs-lookup"><span data-stu-id="080e9-217">Link the button to an action</span></span>
1.  <span data-ttu-id="080e9-218">Znajdź `<OrchestrationStep>` zawierającą `Order="2"` w `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="080e9-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="080e9-219">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="080e9-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="080e9-220">Testowanie zasad niestandardowych edycji profilu przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="080e9-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="080e9-221">Otwórz **ustawienia usługi Azure AD B2C** i przejdź do **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="080e9-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="080e9-222">Otwórz **B2C_1A_ProfileEdit**, jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="080e9-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="080e9-223">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="080e9-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="080e9-224">Można będzie zalogować się przy użyciu konta Google +.</span><span class="sxs-lookup"><span data-stu-id="080e9-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="080e9-225">Pobierz pliki pełną zasad</span><span class="sxs-lookup"><span data-stu-id="080e9-225">Download the complete policy files</span></span>
<span data-ttu-id="080e9-226">Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych zasad niestandardowych, które przeprowadzenie pliki po zakończeniu wprowadzenie do zasad niestandardowych, zamiast korzystać z tych przykładowych plików.</span><span class="sxs-lookup"><span data-stu-id="080e9-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="080e9-227">Przykładowe pliki zasad dla odwołania</span><span class="sxs-lookup"><span data-stu-id="080e9-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
