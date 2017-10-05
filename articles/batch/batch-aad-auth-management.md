---
title: "Użyj usługi Azure Active Directory do uwierzytelniania rozwiązania do zarządzania partii | Dokumentacja firmy Microsoft"
description: "Aplikacji skompilowanej za pomocą usługi Azure resource manager i dostawca zasobów partii uwierzytelniania za pomocą usługi Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="352eb-103">Uwierzytelnianie rozwiązań do zarządzania partii z usługą Active Directory</span><span class="sxs-lookup"><span data-stu-id="352eb-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="352eb-104">Aplikacje, które wywołują usługi zarządzania usługi partia zadań Azure uwierzytelniania za pomocą [usługi Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="352eb-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="352eb-105">Usługi Azure AD jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="352eb-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="352eb-106">Azure sam używa usługi Azure AD do uwierzytelniania klientów, Administratorzy usługi i użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="352eb-107">Biblioteka zarządzania partiami platformy .NET ujawnia typy do pracy z kontami partii, klucze konta, aplikacje i pakiety aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="352eb-108">Biblioteka zarządzania partiami platformy .NET jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] do programowego zarządzania tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="352eb-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="352eb-109">Usługi Azure AD jest wymagany do uwierzytelniania żądań wysyłanych za pomocą dowolnego klienta dostawcy zasobów platformy Azure, w tym biblioteki zarządzania partiami platformy .NET i za pośrednictwem [usługi Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="352eb-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="352eb-110">W tym artykule firma Microsoft eksplorowania przy użyciu usługi Azure AD do uwierzytelniania z aplikacji korzystających z biblioteki zarządzania partiami platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="352eb-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="352eb-111">Zostanie przedstawiony sposób uwierzytelniania administratorem subskrypcji lub administratora współpracującego przy użyciu zintegrowanego uwierzytelniania przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="352eb-112">Używamy [AccountManagment] [ acct_mgmt_sample] przykładowy projekt, dostępne w witrynie GitHub, aby zapoznać się z biblioteki zarządzania partiami platformy .NET przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="352eb-113">Aby dowiedzieć się więcej na temat używania biblioteki zarządzania partiami platformy .NET i przykładowe AccountManagement, zobacz [partii Zarządzanie kontami i limitami przydziału z biblioteki klienta usługi partia zadań zarządzania dla programu .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="352eb-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="352eb-114">Zarejestrować aplikację w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="352eb-114">Register your application with Azure AD</span></span>

<span data-ttu-id="352eb-115">Azure [biblioteki uwierzytelniania usługi Active Directory] [ aad_adal] (ADAL), udostępnia interfejs programowe do usługi Azure AD do użycia w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="352eb-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="352eb-116">Wywoływanie biblioteki ADAL z aplikacji, należy zarejestrować aplikację w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="352eb-117">Podczas rejestrowania aplikacji, podanych usługi Azure AD z informacjami o aplikacji, łącznie z jej nazwę w ramach dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="352eb-118">Następnie usługi Azure AD zapewnia identyfikator aplikacji, która umożliwia kojarzenie aplikacji z usługą Azure AD w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="352eb-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="352eb-119">Aby dowiedzieć się więcej na temat identyfikator aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="352eb-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="352eb-120">Aby zarejestrować AccountManagement przykładowej aplikacji, postępuj zgodnie z instrukcjami [Dodawanie aplikacji](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sekcji [Integrowanie aplikacji z usługą Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="352eb-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="352eb-121">Określ **natywną aplikację kliencką** dla typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="352eb-122">Branży standardowego protokołu OAuth 2.0 Identyfikator URI **identyfikator URI przekierowania** jest `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="352eb-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="352eb-123">Jednak można określić dowolny prawidłowy identyfikator URI (takich jak `http://myaccountmanagementsample`) dla **identyfikator URI przekierowania**, ponieważ nie musi być rzeczywistym punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="352eb-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="352eb-124">Po zakończeniu procesu rejestracji, zostanie wyświetlony identyfikator aplikacji i identyfikator obiektu (nazwy głównej usługi) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="352eb-125">Udziel dostępu do interfejsu API usługi Azure Resource Manager do aplikacji</span><span class="sxs-lookup"><span data-stu-id="352eb-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="352eb-126">Następnie należy delegować dostęp do aplikacji interfejsu API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="352eb-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="352eb-127">Identyfikator usługi Azure AD dla interfejsu API Menedżera zasobów jest **interfejs API zarządzania usługami Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="352eb-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="352eb-128">Wykonaj następujące kroki w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="352eb-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="352eb-129">W okienku nawigacji po lewej stronie portalu Azure wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="352eb-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="352eb-130">Wyszukaj nazwę aplikacji na liście rejestracji aplikacji:</span><span class="sxs-lookup"><span data-stu-id="352eb-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Wyszukaj nazwę aplikacji](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="352eb-132">Wyświetl **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="352eb-132">Display the **Settings** blade.</span></span> <span data-ttu-id="352eb-133">W **dostępu do interfejsu API** zaznacz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="352eb-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="352eb-134">Kliknij przycisk **Dodaj** można dodać nowego wymaganych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="352eb-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="352eb-135">W kroku 1, wprowadź **interfejs API zarządzania usługami Windows Azure**, wybierz z listy wyników tego interfejsu API i kliknij przycisk **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="352eb-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="352eb-136">W kroku 2, zaznacz pole wyboru **Access Azure klasycznego modelu wdrażania jako użytkowników w organizacji**i kliknij przycisk **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="352eb-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="352eb-137">Kliknij przycisk **gotowe** przycisku.</span><span class="sxs-lookup"><span data-stu-id="352eb-137">Click the **Done** button.</span></span>

<span data-ttu-id="352eb-138">**Wymagane uprawnienia** bloku teraz pokazuje, że do biblioteki ADAL i Menedżer zasobów interfejsów API zostały przyznane uprawnienia do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="352eb-139">Przyznano uprawnienia do biblioteki ADAL domyślnie podczas rejestrowania aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegowanie uprawnień do interfejsu API Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="352eb-141">Punkty końcowe systemu Azure AD</span><span class="sxs-lookup"><span data-stu-id="352eb-141">Azure AD endpoints</span></span>

<span data-ttu-id="352eb-142">Na potrzeby uwierzytelniania rozwiązań zarządzania partii z usługą Azure AD, konieczne będzie dwa punkty końcowe dobrze znany.</span><span class="sxs-lookup"><span data-stu-id="352eb-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="352eb-143">**Wspólnego punktu końcowego usługi Azure AD** dostarcza poświadczenia ogólnego zbierania interfejsu po określonym dzierżawcy nie zostanie podany, jak w przypadku zintegrowanego uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="352eb-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="352eb-144">**Punktu końcowego usługi Azure Resource Manager** jest używany do uzyskiwania tokenu do uwierzytelniania żądań do usługi zarządzania partii:</span><span class="sxs-lookup"><span data-stu-id="352eb-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="352eb-145">Przykładowa aplikacja AccountManagement definiuje stałe dla tych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="352eb-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="352eb-146">Pozostaw te stałe, bez zmian:</span><span class="sxs-lookup"><span data-stu-id="352eb-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="352eb-147">Odwołanie do Identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="352eb-147">Reference your application ID</span></span> 

<span data-ttu-id="352eb-148">Aplikacja kliencka używa Identyfikatora aplikacji (nazywane również identyfikator klienta) można uzyskać dostępu do usługi Azure AD w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="352eb-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="352eb-149">Po aplikacji został zarejestrowany w portalu Azure, zaktualizuj kod, aby używał podany przez usługę Azure AD w zarejestrowany aplikacji identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="352eb-150">W przykładowej aplikacji AccountManagement skopiuj swój identyfikator aplikacji z portalu Azure do odpowiedniej stała:</span><span class="sxs-lookup"><span data-stu-id="352eb-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="352eb-151">Kopiuje też przekierowania URI, które zostały określone podczas procesu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="352eb-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="352eb-152">Określone w kodzie identyfikator URI przekierowania musi być zgodna przekierowania URI podane podczas rejestrowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="352eb-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="352eb-153">Uzyskanie tokenu uwierzytelniania usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="352eb-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="352eb-154">Po zarejestrować próbkę AccountManagement w dzierżawie usługi Azure AD i zaktualizować przykładowy kod źródłowy własnymi wartościami próbki jest gotowy do uwierzytelniania za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352eb-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="352eb-155">Po uruchomieniu próbki ADAL próbuje uzyskać tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="352eb-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="352eb-156">W tym kroku monituje o podanie poświadczeń Microsoft:</span><span class="sxs-lookup"><span data-stu-id="352eb-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="352eb-157">Po podaniu poświadczeń przykładowej aplikacji można przystąpić do wysyłania żądań uwierzytelnionych do usługi partia zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="352eb-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="352eb-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="352eb-158">Next steps</span></span>

<span data-ttu-id="352eb-159">Aby uzyskać więcej informacji na temat uruchamiania [AccountManagement przykładowej aplikacji][acct_mgmt_sample], zobacz [partii Zarządzanie kontami i limitami przydziału z biblioteki klienta usługi partia zadań zarządzania dla programu .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="352eb-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="352eb-160">Aby dowiedzieć się więcej na temat usługi Azure AD, zobacz [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="352eb-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="352eb-161">Szczegółowe przykłady przedstawiająca sposób używania biblioteki ADAL są dostępne w [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="352eb-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="352eb-162">Na potrzeby uwierzytelniania partii usługi aplikacji za pomocą usługi Azure AD, zobacz [rozwiązań usług uwierzytelniania partii z usługą Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="352eb-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="352eb-163">[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="352eb-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="352eb-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"</span><span class="sxs-lookup"><span data-stu-id="352eb-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="352eb-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="352eb-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
