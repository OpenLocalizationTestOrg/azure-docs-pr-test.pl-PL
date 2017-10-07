---
title: "rozwiązań usług partii zadań Azure tooauthenticate usługi Azure Active Directory aaaUse | Dokumentacja firmy Microsoft"
description: "Wsadowe obsługuje usługi Azure AD do uwierzytelniania z hello usługa partia zadań."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="b043a-103">Uwierzytelnianie partii rozwiązań usług w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="b043a-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="b043a-104">Partia zadań Azure obsługuje uwierzytelnianie za pomocą [usługi Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b043a-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="b043a-105">Usługi Azure AD jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b043a-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="b043a-106">Azure sam używa usługi Azure AD tooauthenticate swoich klientów, Administratorzy usługi i użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="b043a-107">Jeśli używasz uwierzytelniania usługi Azure AD z partii zadań Azure, można uwierzytelniać się w jednym z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="b043a-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="b043a-108">Za pomocą **zintegrowane uwierzytelnianie** tooauthenticate użytkownika, do którego prowadzi interakcję z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b043a-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="b043a-109">Aplikacji przy użyciu zintegrowanego uwierzytelniania zbiera poświadczeń użytkownika i używa tych poświadczeń tooauthenticate dostępu tooBatch zasobów.</span><span class="sxs-lookup"><span data-stu-id="b043a-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="b043a-110">Za pomocą **nazwy głównej usługi** tooauthenticate nienadzorowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="b043a-111">Nazwy głównej usługi definiuje hello zasad i uprawnień dla aplikacji w aplikacji hello toorepresent kolejności podczas uzyskiwania dostępu do zasobów w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b043a-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="b043a-112">toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b043a-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="b043a-113">Uwierzytelnianie i puli Tryb alokacji</span><span class="sxs-lookup"><span data-stu-id="b043a-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="b043a-114">Podczas tworzenia konta usługi partia zadań można określić, gdzie można przydzielić pule utworzone dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="b043a-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="b043a-115">Pule tooallocate można wybrać w subskrypcji usługi partii domyślne hello lub w ramach subskrypcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b043a-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="b043a-116">Wybór ma wpływ na sposób uwierzytelniania tooresources dostęp na tym koncie.</span><span class="sxs-lookup"><span data-stu-id="b043a-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="b043a-117">**Partii subskrypcji usługi**.</span><span class="sxs-lookup"><span data-stu-id="b043a-117">**Batch service subscription**.</span></span> <span data-ttu-id="b043a-118">Domyślnie partii pule są przydzielane w ramach subskrypcji usługi partii.</span><span class="sxs-lookup"><span data-stu-id="b043a-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="b043a-119">Jeśli wybierzesz tę opcję, można uwierzytelniać tooresources dostępu do tego konta za pomocą [klucz wstępny](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) lub za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="b043a-120">**Subskrypcja użytkownika.**</span><span class="sxs-lookup"><span data-stu-id="b043a-120">**User subscription.**</span></span> <span data-ttu-id="b043a-121">Można wybrać tooallocate pule partii w subskrypcji użytkownika, który określisz.</span><span class="sxs-lookup"><span data-stu-id="b043a-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="b043a-122">Jeśli wybierzesz tę opcję, musi uwierzytelniać się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="b043a-123">Punkty końcowe na potrzeby uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b043a-123">Endpoints for authentication</span></span>

<span data-ttu-id="b043a-124">tooauthenticate partii aplikacji z usługą Azure AD, należy tooinclude niektórych dobrze znanych punktów końcowych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b043a-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="b043a-125">Punktu końcowego platformy Azure AD</span><span class="sxs-lookup"><span data-stu-id="b043a-125">Azure AD endpoint</span></span>

<span data-ttu-id="b043a-126">Witaj podstawowy punkt końcowy urzędu usługi Azure AD jest:</span><span class="sxs-lookup"><span data-stu-id="b043a-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="b043a-127">tooauthenticate z usługą Azure AD, możesz użyć tego punktu końcowego wraz z hello identyfikator dzierżawcy (identyfikator katalogu).</span><span class="sxs-lookup"><span data-stu-id="b043a-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="b043a-128">Identyfikator dzierżawy Hello określa toouse dzierżawy usługi Azure AD hello do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b043a-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="b043a-129">tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b043a-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="b043a-130">punkt końcowy specyficznego dla dzierżawy Hello jest wymagana podczas uwierzytelniania przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="b043a-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="b043a-131">punkt końcowy specyficznego dla dzierżawy Hello jest opcjonalne podczas uwierzytelniania przy użyciu zintegrowanego uwierzytelniania, ale zalecane.</span><span class="sxs-lookup"><span data-stu-id="b043a-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="b043a-132">Jednak umożliwia także wspólnego punktu końcowego hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="b043a-133">Witaj wspólnego punktu końcowego dostarcza poświadczenia ogólnego zbierania interfejsu, gdy nie podano określonych dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b043a-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="b043a-134">punkt końcowy wspólnej Hello jest `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="b043a-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="b043a-135">Aby uzyskać więcej informacji na temat punktów końcowych usługi Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="b043a-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="b043a-136">Punkt końcowy zasobów usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="b043a-136">Batch resource endpoint</span></span>

<span data-ttu-id="b043a-137">Użyj hello **punktu końcowego zasobów partii zadań Azure** tooacquire token do uwierzytelniania żądań toohello usługa partia zadań:</span><span class="sxs-lookup"><span data-stu-id="b043a-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="b043a-138">Zarejestrować aplikację z dzierżawą</span><span class="sxs-lookup"><span data-stu-id="b043a-138">Register your application with a tenant</span></span>

<span data-ttu-id="b043a-139">pierwszym krokiem Hello przy użyciu usługi Azure AD tooauthenticate rejestruje aplikację w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="b043a-140">Rejestrowanie aplikacji umożliwia toocall hello Azure [biblioteki uwierzytelniania usługi Active Directory] [ aad_adal] (ADAL) w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b043a-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="b043a-141">Witaj ADAL dostarcza interfejs API w celu uwierzytelniania w usłudze Azure AD z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="b043a-142">Rejestrowanie aplikacji jest wymagany, czy planujesz toouse zintegrowanego uwierzytelniania lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="b043a-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="b043a-143">Podczas rejestrowania aplikacji, należy podać informacje o Twojej aplikacji tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="b043a-144">Następnie usługi Azure AD zapewnia identyfikator aplikacji używanie tooassociate aplikacji z usługą Azure AD w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b043a-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="b043a-145">toolearn więcej informacji na temat hello identyfikator aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="b043a-146">tooregister aplikacji partii, wykonaj kroki hello hello [Dodawanie aplikacji](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sekcji [Integrowanie aplikacji z usługą Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="b043a-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="b043a-147">Jeśli zarejestrujesz aplikacji jako aplikacji natywnej, można określić żadnych prawidłowy identyfikator URI dla hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="b043a-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="b043a-148">Nie potrzebuje toobe rzeczywistych punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b043a-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="b043a-149">Po aplikacji został zarejestrowany, zostanie wyświetlony identyfikator aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-149">After you've registered your application, you'll see hello application ID:</span></span>

![Rejestrowanie aplikacji partii z usługą Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="b043a-151">Aby uzyskać więcej informacji o rejestrowaniu aplikacji z usługą Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="b043a-152">Uzyskanie Identyfikatora dzierżawy powitania dla usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="b043a-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="b043a-153">Identyfikator dzierżawy Hello określa hello dzierżawy usługi Azure AD, zapewniający uwierzytelnianie usług tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="b043a-154">tooget hello Identyfikatora dzierżawy, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b043a-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="b043a-155">W portalu Azure hello wybierz usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b043a-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="b043a-156">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b043a-156">Click **Properties**.</span></span>
3. <span data-ttu-id="b043a-157">Skopiuj wartość identyfikatora GUID hello identyfikatora hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="b043a-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="b043a-158">Ta wartość jest również określany jako identyfikator hello dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="b043a-158">This value is also called hello tenant ID.</span></span>

![Skopiuj identyfikator katalogu hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="b043a-160">Uwierzytelnianie zintegrowane</span><span class="sxs-lookup"><span data-stu-id="b043a-160">Use integrated authentication</span></span>

<span data-ttu-id="b043a-161">tooauthenticate ze zintegrowanego uwierzytelniania, należy toogrant Twojego toohello tooconnect uprawnienia aplikacji interfejsu API usługi partii.</span><span class="sxs-lookup"><span data-stu-id="b043a-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="b043a-162">Ten krok umożliwia aplikacji tooauthenticate wywołania toohello partii usługi interfejsu API z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="b043a-163">Po wprowadzeniu [zarejestrowana aplikacja](#register-your-application-with-an-azure-ad-tenant), wykonaj następujące kroki w hello Azure portalu toogrant uzyskać dostępu do usługi partia zadań toohello:</span><span class="sxs-lookup"><span data-stu-id="b043a-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="b043a-164">W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b043a-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="b043a-165">Wyszukaj nazwę aplikacji na liście hello rejestracji aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Wyszukaj nazwę aplikacji](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="b043a-167">Otwórz hello **ustawienia** bloku dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="b043a-168">W hello **dostępu do interfejsu API** zaznacz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="b043a-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="b043a-169">W hello **wymagane uprawnienia** bloku, kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b043a-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="b043a-170">W kroku 1 Wyszukaj hello interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="b043a-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="b043a-171">Wyszukiwania dla każdego z tych parametrów do momentu znalezienia hello interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="b043a-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="b043a-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="b043a-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="b043a-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="b043a-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="b043a-174">W przypadku nowszych dzierżaw usługi Azure AD może być używana ta nazwa.</span><span class="sxs-lookup"><span data-stu-id="b043a-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="b043a-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** jest identyfikator hello hello interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="b043a-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="b043a-176">Po znalezieniu hello interfejsu API partii, zaznacz go i kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b043a-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="b043a-177">W kroku 2, wybierz hello pole wyboru obok zbyt**usługa partia zadań Azure dostępu** i kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b043a-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="b043a-178">Kliknij przycisk hello **gotowe** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b043a-178">Click hello **Done** button.</span></span>

<span data-ttu-id="b043a-179">Witaj **wymagane uprawnienia** bloku teraz wskazuje, że aplikacja Azure AD ma dostęp do tooboth ADAL i hello interfejsu API usługi partii.</span><span class="sxs-lookup"><span data-stu-id="b043a-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="b043a-180">Uprawnienia są przyznawane tooADAL automatycznie podczas rejestrowania aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Interfejs API Udziel uprawnień](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="b043a-182">Użyj nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="b043a-182">Use a service principal</span></span> 

<span data-ttu-id="b043a-183">tooauthenticate aplikację, która działa w instalacji nienadzorowanej, możesz użyć nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="b043a-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="b043a-184">Po po zarejestrowaniu aplikacji, wykonaj następujące kroki w hello Azure tooconfigure portalu nazwy głównej usługi:</span><span class="sxs-lookup"><span data-stu-id="b043a-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="b043a-185">Żądanie klucz tajny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="b043a-186">Przypisywanie aplikacji tooyour RBAC roli.</span><span class="sxs-lookup"><span data-stu-id="b043a-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="b043a-187">Żądanie klucz tajny aplikacji</span><span class="sxs-lookup"><span data-stu-id="b043a-187">Request a secret key for your application</span></span>

<span data-ttu-id="b043a-188">Podczas uwierzytelniania aplikacji z nazwy głównej usługi, wysyła identyfikator aplikacji hello jak tooAzure klucza tajnego usługi AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="b043a-189">Będzie konieczne toocreate i skopiuj toouse klucza tajnego hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b043a-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="b043a-190">Wykonaj następujące kroki w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="b043a-191">W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b043a-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="b043a-192">Wyszukaj nazwę hello aplikacji hello liście rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="b043a-193">Wyświetl hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="b043a-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="b043a-194">W hello **dostępu do interfejsu API** zaznacz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="b043a-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="b043a-195">toocreate klucza, wprowadź opis hello klucza.</span><span class="sxs-lookup"><span data-stu-id="b043a-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="b043a-196">Następnie wybierz czas trwania dla klucza hello jeden lub dwa lata.</span><span class="sxs-lookup"><span data-stu-id="b043a-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="b043a-197">Kliknij przycisk hello **zapisać** przycisk toocreate i wyświetla hello klucza.</span><span class="sxs-lookup"><span data-stu-id="b043a-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="b043a-198">Skopiuj hello wartość klucza tooa bezpiecznym miejscu, ponieważ będziesz w stanie tooaccess pozostawić ją ponownie po hello bloku.</span><span class="sxs-lookup"><span data-stu-id="b043a-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Utwórz klucz tajny](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="b043a-200">Przypisanie roli aplikacji tooyour RBAC</span><span class="sxs-lookup"><span data-stu-id="b043a-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="b043a-201">tooauthenticate z nazwy głównej usługi, należy tooassign RBAC roli tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="b043a-202">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b043a-202">Follow these steps:</span></span>

1. <span data-ttu-id="b043a-203">W hello portalu Azure Przejdź konta usługi partia zadań toohello używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="b043a-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="b043a-204">W hello **ustawienia** bloku dla konta wsadowego hello, wybierz opcję **kontroli dostępu (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="b043a-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="b043a-205">Kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b043a-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="b043a-206">Z hello **roli** listy rozwijanej, wybierz albo hello _współautora_ lub _czytnika_ roli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="b043a-207">Aby uzyskać więcej informacji o tych ról, zobacz [wprowadzenie opartej na rolach kontrola dostępu w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="b043a-208">W hello **wybierz** wprowadź nazwę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b043a-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="b043a-209">Wybierz aplikację z listy hello, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="b043a-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="b043a-210">Aplikacja powinien zostać wyświetlony w ustawieniach kontroli dostępu z rolą RBAC przypisane.</span><span class="sxs-lookup"><span data-stu-id="b043a-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Przypisanie roli aplikacji tooyour RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="b043a-212">Uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b043a-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="b043a-213">Identyfikator dzierżawy Hello określa hello dzierżawy usługi Azure AD, zapewniający uwierzytelnianie usług tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="b043a-214">tooget hello Identyfikatora dzierżawy, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b043a-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="b043a-215">W portalu Azure hello wybierz usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b043a-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="b043a-216">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b043a-216">Click **Properties**.</span></span>
3. <span data-ttu-id="b043a-217">Skopiuj wartość identyfikatora GUID hello identyfikatora hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="b043a-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="b043a-218">Ta wartość jest również określany jako identyfikator hello dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="b043a-218">This value is also called hello tenant ID.</span></span>

![Skopiuj identyfikator katalogu hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="b043a-220">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="b043a-220">Code examples</span></span>

<span data-ttu-id="b043a-221">Przykłady kodu Hello w tej sekcji Pokaż jak tooauthenticate z usługi Azure AD przy użyciu zintegrowanego uwierzytelniania i nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="b043a-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="b043a-222">Te przykłady kodu przy użyciu .NET, ale pojęcia hello są podobne dla innych języków.</span><span class="sxs-lookup"><span data-stu-id="b043a-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="b043a-223">Token uwierzytelniania usługi Azure AD wygasa po upływie godziny.</span><span class="sxs-lookup"><span data-stu-id="b043a-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="b043a-224">Korzystając z długotrwałe **BatchClient** obiektu, firma Microsoft zaleca, aby pobrać token z biblioteki ADAL na każdym tooensure żądania zawsze ma nieprawidłowy token.</span><span class="sxs-lookup"><span data-stu-id="b043a-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="b043a-225">tooachieve to w .NET napisanie metody, że pobiera hello tokenu z usługi Azure AD i przekaż tooa tej metody **BatchTokenCredentials** obiektu jako pełnomocnik.</span><span class="sxs-lookup"><span data-stu-id="b043a-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="b043a-226">Hello delegata metoda jest wywoływana na każdego żądania toohello partii usługi tooensure dostarczonego prawidłowego tokenu.</span><span class="sxs-lookup"><span data-stu-id="b043a-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="b043a-227">Domyślnie ADAL buforuje tokenów, aby nowy token są pobierane z usługi Azure AD tylko wtedy, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b043a-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="b043a-228">Aby uzyskać więcej informacji dotyczących tokenów w usłudze Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="b043a-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="b043a-229">Przykład kodu: używanie programu Azure AD zintegrowane uwierzytelnianie z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b043a-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="b043a-230">tooauthenticate przy użyciu zintegrowanego uwierzytelniania z partiami platformy .NET, odwołanie hello [Azure partiami platformy .NET](https://www.nuget.org/packages/Azure.Batch/) pakietu i hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="b043a-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="b043a-231">Uwzględnij następujące elementy hello `using` instrukcje w kodzie:</span><span class="sxs-lookup"><span data-stu-id="b043a-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="b043a-232">Witaj odwołanie do punktu końcowego usługi Azure AD w kodzie, w tym hello dzierżawy identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="b043a-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="b043a-233">tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b043a-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="b043a-234">Odwołanie hello partii zasobu punktu końcowego usługi:</span><span class="sxs-lookup"><span data-stu-id="b043a-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="b043a-235">Odwołanie konta partii zadań:</span><span class="sxs-lookup"><span data-stu-id="b043a-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="b043a-236">Określ identyfikator aplikacji hello (identyfikator klienta) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="b043a-237">Identyfikator aplikacji Hello jest dostępny z rejestracji aplikacji w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="b043a-238">Kopiuje też hello przekierowania URI, które zostały określone podczas procesu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="b043a-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="b043a-239">Witaj przekierowania określony w kodzie identyfikator URI musi być zgodna hello przekierowania URI podane podczas rejestrowania aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="b043a-240">Zapis token uwierzytelniania hello tooacquire metody wywołania zwrotnego z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="b043a-241">Witaj **GetAuthenticationTokenAsync** wywołania metod wywołania zwrotnego pokazane ADAL tooauthenticate użytkownika, który prowadzi interakcję z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b043a-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="b043a-242">Witaj **AcquireTokenAsync** Metoda podana przez ADAL monity hello ich poświadczenia użytkownika i aplikacji hello będzie kontynuowana po hello użytkownika zapewni im (chyba że ma już pamięci podręcznej poświadczeń):</span><span class="sxs-lookup"><span data-stu-id="b043a-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="b043a-243">Utworzyć **BatchTokenCredentials** obiekt, który przyjmuje hello delegata jako parametr.</span><span class="sxs-lookup"><span data-stu-id="b043a-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="b043a-244">Użyj tych poświadczeń tooopen **BatchClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="b043a-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="b043a-245">Możesz użyć tych **BatchClient** obiektu dla kolejnych operacji względem hello usługa partia zadań:</span><span class="sxs-lookup"><span data-stu-id="b043a-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="b043a-246">Przykład kodu: przy użyciu nazwy głównej usługi Azure AD z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b043a-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="b043a-247">tooauthenticate z nazwy głównej usługi z partiami platformy .NET, odwołanie hello [Azure partiami platformy .NET](https://www.nuget.org/packages/Azure.Batch/) pakietu i hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="b043a-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="b043a-248">Uwzględnij następujące elementy hello `using` instrukcje w kodzie:</span><span class="sxs-lookup"><span data-stu-id="b043a-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="b043a-249">Witaj odwołanie do punktu końcowego usługi Azure AD w kodzie, w tym hello dzierżawy identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="b043a-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="b043a-250">Przy użyciu nazwy głównej usługi, należy podać punktu końcowego specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b043a-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="b043a-251">tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b043a-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="b043a-252">Odwołanie hello partii zasobu punktu końcowego usługi:</span><span class="sxs-lookup"><span data-stu-id="b043a-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="b043a-253">Odwołanie konta partii zadań:</span><span class="sxs-lookup"><span data-stu-id="b043a-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="b043a-254">Określ identyfikator aplikacji hello (identyfikator klienta) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b043a-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="b043a-255">Identyfikator aplikacji Hello jest dostępny z rejestracji aplikacji w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="b043a-256">Określ klucz tajny hello skopiowany z portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b043a-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="b043a-257">Zapis token uwierzytelniania hello tooacquire metody wywołania zwrotnego z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b043a-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="b043a-258">Witaj **GetAuthenticationTokenAsync** metody wywołania zwrotnego pokazane wywołań biblioteki ADAL do uwierzytelniania instalacji nienadzorowanej:</span><span class="sxs-lookup"><span data-stu-id="b043a-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="b043a-259">Utworzyć **BatchTokenCredentials** obiekt, który przyjmuje hello delegata jako parametr.</span><span class="sxs-lookup"><span data-stu-id="b043a-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="b043a-260">Użyj tych poświadczeń tooopen **BatchClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="b043a-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="b043a-261">Następnie można użyć który **BatchClient** obiektu dla kolejnych operacji względem hello usługa partia zadań:</span><span class="sxs-lookup"><span data-stu-id="b043a-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b043a-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b043a-262">Next steps</span></span>

<span data-ttu-id="b043a-263">toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b043a-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="b043a-264">Szczegółowe przykłady, pokazujący, jak są dostępne w hello toouse ADAL [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b043a-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="b043a-265">toolearn więcej informacji na temat nazwy główne usług, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="b043a-266">toocreate główną usługi za pomocą hello Azure portalu, zobacz [toocreate portalu aplikacji usługi Active Directory i nazwy głównej usługi, który ma dostęp do zasobów](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b043a-267">Można również utworzyć nazwy głównej usługi z programu PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b043a-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="b043a-268">aplikacje do zarządzania partii tooauthenticate przy użyciu usługi Azure AD, zobacz [rozwiązań do zarządzania partii uwierzytelniania z usługi Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="b043a-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"
[azure_portal]: http://portal.azure.com
