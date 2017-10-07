---
title: "rozwiązania do zarządzania partii tooauthenticate aaaUse usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Aplikacji skompilowanej za pomocą usługi Azure resource manager i dostawca zasobów partii hello uwierzytelniania za pomocą usługi Azure AD."
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
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="9bd9b-103">Uwierzytelnianie rozwiązań do zarządzania partii z usługą Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bd9b-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="9bd9b-104">Aplikacje, które wywołują usługi zarządzania usługi partia zadań Azure hello uwierzytelniania za pomocą [usługi Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="9bd9b-105">Usługi Azure AD jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="9bd9b-106">Azure sam używa usługi Azure AD do uwierzytelniania hello swoich klientów, Administratorzy usługi i użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="9bd9b-107">Biblioteka zarządzania partiami platformy .NET Hello ujawnia typy do pracy z kontami partii, klucze konta, aplikacje i pakiety aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="9bd9b-108">Biblioteka zarządzania partiami platformy .NET Hello jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] toomanage tych zasobów programowo.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="9bd9b-109">Usługi Azure AD jest żądań tooauthenticate wymagane przez dowolnego klienta dostawcy zasobów platformy Azure, w tym hello biblioteki zarządzania partiami platformy .NET oraz [usługi Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="9bd9b-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="9bd9b-110">W tym artykule firma Microsoft eksplorowania przy użyciu usługi Azure AD tooauthenticate przez aplikacje korzystające z biblioteki zarządzania partiami platformy .NET hello.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="9bd9b-111">Zostanie przedstawiony sposób tooauthenticate toouse usługi Azure AD administratora subskrypcji lub administratora współpracującego przy użyciu zintegrowanego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="9bd9b-112">Używamy hello [AccountManagment] [ acct_mgmt_sample] przykładowy projekt, dostępne w witrynie GitHub, toowalk hello biblioteki zarządzania partiami platformy .NET przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="9bd9b-113">toolearn więcej informacji na temat przy użyciu biblioteki zarządzania partiami platformy .NET hello i przykładowe AccountManagement hello, zobacz [konta usługi partia zadań zarządzania i przydziały hello biblioteki klienta usługi partia zadań zarządzania dla platformy .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="9bd9b-114">Zarejestrować aplikację w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bd9b-114">Register your application with Azure AD</span></span>

<span data-ttu-id="9bd9b-115">Hello Azure [biblioteki uwierzytelniania usługi Active Directory] [ aad_adal] (ADAL) udostępnia interfejs programistyczny tooAzure AD do użycia w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="9bd9b-116">toocall biblioteki ADAL z aplikacji, musisz zarejestrować aplikację w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="9bd9b-117">Podczas rejestrowania aplikacji, podanych usługi Azure AD z informacjami o aplikacji, łącznie z jej nazwę w ramach dzierżawy usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="9bd9b-118">Następnie usługi Azure AD zapewnia identyfikator aplikacji używanie tooassociate aplikacji z usługą Azure AD w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="9bd9b-119">toolearn więcej informacji na temat hello identyfikator aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="9bd9b-120">Witaj tooregister AccountManagement przykładowej aplikacji, wykonaj kroki hello hello [Dodawanie aplikacji](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sekcji [Integrowanie aplikacji z usługą Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="9bd9b-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="9bd9b-121">Określ **natywną aplikację kliencką** hello typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="9bd9b-122">Witaj branżowy standard OAuth 2.0 Identyfikator URI hello **identyfikator URI przekierowania** jest `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="9bd9b-123">Jednak można określić dowolny prawidłowy identyfikator URI (takich jak `http://myaccountmanagementsample`) dla hello **identyfikator URI przekierowania**, ponieważ nie jest konieczne toobe rzeczywistych punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="9bd9b-124">Po zakończeniu procesu rejestracji hello zostanie Zobacz identyfikator aplikacji hello oraz hello Identyfikatora obiektu (nazwy głównej usługi) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="9bd9b-125">Udzielić aplikacji tooyour dostępu do interfejsu API usługi Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="9bd9b-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="9bd9b-126">Następnie należy toodelegate dostępu tooyour aplikacji toohello interfejsu API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="9bd9b-127">Identyfikator Hello Azure AD dla hello interfejs API Menedżera zasobów jest **interfejs API zarządzania usługami Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="9bd9b-128">Wykonaj następujące kroki w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="9bd9b-129">W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="9bd9b-130">Wyszukaj nazwę aplikacji na liście hello rejestracji aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Wyszukaj nazwę aplikacji](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="9bd9b-132">Wyświetl hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="9bd9b-133">W hello **dostępu do interfejsu API** zaznacz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="9bd9b-134">Kliknij przycisk **Dodaj** tooadd nowe wymaganych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="9bd9b-135">W kroku 1, wprowadź **interfejs API zarządzania usługami Windows Azure**, wybierz z listy hello wyników tego interfejsu API i kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="9bd9b-136">W kroku 2, wybierz hello pole wyboru obok zbyt**Access Azure klasycznego modelu wdrażania jako użytkowników w organizacji**i kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="9bd9b-137">Kliknij przycisk hello **gotowe** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-137">Click hello **Done** button.</span></span>

<span data-ttu-id="9bd9b-138">Witaj **wymagane uprawnienia** bloku teraz pokazuje, że aplikacja tooyour uprawnienia zostały przyznane tooboth hello ADAL i interfejsów API Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="9bd9b-139">Uprawnienia są przyznawane tooADAL domyślnie podczas rejestrowania aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Delegowanie uprawnień toohello interfejsu API usługi Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="9bd9b-141">Punkty końcowe systemu Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bd9b-141">Azure AD endpoints</span></span>

<span data-ttu-id="9bd9b-142">tooauthenticate Twojego rozwiązania do zarządzania partii z usługą Azure AD, będą potrzebne dwa punkty końcowe dobrze znany.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="9bd9b-143">Witaj **wspólnego punktu końcowego usługi Azure AD** dostarcza poświadczenia ogólnego zbierania interfejsu po określonym dzierżawcy nie zostanie podany, tak jak przypadku hello zintegrowanego uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="9bd9b-144">Witaj **punktu końcowego usługi Azure Resource Manager** jest używane tooacquire token dla usługi zarządzania partii toohello żądań uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="9bd9b-145">Witaj AccountManagement przykładowej aplikacji definiuje stałe dla tych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="9bd9b-146">Pozostaw te stałe, bez zmian:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="9bd9b-147">Odwołanie do Identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="9bd9b-147">Reference your application ID</span></span> 

<span data-ttu-id="9bd9b-148">Aplikacja kliencka używa tooaccess identyfikator (również określonego tooas hello identyfikator klienta) aplikacji hello Azure AD w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="9bd9b-149">Aplikacji został zarejestrowany w portalu Azure hello, zaktualizuj kod toouse hello aplikacji Identyfikatora dostarczane przez usługę Azure AD w zarejestrowany aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="9bd9b-150">W hello AccountManagement przykładowej aplikacji skopiuj swój identyfikator aplikacji z stała odpowiednie hello toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="9bd9b-151">Kopiuje też hello przekierowania URI, które zostały określone podczas procesu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="9bd9b-152">Witaj przekierowania określony w kodzie identyfikator URI musi być zgodna hello przekierowania URI podane podczas rejestrowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="9bd9b-153">Uzyskanie tokenu uwierzytelniania usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bd9b-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="9bd9b-154">Po zarejestrować próbkę AccountManagement hello w dzierżawie usługi Azure AD hello i zaktualizować hello przykładowy kod źródłowy własnymi wartościami próbki hello jest gotowy tooauthenticate przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="9bd9b-155">Po uruchomieniu próbki hello hello ADAL prób tooacquire tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="9bd9b-156">W tym kroku monituje o podanie poświadczeń Microsoft:</span><span class="sxs-lookup"><span data-stu-id="9bd9b-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="9bd9b-157">Po podaniu poświadczeń hello przykładowej aplikacji przejść tooissue uwierzytelnić żądania toohello usługa partia zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9bd9b-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9bd9b-158">Next steps</span></span>

<span data-ttu-id="9bd9b-159">Aby uzyskać więcej informacji na temat uruchamiania hello [AccountManagement przykładowej aplikacji][acct_mgmt_sample], zobacz [konta usługi partia zadań zarządzania i przydziały hello biblioteki klienta usługi partia zadań zarządzania dla platformy .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="9bd9b-160">toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="9bd9b-161">Szczegółowe przykłady, pokazujący, jak są dostępne w hello toouse ADAL [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9bd9b-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="9bd9b-162">aplikacje usług partii tooauthenticate przy użyciu usługi Azure AD, zobacz [rozwiązań usług uwierzytelniania partii z usługą Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9bd9b-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
