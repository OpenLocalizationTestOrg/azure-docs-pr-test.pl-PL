---
title: "Usługa Azure Active Directory B2C: Dodać własne atrybutów niestandardowych zasad i używać w edycji profilu | Dokumentacja firmy Microsoft"
description: "Przewodnik dotyczący przy użyciu właściwości rozszerzenia, atrybuty niestandardowe, w tym ich z interfejsu użytkownika"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="864ed-103">Usługa Azure Active Directory B2C: Tworzenie i używanie niestandardowych atrybutów w profilu niestandardowego edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="864ed-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="864ed-104">W tym artykule Tworzenie niestandardowego atrybutu w katalogu usługi Azure AD B2C i jako oświadczenia niestandardowego w podróży użytkownika edycji profilu za pomocą tego nowego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="864ed-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="864ed-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="864ed-105">Prerequisites</span></span>

<span data-ttu-id="864ed-106">Wykonaj kroki w artykule [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="864ed-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="864ed-107">Wykorzystaj niestandardowe atrybuty do zbierania informacji o klientach w usłudze Azure Active Directory B2C za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="864ed-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="864ed-108">Katalogu usługi Azure Active Directory (Azure AD) B2C jest dostarczany z wbudowanego zestawu atrybutów: podana imię, nazwisko, Miasto, kod pocztowy, userPrincipalName, itp.  Często muszą utworzyć własne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="864ed-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="864ed-109">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="864ed-109">For example:</span></span>
* <span data-ttu-id="864ed-110">Aplikacja klienta uwzględniającym musi być zachowany atrybut, taki jak "LoyaltyNumber."</span><span class="sxs-lookup"><span data-stu-id="864ed-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="864ed-111">Dostawca tożsamości ma identyfikator unikatowy użytkownika, który musi zostać zapisany, takie jak "uniqueUserGUID"."</span><span class="sxs-lookup"><span data-stu-id="864ed-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="864ed-112">Przebieg użytkownika niestandardowego musi być zachowany stan użytkownika, takie jak "migrationStatus."</span><span class="sxs-lookup"><span data-stu-id="864ed-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="864ed-113">Z usługi Azure AD B2C można rozszerzyć zestaw atrybutów przechowywanych dla każdego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="864ed-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="864ed-114">Może także odczytywać i zapisywać te atrybuty za pomocą [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="864ed-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="864ed-115">Właściwości rozszerzenia rozszerzenie schematu obiektu użytkownika w katalogu.</span><span class="sxs-lookup"><span data-stu-id="864ed-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="864ed-116">Właściwość rozszerzenia warunki, atrybutu niestandardowego i oświadczenia niestandardowe zapoznaj się samo w kontekście tego artykułu, a nazwa może być różna w zależności od kontekstu (aplikacji, obiekt zasad).</span><span class="sxs-lookup"><span data-stu-id="864ed-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="864ed-117">Właściwości rozszerzenia mogą być rejestrowane tylko dla obiektu aplikacji, nawet jeśli dane mogą zawierać dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="864ed-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="864ed-118">Właściwość jest dołączony do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="864ed-118">The property is attached to the application.</span></span> <span data-ttu-id="864ed-119">Obiekt aplikacji muszą mieć uprawnienie zapisu do rejestru właściwość rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="864ed-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="864ed-120">100 właściwości rozszerzenia (za pośrednictwem wszystkich typów i wszystkie aplikacje) mogą być zapisywane na żadnym pojedynczym obiektem.</span><span class="sxs-lookup"><span data-stu-id="864ed-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="864ed-121">Właściwości rozszerzenia są dodawane na typ docelowy katalogu i stanie się dostępny natychmiast w dzierżawie usługi Azure AD B2C w katalogu.</span><span class="sxs-lookup"><span data-stu-id="864ed-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="864ed-122">Jeśli aplikacja zostanie usunięty, są również usuwane te właściwości rozszerzenia wraz z danymi znajdującymi się w nich dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="864ed-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="864ed-123">Jeśli właściwość rozszerzenia zostanie usunięty przez aplikację, zostanie ono usunięte obiekty katalogu docelowego i wartości usunięte.</span><span class="sxs-lookup"><span data-stu-id="864ed-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="864ed-124">Właściwości rozszerzenia istnieje tylko w kontekście zarejestrowaną aplikację w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="864ed-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="864ed-125">Identyfikator obiektu tej aplikacji muszą być zawarte w TechnicalProfile, który go używać.</span><span class="sxs-lookup"><span data-stu-id="864ed-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="864ed-126">Katalog usługi Azure AD B2C zwykle obejmuje aplikację sieci Web o nazwie `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="864ed-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="864ed-127">Ta aplikacja jest używany głównie za pomocą zasad wbudowany b2c dla oświadczenia niestandardowe utworzone za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="864ed-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="864ed-128">Za pomocą tej aplikacji do zarejestrowania rozszerzenia zasad niestandardowych b2c jest zalecane tylko dla użytkowników zaawansowanych.</span><span class="sxs-lookup"><span data-stu-id="864ed-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="864ed-129">Odpowiednie instrukcje znajdują się w sekcji kolejne kroki w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="864ed-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="864ed-130">Tworzenie nowej aplikacji do zapisania właściwości rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="864ed-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="864ed-131">Otwórz sesję przeglądania i przejdź do [Azure porta](https://portal.azure.com) i zaloguj się przy użyciu poświadczeń administracyjnych katalogu B2C, chcesz skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="864ed-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="864ed-132">Kliknij przycisk **usługi Azure Active Directory** w menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="864ed-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="864ed-133">Konieczne może być go znaleźć, wybierając więcej usług >.</span><span class="sxs-lookup"><span data-stu-id="864ed-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="864ed-134">Wybierz **rejestracji aplikacji** i kliknij przycisk **nowej rejestracji aplikacji**</span><span class="sxs-lookup"><span data-stu-id="864ed-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="864ed-135">Podaj następujące wpisy zalecane:</span><span class="sxs-lookup"><span data-stu-id="864ed-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="864ed-136">Określ nazwę dla aplikacji sieci web: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="864ed-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="864ed-137">Typ aplikacji: aplikacja/interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="864ed-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="864ed-138">URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="864ed-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="864ed-139">Wybierz ** utworzyć.</span><span class="sxs-lookup"><span data-stu-id="864ed-139">Select **Create.</span></span> <span data-ttu-id="864ed-140">Pomyślne zakończenie pojawia się w **powiadomienia**</span><span class="sxs-lookup"><span data-stu-id="864ed-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="864ed-141">Wybierz aplikację sieci web nowo utworzony: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="864ed-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="864ed-142">Wybierz ustawienia: **wymagane uprawnienia**</span><span class="sxs-lookup"><span data-stu-id="864ed-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="864ed-143">Wybierz interfejs API **usługi Active Directory systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="864ed-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="864ed-144">Należy zaznaczyć uprawnienia aplikacji: **Odczyt i zapis danych katalogu**, i **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="864ed-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="864ed-145">Wybierz **udzielić uprawnień** i Potwierdź **tak**.</span><span class="sxs-lookup"><span data-stu-id="864ed-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="864ed-146">Skopiuj do Schowka i Zapisz następujące identyfikatory z aplikacji sieci Web-GraphAPI-DirectoryExtensions > Ustawienia > Właściwości ></span><span class="sxs-lookup"><span data-stu-id="864ed-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="864ed-147">**Identyfikator aplikacji** .</span><span class="sxs-lookup"><span data-stu-id="864ed-147">**Application ID** .</span></span> <span data-ttu-id="864ed-148">Przykład:`103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="864ed-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="864ed-149">**Obiekt o identyfikatorze**.</span><span class="sxs-lookup"><span data-stu-id="864ed-149">**Object ID**.</span></span> <span data-ttu-id="864ed-150">Przykład:`80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="864ed-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="864ed-151">Modyfikowanie zasad niestandardowych do dodania ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="864ed-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="864ed-152"><TechnicalProfile Id="AAD-Common"> Jest określana jako "wspólne", ponieważ jego elementy są uwzględnione w i użyć ponownie w wszystkie usługi Azure Active Directory TechnicalProfiles przy użyciu elementu:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="864ed-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="864ed-153">Podczas TechnicalProfile zapisuje po raz pierwszy właściwość nowo utworzonego rozszerzenia, może wystąpić błąd jednorazowego.</span><span class="sxs-lookup"><span data-stu-id="864ed-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="864ed-154">Właściwość rozszerzenia jest tworzony podczas pierwszego, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="864ed-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="864ed-155">Przy użyciu nowego rozszerzenia właściwości / atrybutu niestandardowego w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="864ed-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="864ed-156">Otwieranie pliku Party(RP) jednostki uzależnionej, który opisuje zasady edytować przebieg użytkownika.</span><span class="sxs-lookup"><span data-stu-id="864ed-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="864ed-157">Jest uruchamiany,, może być wskazane w celu pobrania z już skonfigurowany wersji pliku RP PolicyEdit bezpośrednio z sekcji zasady niestandardowe Azure B2C w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="864ed-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="864ed-158">Alternatywnie można otworzyć pliku XML z folderu magazynu.</span><span class="sxs-lookup"><span data-stu-id="864ed-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="864ed-159">Dodawanie oświadczenia niestandardowego `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="864ed-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="864ed-160">Dodając niestandardowe oświadczenia w `<RelyingParty>` elementu, jest przekazywany jako parametr do UserJourney TechnicalProfiles i uwzględnione w tokenie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="864ed-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="864ed-161">Dodawanie definicji oświadczenia do pliku rozszerzenie zasad `TrustFrameworkExtensions.xml` wewnątrz `<ClaimsSchema>` element, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="864ed-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="864ed-162">Dodaj takie same oświadczeń definicji do pliku podstawowego zasad `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="864ed-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="864ed-163">Dodawanie `ClaimType` definicji w zarówno dla typu podstawowego, jak i plik rozszerzenia zwykle nie jest konieczne, jednak ponieważ następnych krokach zostaną dodane extension_loyaltyId do TechnicalProfiles w pliku podstawowego, modułu sprawdzania poprawności zasad spowoduje odrzucenie przekazywania pliku podstawowego bez niego.</span><span class="sxs-lookup"><span data-stu-id="864ed-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="864ed-164">Może to być przydatne do śledzenia realizacji przebieg użytkownika o nazwie "ProfileEdit" w pliku TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="864ed-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="864ed-165">Wyszukaj przebieg użytkownika o tej samej nazwie w edytorze i sprawdź, czy aranżacji krok 5 wywołuje TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="864ed-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="864ed-166">Wyszukiwanie i sprawdzić to TechnicalProfile, aby zapoznać się z przepływem.</span><span class="sxs-lookup"><span data-stu-id="864ed-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="864ed-167">Dodaj loyaltyId zgodnie z oświadczeń przychodzących i wychodzących w TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="864ed-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="864ed-168">Dodaj oświadczenie w TechnicalProfile "AAD-UserWriteProfileUsingObjectId", aby zachować wartości oświadczenia we właściwości rozszerzenia dla bieżącego użytkownika w katalogu.</span><span class="sxs-lookup"><span data-stu-id="864ed-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="864ed-169">Dodaj oświadczenie w TechnicalProfile "AAD-UserReadUsingObjectId" można odczytać wartości atrybutu rozszerzenia za każdym razem, gdy użytkownik loguje.</span><span class="sxs-lookup"><span data-stu-id="864ed-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="864ed-170">Dotychczas TechnicalProfiles zostały zmienione w strumieniu tylko kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="864ed-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="864ed-171">Razie nowy atrybut przepływu konto społecznego/federacyjnych inny zestaw TechnicalProfiles musi zostać zmienione.</span><span class="sxs-lookup"><span data-stu-id="864ed-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="864ed-172">Zobacz następne kroki.</span><span class="sxs-lookup"><span data-stu-id="864ed-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="864ed-173">IncludeTechnicalProfile element dodaje wszystkie elementy wspólnych AAD tego TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="864ed-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="864ed-174">Testowanie zasad niestandardowych za pomocą "Uruchom teraz"</span><span class="sxs-lookup"><span data-stu-id="864ed-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="864ed-175">Otwórz **bloku usługi Azure AD B2C** i przejdź do **tożsamości środowiska Framework > zasady niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="864ed-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="864ed-176">Wybierz zasady niestandardowe przekazywane i kliknij przycisk **Uruchom teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="864ed-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="864ed-177">Należy zalogowanie przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="864ed-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="864ed-178">Token identyfikatora wysyłane powrót do aplikacji zawiera nową właściwość rozszerzenia jako oświadczenia niestandardowego poprzedzony extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="864ed-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="864ed-179">Zobacz przykład.</span><span class="sxs-lookup"><span data-stu-id="864ed-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="864ed-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="864ed-180">Next steps</span></span>

<span data-ttu-id="864ed-181">Dodaj nowe oświadczenie do przepływów dla logowania do kont społecznościowych, zmieniając TechnicalProfiles na liście.</span><span class="sxs-lookup"><span data-stu-id="864ed-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="864ed-182">Te dwie TechnicalProfiles są używane przez federacyjne/społecznego konto logowania do zapisu i odczytu danych użytkownika za pomocą alternativeSecurityId jako lokalizacji obiektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="864ed-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="864ed-183">Przy użyciu tego samego atrybuty rozszerzenia między zasadami wbudowanych i niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="864ed-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="864ed-184">Po dodaniu rozszerzenia atrybutów (alias niestandardowych atrybutów) za pośrednictwem portalu środowisko te atrybuty są rejestrowane przy użyciu ** b2c rozszerzeń aplikacji w każdej dzierżawy b2c.</span><span class="sxs-lookup"><span data-stu-id="864ed-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="864ed-185">Aby użyć te atrybuty rozszerzenia w zasadach niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="864ed-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="864ed-186">W ramach dzierżawy usługi b2c w portal.azure.com, przejdź do **usługi Azure Active Directory** i wybierz **rejestracji aplikacji**</span><span class="sxs-lookup"><span data-stu-id="864ed-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="864ed-187">Znajdź użytkownika **b2c rozszerzeń aplikacji** i wybierz ją</span><span class="sxs-lookup"><span data-stu-id="864ed-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="864ed-188">W obszarze "Essentials" rekordu **identyfikator aplikacji** i **identyfikator obiektu:**</span><span class="sxs-lookup"><span data-stu-id="864ed-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="864ed-189">Należy uwzględnić je w metadanych programu AAD typowe techniczne profilu podobnie jak w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="864ed-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="864ed-190">Aby zachować spójność z obsługi portalu, Utwórz te atrybuty przy użyciu interfejsu użytkownika portalu *przed* używane w niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="864ed-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="864ed-191">Podczas tworzenia atrybutu "ActivationStatus" w portalu, użytkownik musi odwoływać się do niego w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="864ed-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="864ed-192">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="864ed-192">Reference</span></span>

* <span data-ttu-id="864ed-193">A **techniczne profilu (TP)** jest typem elementu, który można traktować jako *funkcja* definiuje nazwę punktu końcowego, jego metadanych, protokół, a szczegóły programu exchange oświadczeń który tożsamości Należy wykonać czynności Framework.</span><span class="sxs-lookup"><span data-stu-id="864ed-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="864ed-194">Gdy to *funkcja* jest wywoływana w kroku aranżacji lub z innego TechnicalProfile, InputClaims i OutputClaims są przekazywane jako parametry przez obiekt wywołujący.</span><span class="sxs-lookup"><span data-stu-id="864ed-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="864ed-195">Pełna oczyszczania we właściwościach rozszerzenia, zobacz artykuł [rozszerzenia SCHEMATU katalogu | POJĘCIA DOTYCZĄCE INTERFEJSU API PROGRAMU GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="864ed-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="864ed-196">Atrybuty rozszerzenia interfejsu API programu Graph są nazywane zgodnie z Konwencją `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="864ed-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="864ed-197">Zasady niestandardowe nazywać atrybuty rozszerzenia extension_attributename, w związku z tym pominięcie ApplicationObjectId w pliku XML</span><span class="sxs-lookup"><span data-stu-id="864ed-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
