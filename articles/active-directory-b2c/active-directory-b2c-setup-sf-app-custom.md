---
title: "Usługa Azure Active Directory B2C: Dodawanie dostawcy usług Salesforce SAML za pomocą niestandardowych zasad | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu tworzenia i zarządzania nimi w zasadach niestandardowych usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="94f6a-103">Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usług Salesforce za pośrednictwem SAML</span><span class="sxs-lookup"><span data-stu-id="94f6a-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="94f6a-104">W tym artykule przedstawiono sposób użycia [zasady niestandardowe](active-directory-b2c-overview-custom.md) można skonfigurować konta logowania dla użytkowników z określonych organizacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94f6a-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94f6a-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="94f6a-106">Instalacja usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94f6a-106">Azure AD B2C setup</span></span>

<span data-ttu-id="94f6a-107">Upewnij się, że zostały wykonane wszystkie kroki, które opisano, jak do [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) w usłudze Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="94f6a-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="94f6a-108">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="94f6a-108">These include:</span></span>

* <span data-ttu-id="94f6a-109">Tworzenie dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="94f6a-110">Tworzenie aplikacji usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="94f6a-111">Zarejestruj dwie aplikacje aparatu zasad.</span><span class="sxs-lookup"><span data-stu-id="94f6a-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="94f6a-112">Konfigurowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="94f6a-112">Set up keys.</span></span>
* <span data-ttu-id="94f6a-113">Skonfiguruj pakiet początkowy.</span><span class="sxs-lookup"><span data-stu-id="94f6a-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="94f6a-114">Instalator usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="94f6a-114">Salesforce setup</span></span>

<span data-ttu-id="94f6a-115">W tym artykule przyjęto założenie, że już wykonano następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="94f6a-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="94f6a-116">Konta konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="94f6a-117">Możesz zarejestrować się w celu [bezpłatne konto Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="94f6a-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="94f6a-118">[Konfigurowanie domeny Moje](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) organizacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="94f6a-119">Konfigurowanie usług Salesforce, umożliwiające użytkownikom można było wykonać Federację</span><span class="sxs-lookup"><span data-stu-id="94f6a-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="94f6a-120">Aby pomóc w usłudze Azure AD B2C komunikować się z usług Salesforce, należy uzyskać adres URL metadanych usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="94f6a-121">Konfigurowanie usług Salesforce jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="94f6a-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="94f6a-122">W tym artykule przyjęto założenie, używane są [Salesforce Lightning środowisko](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="94f6a-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="94f6a-123">[Zaloguj się do usługi Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="94f6a-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="94f6a-124">W menu po lewej stronie w obszarze **ustawienia**, rozwiń węzeł **tożsamości**, a następnie kliknij przycisk **dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="94f6a-125">Kliknij przycisk **włączenia dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="94f6a-126">W obszarze **wybierz certyfikat**, wybierz żądany certyfikat usługi Salesforce, aby używać do komunikacji z usługą Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="94f6a-127">(Możesz użyć domyślnego certyfikatu). Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="94f6a-128">Tworzenie połączonej aplikacji w usłudze Salesforce</span><span class="sxs-lookup"><span data-stu-id="94f6a-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="94f6a-129">Na **dostawcy tożsamości** strony, przejdź do **usługodawców**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="94f6a-130">Kliknij przycisk **usługodawców zostaną utworzone za pośrednictwem połączenia aplikacji. Kliknij tutaj.**</span><span class="sxs-lookup"><span data-stu-id="94f6a-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="94f6a-131">W obszarze **podstawowe informacje**, wprowadź wymagane wartości dla połączonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94f6a-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="94f6a-132">W obszarze **ustawień aplikacji sieci Web**, wybierz pozycję **Włącz SAML** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="94f6a-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="94f6a-133">W **identyfikator jednostki** wprowadź następujący adres URL.</span><span class="sxs-lookup"><span data-stu-id="94f6a-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="94f6a-134">Upewnij się, że zastąpić wartość `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="94f6a-135">W **adres URL usługi ACS** wprowadź następujący adres URL.</span><span class="sxs-lookup"><span data-stu-id="94f6a-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="94f6a-136">Upewnij się, że zastąpić wartość `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="94f6a-137">Pozostaw wartości domyślne dla wszystkich innych ustawień.</span><span class="sxs-lookup"><span data-stu-id="94f6a-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="94f6a-138">Przewiń w dół listy, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="94f6a-139">Pobierz adres URL metadanych</span><span class="sxs-lookup"><span data-stu-id="94f6a-139">Get the metadata URL</span></span>

1. <span data-ttu-id="94f6a-140">Na stronie Przegląd połączonych aplikacji, kliknij przycisk **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="94f6a-141">Skopiuj wartość **punkt końcowy odnajdowania metadanych**, a następnie zapisz je.</span><span class="sxs-lookup"><span data-stu-id="94f6a-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="94f6a-142">Będzie on używany w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="94f6a-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="94f6a-143">Konfigurowanie użytkowników Salesforce możliwości utworzenia Federacji</span><span class="sxs-lookup"><span data-stu-id="94f6a-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="94f6a-144">Na **Zarządzaj** strony z połączonych aplikacji, przejdź do **profile**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="94f6a-145">Kliknij przycisk **zarządzania profilami**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="94f6a-146">Wybierz profile (lub grupom użytkowników), który ma zostać wykonana Federacja z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="94f6a-147">Administrator systemu, wybierz **administratorem** Sprawdź okno, tak aby można było wykonać Federację przy użyciu konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="94f6a-148">Generuj certyfikat podpisywania dla usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94f6a-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="94f6a-149">Żądania wysyłane do usługi Salesforce muszą być podpisane przez usługę Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="94f6a-150">Aby wygenerować certyfikat podpisywania, Otwórz program Azure PowerShell, a następnie uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="94f6a-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="94f6a-151">Upewnij się, należy zaktualizować dzierżawy nazwę i hasło w dwóch pierwszych wierszy.</span><span class="sxs-lookup"><span data-stu-id="94f6a-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="94f6a-152">Dodawanie certyfikatu podpisywania SAML do usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94f6a-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="94f6a-153">Przekaż certyfikat podpisywania dla Twojej dzierżawy usługi Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="94f6a-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="94f6a-154">Przejdź do dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94f6a-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="94f6a-155">Kliknij przycisk **ustawienia** > **Framework obsługi tożsamości** > **klucze zasad**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="94f6a-156">Kliknij przycisk **+ Dodaj**, a następnie:</span><span class="sxs-lookup"><span data-stu-id="94f6a-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="94f6a-157">Kliknij przycisk **opcje** > **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="94f6a-158">Wprowadź **nazwa** (na przykład SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="94f6a-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="94f6a-159">Prefiks *B2C_1A_* jest automatycznie dodawany do nazwy klucza.</span><span class="sxs-lookup"><span data-stu-id="94f6a-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="94f6a-160">Aby wybrać certyfikat, wybierz **przekazać formant pliku**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="94f6a-161">Wprowadź hasło certyfikatu, które można ustawić w skrypcie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94f6a-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="94f6a-162">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-162">Click **Create**.</span></span>
4. <span data-ttu-id="94f6a-163">Sprawdź, czy utworzono klucz (na przykład B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="94f6a-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="94f6a-164">Zwróć uwagę, jaka jest pełna nazwa (włącznie z *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="94f6a-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="94f6a-165">Będzie odnosić się do tego klucza później w zasadach.</span><span class="sxs-lookup"><span data-stu-id="94f6a-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="94f6a-166">Tworzenie dostawcy oświadczeń Salesforce SAML w zasadach podstawowej</span><span class="sxs-lookup"><span data-stu-id="94f6a-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="94f6a-167">Musisz zdefiniować Salesforce jako dostawcy oświadczeń, dlatego użytkownicy mogą zarejestrować się przy użyciu Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="94f6a-168">Innymi słowy należy określić punkt końcowy, który usługi Azure AD B2C będzie komunikować się z.</span><span class="sxs-lookup"><span data-stu-id="94f6a-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="94f6a-169">Punkt końcowy zostanie *podaj* zestaw *oświadczeń* używającej usługi Azure AD B2C, aby sprawdzić, czy określony użytkownik został uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="94f6a-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="94f6a-170">Aby to zrobić, należy dodać `<ClaimsProvider>` dla usług Salesforce w pliku rozszerzenie zasad:</span><span class="sxs-lookup"><span data-stu-id="94f6a-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="94f6a-171">W katalogu roboczym otwórz plik rozszerzenia (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="94f6a-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="94f6a-172">Znajdź `<ClaimsProviders>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="94f6a-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="94f6a-173">Jeśli nie istnieje, utwórz go w obszarze węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="94f6a-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="94f6a-174">Dodaj nową `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="94f6a-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="94f6a-175">W obszarze `<ClaimsProvider>` węzła:</span><span class="sxs-lookup"><span data-stu-id="94f6a-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="94f6a-176">Zmień wartość atrybutu `<Domain>` unikatowa wartość odróżniająca `<ClaimsProvider>` od innych dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="94f6a-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="94f6a-177">Zaktualizuj wartość `<DisplayName>` na nazwę wyświetlaną dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="94f6a-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="94f6a-178">Ta wartość nie jest obecnie używana.</span><span class="sxs-lookup"><span data-stu-id="94f6a-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="94f6a-179">Aktualizuj profil techniczne</span><span class="sxs-lookup"><span data-stu-id="94f6a-179">Update the technical profile</span></span>

<span data-ttu-id="94f6a-180">Aby uzyskać tokenu SAML z usług Salesforce, zdefiniuj protokołów używających usługi Azure AD B2C do komunikowania się z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94f6a-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="94f6a-181">Tym `<TechnicalProfile>` elementu `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="94f6a-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="94f6a-182">Aktualizacja Identyfikatora `<TechnicalProfile>` węzła.</span><span class="sxs-lookup"><span data-stu-id="94f6a-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="94f6a-183">Ten identyfikator służy do odwoływania się do tego profilu techniczne z innymi częściami zasad.</span><span class="sxs-lookup"><span data-stu-id="94f6a-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="94f6a-184">Zaktualizuj wartość `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="94f6a-185">Ta wartość jest wyświetlany na przycisku logowania na stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="94f6a-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="94f6a-186">Zaktualizuj wartość `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="94f6a-187">SalesForce korzysta z protokołu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="94f6a-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="94f6a-188">Upewnij się, że wartość `<Protocol>` jest **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="94f6a-189">Aktualizacja `<Metadata>` części poprzedniego XML, aby uwzględnić ustawienia dla określonego konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="94f6a-190">W pliku XML zaktualizuj wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="94f6a-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="94f6a-191">Zaktualizuj wartość `<Item Key="PartnerEntity">` z adresem URL metadanych usługi Salesforce, które zostały wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="94f6a-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="94f6a-192">Ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="94f6a-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="94f6a-193">W `<CryptographicKeys>` sekcji, zaktualizuj tę wartość dla obu wystąpień `StorageReferenceId` na nazwę klucza certyfikatu podpisywania (na przykład B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="94f6a-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="94f6a-194">Przekaż plik rozszerzenia do weryfikacji</span><span class="sxs-lookup"><span data-stu-id="94f6a-194">Upload the extension file for verification</span></span>

<span data-ttu-id="94f6a-195">Twoje zasady został skonfigurowany tak, aby usługi Azure AD B2C potrafi do komunikowania się z usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="94f6a-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="94f6a-196">Spróbuj przekazać plik rozszerzenia zasad, aby sprawdzić, czy nie ma żadnych problemów wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="94f6a-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="94f6a-197">Aby przekazać plik rozszerzenia zasad:</span><span class="sxs-lookup"><span data-stu-id="94f6a-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="94f6a-198">W dzierżawie usługi Azure AD B2C, przejdź do **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="94f6a-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="94f6a-199">Wybierz **zastąpić zasady, jeśli istnieje** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="94f6a-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="94f6a-200">Przekaż plik rozszerzenia (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="94f6a-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="94f6a-201">Upewnij się, że nie wystąpi niepowodzenie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="94f6a-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="94f6a-202">Zarejestruj dostawcę oświadczeń Salesforce SAML na przebieg użytkownika</span><span class="sxs-lookup"><span data-stu-id="94f6a-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="94f6a-203">Następnie dodaj dostawca tożsamości Salesforce SAML do jednego z podróże użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94f6a-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="94f6a-204">W tym momencie Konfigurowanie dostawcy tożsamości, ale nie jest dostępny na stronach rejestracji i logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94f6a-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="94f6a-205">Aby dodać dostawcę tożsamości do strony logowania, najpierw utwórz duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="94f6a-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="94f6a-206">Następnie należy zmodyfikować szablon, dzięki czemu ma również dostawcy tożsamości usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94f6a-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="94f6a-207">Otwórz plik bazowy tej zasady (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="94f6a-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="94f6a-208">Znajdź `<UserJourneys>` elementu, a następnie skopiuj cały `<UserJourney>` wartość, tym Id = "SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="94f6a-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="94f6a-209">Otwórz plik rozszerzenia (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="94f6a-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="94f6a-210">Znajdź `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="94f6a-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="94f6a-211">Jeśli element nie istnieje, utwórz je.</span><span class="sxs-lookup"><span data-stu-id="94f6a-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="94f6a-212">Wklej skopiowany cały `<UserJourney>` jako element podrzędny `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="94f6a-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="94f6a-213">Zmień nazwę Identyfikatora nowej `<UserJourney>` (na przykład SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="94f6a-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="94f6a-214">Wyświetlany przycisk dostawcy tożsamości</span><span class="sxs-lookup"><span data-stu-id="94f6a-214">Display the identity provider button</span></span>

<span data-ttu-id="94f6a-215">`<ClaimsProviderSelection>` Element jest odpowiednikiem przycisk dostawcy tożsamości na stronie tworzenia konta lub logowania.</span><span class="sxs-lookup"><span data-stu-id="94f6a-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="94f6a-216">Dodając `<ClaimsProviderSelection>` elementu Salesforce, nowy przycisk jest wyświetlany, gdy użytkownik przechodzi do tej strony.</span><span class="sxs-lookup"><span data-stu-id="94f6a-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="94f6a-217">Aby wyświetlić przycisk dostawcy tożsamości:</span><span class="sxs-lookup"><span data-stu-id="94f6a-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="94f6a-218">W `<UserJourney>` utworzony, Znajdź `<OrchestrationStep>` z `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="94f6a-219">Dodaj następujący kod XML:</span><span class="sxs-lookup"><span data-stu-id="94f6a-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="94f6a-220">Ustaw `TargetClaimsExchangeId` na wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="94f6a-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="94f6a-221">Zaleca się następujące tej samej Konwencji jako innych (na przykład  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="94f6a-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="94f6a-222">Połącz przycisk dostawcy tożsamości akcji</span><span class="sxs-lookup"><span data-stu-id="94f6a-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="94f6a-223">Teraz, gdy masz przycisk dostawcy tożsamości w miejscu, należy go powiązać akcji.</span><span class="sxs-lookup"><span data-stu-id="94f6a-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="94f6a-224">W takim przypadku akcja jest dla usługi Azure AD B2C do komunikowania się z Salesforce odebrać tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="94f6a-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="94f6a-225">Można to zrobić przez łączenie techniczne profilu dla użytkownika SAML Salesforce dostawcy oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="94f6a-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="94f6a-226">W `<UserJourney>` węzła, Znajdź `<OrchestrationStep>` z `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="94f6a-227">Dodaj następujący kod XML:</span><span class="sxs-lookup"><span data-stu-id="94f6a-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="94f6a-228">Aktualizacja `Id` na tę samą wartość, który był wcześniej używany przez `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="94f6a-229">Aktualizacja `TechnicalProfileReferenceId` do `Id` techniczne profilu utworzonego wcześniej (na przykład ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="94f6a-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="94f6a-230">Przekaż plik rozszerzenia zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="94f6a-230">Upload the updated extension file</span></span>

<span data-ttu-id="94f6a-231">Po zakończeniu modyfikowania pliku rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="94f6a-231">You are done modifying the extension file.</span></span> <span data-ttu-id="94f6a-232">Zapisz i przekazywanie tego pliku.</span><span class="sxs-lookup"><span data-stu-id="94f6a-232">Save and upload this file.</span></span> <span data-ttu-id="94f6a-233">Upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="94f6a-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="94f6a-234">Zaktualizuj plik jednostki uzależnionej strony</span><span class="sxs-lookup"><span data-stu-id="94f6a-234">Update the relying party file</span></span>

<span data-ttu-id="94f6a-235">Następnie zaktualizuj jednostki uzależnionej pliku strony (RP), który inicjuje przebieg użytkownika, który został utworzony:</span><span class="sxs-lookup"><span data-stu-id="94f6a-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="94f6a-236">Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="94f6a-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="94f6a-237">Następnie należy zmienić jego nazwę (na przykład SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="94f6a-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="94f6a-238">Otwórz nowy plik i aktualizacji `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` z unikatową wartość.</span><span class="sxs-lookup"><span data-stu-id="94f6a-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="94f6a-239">Jest to nazwa zasady (na przykład SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="94f6a-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="94f6a-240">Modyfikowanie `ReferenceId` atrybutu w `<DefaultUserJourney>` odpowiadające `Id` nowe podróży użytkownika utworzony (na przykład SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="94f6a-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="94f6a-241">Zapisz zmiany, a następnie przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="94f6a-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="94f6a-242">Testowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="94f6a-242">Test and troubleshoot</span></span>

<span data-ttu-id="94f6a-243">Testowanie zasad niestandardowych, które przekazanym właśnie, w portalu Azure, przejdź do bloku zasady, a następnie kliknij przycisk **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="94f6a-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="94f6a-244">Jeśli nie powiedzie się, zobacz [Rozwiązywanie problemów dotyczących zasad niestandardowych](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="94f6a-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94f6a-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94f6a-245">Next steps</span></span>

<span data-ttu-id="94f6a-246">Przekazywania informacji pozwalających na [ AADB2CPreview@microsoft.com ](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="94f6a-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
