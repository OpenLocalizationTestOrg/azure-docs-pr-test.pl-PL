---
title: "Wdrożenia, wywołaj i uwierzytelniania sieci web API i interfejsów API REST dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wdrażanie, uwierzytelniania i wywołania interfejsów API i interfejsów API REST w sieci web w przepływach pracy dla systemu integracji z usługą Azure Logic Apps"
keywords: "interfejsy API, interfejsy API REST, łączniki, przepływy pracy, integracji systemu w sieci Web, uwierzytelniania"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="22fb9-104">Wdrożenia, wywołaj i uwierzytelniania niestandardowych interfejsów API łączników dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="22fb9-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="22fb9-105">Po [Tworzenie niestandardowych interfejsów API](./logic-apps-create-api-app.md) zawierających akcji lub wyzwalaczy do użycia w przepływach pracy aplikacji logiki, swoje interfejsy API należy wdrożyć przed wywołaniem je.</span><span class="sxs-lookup"><span data-stu-id="22fb9-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="22fb9-106">I chociaż jakiegokolwiek interfejsu API można wywołać z aplikacji logiki, aby uzyskać najlepsze wyniki, Dodaj [Swagger metadanych](http://swagger.io/specification/) opisujący Twój interfejs API operacji i parametry.</span><span class="sxs-lookup"><span data-stu-id="22fb9-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="22fb9-107">Ten plik struktury Swagger pomaga interfejsu API działa lepiej i łatwo zintegrować z usługą logic apps.</span><span class="sxs-lookup"><span data-stu-id="22fb9-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="22fb9-108">Można wdrożyć swoje interfejsy API jako [sieci web aplikacji](../app-service-web/app-service-web-overview.md), ale warto wdrożyć swoje interfejsy API jako [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md), które mogą ułatwić zadania podczas kompilacji, hosta i korzystanie z interfejsów API w chmurze i lokalnie.</span><span class="sxs-lookup"><span data-stu-id="22fb9-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="22fb9-109">Nie trzeba zmieniać żadnego kodu w swoje interfejsy API — wystarczy go wdrożyć kod w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="22fb9-110">Swoje interfejsy API mogą być hostowane na [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md), platformy jako — usługa (PaaS) oferta zapewnia w jednym ze sposobów najlepsze najprostszym i najbardziej skalowalny hosting interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="22fb9-111">Do uwierzytelnienia wywołania z aplikacji logiki swoje interfejsy API, można ustawić usługę Azure Active Directory w portalu Azure, nie trzeba zaktualizować kodu.</span><span class="sxs-lookup"><span data-stu-id="22fb9-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="22fb9-112">Lub może wymagać i wymusić uwierzytelnianie za pomocą kodu Twój interfejs API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="22fb9-113">Wdrażanie aplikacji sieci web lub aplikacji interfejsu API interfejsu API</span><span class="sxs-lookup"><span data-stu-id="22fb9-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="22fb9-114">Przed niestandardowego interfejsu API można wywołać z aplikacji logiki, należy wdrożyć jako aplikacji sieci web lub aplikacji interfejsu API interfejsu API w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="22fb9-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="22fb9-115">Ponadto odczytywać dokumentu Swagger przez projektanta aplikacji logiki, ustaw właściwości definicji interfejsu API i Włącz [współużytkowanie zasobów między źródłami (CORS) do udostępniania](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) dla aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="22fb9-116">W portalu Azure wybierz aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="22fb9-117">W bloku, który zostanie otwarty, w obszarze **interfejsu API**, wybierz **definicji interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="22fb9-118">Ustaw **lokalizacji definicji interfejsu API** na adres URL pliku swagger.json.</span><span class="sxs-lookup"><span data-stu-id="22fb9-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="22fb9-119">Adres URL pojawia się zwykle w następującym formacie:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="22fb9-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Łącze do pliku programu Swagger do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="22fb9-121">W obszarze **interfejsu API**, wybierz **CORS**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="22fb9-122">Ustawienie zasad CORS dla **dozwolone źródła** do  **"*"** (Zezwalaj na wszystkie).</span><span class="sxs-lookup"><span data-stu-id="22fb9-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="22fb9-123">Ustawienie to pozwala żądania przy użyciu projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-123">This setting permits requests from Logic App Designer.</span></span>

   ![Zezwala na żądania z projektanta aplikacji logiki do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="22fb9-125">Aby uzyskać więcej informacji zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="22fb9-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="22fb9-126">Dodaj metadane programu Swagger dla interfejsów API sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="22fb9-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="22fb9-127">Wdrażanie interfejsów API sieci web ASP.NET w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="22fb9-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="22fb9-128">Wywoływanie niestandardowego interfejsu API z logiki przepływów pracy aplikacji</span><span class="sxs-lookup"><span data-stu-id="22fb9-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="22fb9-129">Po skonfigurowaniu właściwości definicji interfejsu API i mechanizmu CORS wyzwalacze i akcje niestandardowego interfejsu API powinien być dostępny do uwzględnienia w przepływie pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="22fb9-130">Aby wyświetlić Swagger URL witryn sieci Web, możesz wyszukać subskrypcji witryny sieci Web w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="22fb9-131">Aby wyświetlić dostępne akcje i dane wejściowe, wskazując dokumentu Swagger, użyj [HTTP + Swagger akcji](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="22fb9-132">Aby wywołać jakiegokolwiek interfejsu API, łącznie z interfejsów API, które nie mają lub udostępnianie dokumentu Swagger, zawsze można utworzyć żądania z [akcji HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="22fb9-133">Uwierzytelnienia wywołań do niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="22fb9-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="22fb9-134">Możesz zabezpieczyć wywołania do niestandardowego interfejsu API w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="22fb9-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="22fb9-135">[Nie zmian w kodzie](#no-code): interfejs API ochrony [usługi Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) za pośrednictwem portalu Azure, więc nie trzeba zaktualizować kodu lub ponownego wdrażania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="22fb9-136">Domyślnie uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure nie zapewnia precyzyjną autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="22fb9-137">Na przykład to uwierzytelnianie blokuje interfejsu API do określonych dzierżawy, a nie do określonego użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="22fb9-138">[Zaktualizuj kod Twój interfejs API](#update-code): ochrona interfejsu API przez wymuszenie [uwierzytelnianie certyfikatu](#certificate), [uwierzytelnianie podstawowe](#basic), lub [uwierzytelniania usługi Azure AD](#azure-ad-code) za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="22fb9-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="22fb9-139">Uwierzytelnianie wywołań interfejsu API bez zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="22fb9-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="22fb9-140">Poniżej przedstawiono ogólne kroki dla tej metody:</span><span class="sxs-lookup"><span data-stu-id="22fb9-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="22fb9-141">Utwórz dwa [tożsamości aplikacji usługi Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): jeden dla aplikacji logiki i jeden dla aplikacji sieci web (lub aplikacji interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="22fb9-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="22fb9-142">Na potrzeby uwierzytelniania wywołań interfejsu API, Użyj poświadczeń (identyfikator klienta i klucz tajny) dla [nazwy głównej usługi](../app-service-api/app-service-api-dotnet-service-principal-auth.md) która jest skojarzona z tożsamość aplikacji usługi Azure AD dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="22fb9-143">Zawiera identyfikatorów aplikacji w definicji aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="22fb9-144">Część 1: Tworzenie aplikacji logiki tożsamość aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="22fb9-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="22fb9-145">Aplikację logiki używa tego tożsamość aplikacji usługi Azure AD do uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22fb9-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="22fb9-146">Wystarczy tylko skonfigurować tej tożsamości jeden raz dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="22fb9-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="22fb9-147">Na przykład możesz użyć tej samej tożsamości dla wszystkich aplikacji logiki, mimo że można utworzyć unikatowych tożsamości dla każdej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="22fb9-148">Możesz skonfigurować te tożsamości w portalu Azure [klasycznego portalu Azure](#app-identity-logic-classic), lub użyj [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="22fb9-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="22fb9-149">**Tworzenie aplikacji logiki tożsamości aplikacji w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="22fb9-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="22fb9-150">W [portalu Azure](https://portal.azure.com "https://portal.azure.com"), wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="22fb9-151">Upewnij się, że jesteś w tym samym katalogu co aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="22fb9-152">Aby przełączyć katalogów, kliknij profil i wybierz inny katalog.</span><span class="sxs-lookup"><span data-stu-id="22fb9-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="22fb9-153">Lub wybierz **omówienie** > **katalogu przełącznika**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="22fb9-154">W menu katalogu w obszarze **Zarządzaj**, wybierz **rejestracji aplikacji** > **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="22fb9-155">Domyślnie lista rejestracji aplikacji zawiera wszystkich rejestracji aplikacji w katalogu.</span><span class="sxs-lookup"><span data-stu-id="22fb9-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="22fb9-156">Aby wyświetlić tylko rejestracji aplikacji, w polu wyszukiwania, wybierz **Moje aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Tworzenie nowej rejestracji aplikacji](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="22fb9-158">Nadaj nazwę tożsamości aplikacji, pozostaw **typu aplikacji** ustawioną **aplikacji sieci Web / interfejs API**, Podaj unikatową ciąg w formacie domeny dla **adres URL logowania**i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Podaj nazwę i logowania jednokrotnego adres URL dla tożsamości aplikacji](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="22fb9-160">Tożsamość aplikacji utworzonej dla aplikacji logiki teraz zostanie wyświetlony na liście rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Tożsamość aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="22fb9-162">Na liście rejestracji aplikacji wybierz nowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="22fb9-163">Skopiuj i Zapisz **identyfikator aplikacji** do użycia jako "Identyfikator klienta" aplikację logiki w część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Skopiuj i Zapisz identyfikator aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="22fb9-165">Jeśli ustawienia tożsamość aplikacji nie są widoczne, wybierz **ustawienia** lub **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="22fb9-166">W obszarze **dostępu do interfejsu API**, wybierz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="22fb9-167">W obszarze **opis**, podaj nazwę klucza.</span><span class="sxs-lookup"><span data-stu-id="22fb9-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="22fb9-168">W obszarze **Expires**, wybierz czas trwania dla klucza.</span><span class="sxs-lookup"><span data-stu-id="22fb9-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="22fb9-169">Klucz, który tworzysz działa jako tożsamość aplikacji "tajny" lub hasła do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Utwórz klucz tożsamości aplikacji logiki](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="22fb9-171">Na pasku narzędzi wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="22fb9-172">W obszarze **wartość**, klucz zostanie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="22fb9-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="22fb9-173">**Upewnij się, że skopiuj i Zapisz klucz** do późniejszego użycia, ponieważ jest ukryta klucz wychodząc klucza bloku.</span><span class="sxs-lookup"><span data-stu-id="22fb9-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="22fb9-174">Podczas konfigurowania aplikacji logiki w część 3, należy określić ten klucz jako "secret" lub hasło.</span><span class="sxs-lookup"><span data-stu-id="22fb9-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Skopiuj i Zapisz klucz do użycia później](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="22fb9-176">**Utwórz tożsamość aplikacji dla aplikacji logiki w klasycznym portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="22fb9-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="22fb9-177">W klasycznym portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="22fb9-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="22fb9-178">Należy wybrać ten sam katalog, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="22fb9-179">Na **aplikacji** , wybierz pozycję **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="22fb9-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="22fb9-180">Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **dalej** (Strzałka w prawo).</span><span class="sxs-lookup"><span data-stu-id="22fb9-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="22fb9-181">W obszarze **właściwości aplikacji**, podaj unikatowy ciąg w formacie domeny **adres URL logowania** i **identyfikator URI aplikacji**i wybierz polecenie **Complete** (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="22fb9-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="22fb9-182">Na **Konfiguruj** karcie, skopiuj i Zapisz **identyfikator klienta** aplikacji logiki do używania w części 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="22fb9-183">W obszarze **klucze**, otwórz **wybierz czas trwania** listy.</span><span class="sxs-lookup"><span data-stu-id="22fb9-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="22fb9-184">Wybierz czas trwania dla klucza.</span><span class="sxs-lookup"><span data-stu-id="22fb9-184">Select a duration for your key.</span></span>

   <span data-ttu-id="22fb9-185">Klucz, który tworzysz działa jako tożsamość aplikacji "tajny" lub hasła do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="22fb9-186">W dolnej części strony, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="22fb9-187">Może być konieczne kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="22fb9-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="22fb9-188">W obszarze **klucze**, skopiuj i Zapisz klucz pojawia się która teraz.</span><span class="sxs-lookup"><span data-stu-id="22fb9-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="22fb9-189">Podczas konfigurowania aplikacji logiki w część 3, należy określić ten klucz jako "secret" lub hasło.</span><span class="sxs-lookup"><span data-stu-id="22fb9-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="22fb9-190">Aby uzyskać więcej informacji, Dowiedz się, jak [skonfigurować aplikację usługi aplikacji do użycia usługi Azure Active Directory logowania](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="22fb9-191">**Tworzenie aplikacji logiki tożsamości aplikacji w programie PowerShell**</span><span class="sxs-lookup"><span data-stu-id="22fb9-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="22fb9-192">Można wykonać tego zadania za pomocą usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22fb9-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="22fb9-193">W programie PowerShell uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="22fb9-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="22fb9-194">Upewnij się skopiować **identyfikator dzierżawcy** (identyfikator GUID dla dzierżawy usługi Azure AD), **identyfikator aplikacji**i hasła, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="22fb9-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="22fb9-195">Aby uzyskać więcej informacji, Dowiedz się, jak [Tworzenie nazwy głównej usługi przy użyciu programu PowerShell dostęp do zasobów](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="22fb9-196">Część 2: Tworzenie tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="22fb9-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="22fb9-197">Jeśli aplikację sieci web lub aplikacji interfejsu API jest już wdrożone, można włączyć uwierzytelnianie i utworzenia tożsamości aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22fb9-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="22fb9-198">W przeciwnym razie można [włączyć uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="22fb9-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="22fb9-199">**Utwórz tożsamość aplikacji i włączyć uwierzytelnianie w portalu Azure w przypadku wdrożonej aplikacji**</span><span class="sxs-lookup"><span data-stu-id="22fb9-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="22fb9-200">W [portalu Azure](https://portal.azure.com "https://portal.azure.com"), Znajdź i wybierz aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="22fb9-201">W obszarze **ustawienia**, wybierz **uwierzytelniania/autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="22fb9-202">W obszarze **aplikacji uwierzytelniania usługi**, Włącz uwierzytelnianie **na**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="22fb9-203">W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Włączanie uwierzytelniania](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="22fb9-205">Teraz należy utworzyć tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="22fb9-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="22fb9-206">Na **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** do **Express**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="22fb9-207">Wybierz **Utwórz nową aplikację usługi AD**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="22fb9-208">Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Utwórz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="22fb9-210">Na **uwierzytelniania / autoryzacji bloku**, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="22fb9-211">Teraz należy znaleźć tożsamości aplikacji, który został skojarzony z aplikacji sieci web lub aplikacji interfejsu API klienta ID oraz Identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="22fb9-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="22fb9-212">Należy użyć tych identyfikatorów w część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="22fb9-213">Aby kontynuować następujące kroki w portalu Azure lub [klasycznego portalu Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="22fb9-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="22fb9-214">**Znajdź identyfikator klienta i Identyfikatora dzierżawcy tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="22fb9-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="22fb9-215">W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Wybierz polecenie "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="22fb9-217">Na **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** do **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="22fb9-218">Kopiuj **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="22fb9-219">Jeśli **identyfikator klienta** i **adres Url wystawcy** nie są wyświetlane, spróbuj odświeżyć portalu Azure i powtórz krok 1.</span><span class="sxs-lookup"><span data-stu-id="22fb9-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="22fb9-220">W obszarze **adres Url wystawcy**, skopiuj i Zapisz tylko identyfikator GUID dla część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="22fb9-221">Umożliwia także ten identyfikator GUID w aplikacji sieci web lub w szablonie wdrożenia aplikacji interfejsu API, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="22fb9-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="22fb9-222">Ten identyfikator GUID jest identyfikatorem GUID dzierżawy określonych ("identyfikator dzierżawy") i powinna być widoczna w tym adresem URL:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="22fb9-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="22fb9-223">Bez zapisywania zmian, Zamknij **ustawień usługi Azure Active Directory** bloku.</span><span class="sxs-lookup"><span data-stu-id="22fb9-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="22fb9-224">**Znajdź identyfikator klienta i Identyfikatora dzierżawcy tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API w klasycznym portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="22fb9-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="22fb9-225">W klasycznym portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="22fb9-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="22fb9-226">Wybierz katalog, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="22fb9-227">W **wyszukiwania** , Znajdź i wybierz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="22fb9-228">Na **Konfiguruj** karcie, skopiuj **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="22fb9-229">Po pobraniu Identyfikatora klienta w dolnej części **Konfiguruj** , wybierz pozycję **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="22fb9-230">Skopiuj adres URL dla **dokument metadanych usług federacyjnych**, a następnie przejdź do tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="22fb9-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="22fb9-231">W dokumencie metadanych można znaleźć katalogu głównego **identyfikator EntityDescriptor** element, który ma **entityID** atrybut w tym formularzu:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="22fb9-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="22fb9-232">Identyfikator GUID w tym atrybucie jest dzierżawy określonego identyfikatora GUID (identyfikator dzierżawcy).</span><span class="sxs-lookup"><span data-stu-id="22fb9-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="22fb9-233">Skopiuj identyfikator dzierżawcy i Zapisz ten identyfikator do użycia w część 3, a także do użycia w aplikacji sieci web lub aplikacji interfejsu API szablonu wdrażania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="22fb9-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="22fb9-234">Aby uzyskać więcej informacji zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="22fb9-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="22fb9-235">Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="22fb9-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="22fb9-236">Uwierzytelnianie i autoryzację w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="22fb9-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="22fb9-237">**Włącz uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="22fb9-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="22fb9-238">Nadal należy utworzyć tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, która różni się od tożsamości aplikacji dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="22fb9-239">Aby utworzyć tożsamość aplikacji, wykonaj poprzednie kroki w część 2 dla portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22fb9-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="22fb9-240">Możesz również wykonaj kroki opisane w części 1, ale pamiętaj korzystać z aplikacji sieci web lub aplikacji interfejsu API rzeczywiste `https://{URL}` dla **adres URL logowania** i **identyfikator URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="22fb9-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="22fb9-241">Z tych kroków należy zapisać identyfikator klienta i identyfikator dzierżawcy do użytku w szablonie wdrożenia aplikacji, a także dla część 3.</span><span class="sxs-lookup"><span data-stu-id="22fb9-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="22fb9-242">Podczas tworzenia tożsamość aplikacji usługi Azure AD dla twojej aplikacji sieci web lub aplikacji interfejsu API, musisz użyć portalu Azure lub klasycznego portalu Azure, zamiast programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22fb9-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="22fb9-243">Polecenia programu PowerShell nie skonfigurować wymagane uprawnienia do logowania się użytkowników do witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="22fb9-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="22fb9-244">Po pobraniu klienta identyfikator i identyfikator dzierżawy obejmują tych identyfikatorów jako subresource aplikacji sieci web lub aplikacji interfejsu API w szablonie wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="22fb9-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="22fb9-245">Automatyczne wdrażanie aplikacji sieci web puste i aplikacji logiki wraz z uwierzytelniania usługi Azure Active Directory [wyświetlić pełną szablonu tutaj](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), lub kliknij przycisk **wdrażanie na platformie Azure** tutaj:</span><span class="sxs-lookup"><span data-stu-id="22fb9-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="22fb9-246">[![Wdrażanie na platformie Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="22fb9-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="22fb9-247">Część 3: Wypełnić sekcję autoryzacji w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="22fb9-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="22fb9-248">Poprzedni szablon jest już w tej sekcji autoryzacji, konfigurowanie, ale są bezpośrednie tworzenie aplikacji logiki, należy dołączyć sekcji pełne autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="22fb9-249">Otwórz definicję aplikacji logiki w widoku kodu, przejdź do **HTTP** sekcji Akcja znaleźć **autoryzacji** , a następnie Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="22fb9-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="22fb9-250">Element</span><span class="sxs-lookup"><span data-stu-id="22fb9-250">Element</span></span> | <span data-ttu-id="22fb9-251">Opis</span><span class="sxs-lookup"><span data-stu-id="22fb9-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="22fb9-252">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="22fb9-252">tenant</span></span> |<span data-ttu-id="22fb9-253">Identyfikator GUID dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="22fb9-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="22fb9-254">grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="22fb9-254">audience</span></span> |<span data-ttu-id="22fb9-255">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-255">Required.</span></span> <span data-ttu-id="22fb9-256">Identyfikator GUID zasobu docelowego, który chcesz uzyskać dostęp — identyfikator klienta z tożsamości aplikacji dla aplikacji sieci web lub aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="22fb9-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="22fb9-257">clientId</span><span class="sxs-lookup"><span data-stu-id="22fb9-257">clientId</span></span> |<span data-ttu-id="22fb9-258">Identyfikator GUID dla klienta żąda dostępu — identyfikator klienta z tożsamość aplikacji dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="22fb9-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="22fb9-259">klucz tajny</span><span class="sxs-lookup"><span data-stu-id="22fb9-259">secret</span></span> |<span data-ttu-id="22fb9-260">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-260">Required.</span></span> <span data-ttu-id="22fb9-261">Klucz lub hasło z tożsamość aplikacji, gdy klient żąda token dostępu</span><span class="sxs-lookup"><span data-stu-id="22fb9-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="22fb9-262">type</span><span class="sxs-lookup"><span data-stu-id="22fb9-262">type</span></span> |<span data-ttu-id="22fb9-263">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="22fb9-263">The authentication type.</span></span> <span data-ttu-id="22fb9-264">Wartość dla uwierzytelniania ActiveDirectoryOAuth jest `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="22fb9-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="22fb9-265">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="22fb9-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="22fb9-266">Bezpieczne wywołania interfejsu API przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="22fb9-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="22fb9-267">Uwierzytelnianie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="22fb9-267">Certificate authentication</span></span>

<span data-ttu-id="22fb9-268">Aby sprawdzić poprawność żądań przychodzących od aplikacji logiki do aplikacji sieci web lub aplikacji interfejsu API, można użyć certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="22fb9-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="22fb9-269">Aby skonfigurować swój kod, Dowiedz się [jak skonfigurować uwierzytelnianie wzajemne TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="22fb9-270">W **autoryzacji** sekcji, Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="22fb9-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="22fb9-271">Element</span><span class="sxs-lookup"><span data-stu-id="22fb9-271">Element</span></span> | <span data-ttu-id="22fb9-272">Opis</span><span class="sxs-lookup"><span data-stu-id="22fb9-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="22fb9-273">type</span><span class="sxs-lookup"><span data-stu-id="22fb9-273">type</span></span> |<span data-ttu-id="22fb9-274">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-274">Required.</span></span> <span data-ttu-id="22fb9-275">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="22fb9-275">The authentication type.</span></span> <span data-ttu-id="22fb9-276">Dla certyfikatów klienta SSL, wartość musi być `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="22fb9-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="22fb9-277">hasło</span><span class="sxs-lookup"><span data-stu-id="22fb9-277">password</span></span> |<span data-ttu-id="22fb9-278">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-278">Required.</span></span> <span data-ttu-id="22fb9-279">Hasło do uzyskiwania dostępu do certyfikatu klienta (plik PFX)</span><span class="sxs-lookup"><span data-stu-id="22fb9-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="22fb9-280">PFX</span><span class="sxs-lookup"><span data-stu-id="22fb9-280">pfx</span></span> |<span data-ttu-id="22fb9-281">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-281">Required.</span></span> <span data-ttu-id="22fb9-282">Zawartość algorytmem Base64 certyfikatu klienta (plik PFX)</span><span class="sxs-lookup"><span data-stu-id="22fb9-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="22fb9-283">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="22fb9-283">Basic authentication</span></span>

<span data-ttu-id="22fb9-284">Można sprawdzić poprawności przychodzących żądań od aplikacji logiki do aplikacji sieci web lub aplikacji interfejsu API, można użyć uwierzytelnianie podstawowe, takie jak nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="22fb9-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="22fb9-285">Uwierzytelnianie podstawowe jest wspólnego wzorca i może uwierzytelnianie w dowolnym języku używanym do budowania aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22fb9-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="22fb9-286">W **autoryzacji** sekcji, Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="22fb9-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="22fb9-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="22fb9-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="22fb9-288">Element</span><span class="sxs-lookup"><span data-stu-id="22fb9-288">Element</span></span> | <span data-ttu-id="22fb9-289">Opis</span><span class="sxs-lookup"><span data-stu-id="22fb9-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22fb9-290">type</span><span class="sxs-lookup"><span data-stu-id="22fb9-290">type</span></span> |<span data-ttu-id="22fb9-291">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-291">Required.</span></span> <span data-ttu-id="22fb9-292">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="22fb9-292">The authentication type.</span></span> <span data-ttu-id="22fb9-293">W przypadku uwierzytelniania podstawowego musi być wartością `Basic`.</span><span class="sxs-lookup"><span data-stu-id="22fb9-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="22fb9-294">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="22fb9-294">username</span></span> |<span data-ttu-id="22fb9-295">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-295">Required.</span></span> <span data-ttu-id="22fb9-296">Nazwa użytkownika do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="22fb9-296">The username for authentication</span></span> |
| <span data-ttu-id="22fb9-297">hasło</span><span class="sxs-lookup"><span data-stu-id="22fb9-297">password</span></span> |<span data-ttu-id="22fb9-298">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="22fb9-298">Required.</span></span> <span data-ttu-id="22fb9-299">Hasło do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="22fb9-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="22fb9-300">Azure uwierzytelniania usługi Active Directory przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="22fb9-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="22fb9-301">Domyślnie uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure nie zapewnia precyzyjną autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="22fb9-302">Na przykład to uwierzytelnianie blokuje interfejsu API do określonych dzierżawy, a nie do określonego użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22fb9-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="22fb9-303">Aby ograniczyć dostęp do interfejsu API do aplikacji logiki do kodu, Wyodrębnij nagłówek, który ma tokenu web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="22fb9-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="22fb9-304">Sprawdź tożsamość obiektu wywołującego i odrzucanie żądań, które nie są zgodne.</span><span class="sxs-lookup"><span data-stu-id="22fb9-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="22fb9-305">Kontynuowanie, aby zaimplementować uwierzytelnianie całkowicie w swoim własnym kodem, a nie za pomocą portalu Azure, Dowiedz się jak [uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="22fb9-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="22fb9-306">Aby utworzyć tożsamość aplikacji dla aplikacji logiki i użyć tej tożsamości do wywołania interfejsu API, należy wykonać poprzednie kroki.</span><span class="sxs-lookup"><span data-stu-id="22fb9-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22fb9-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22fb9-307">Next steps</span></span>

* [<span data-ttu-id="22fb9-308">Sprawdź wydajność aplikacji logiki z dzienników diagnostycznych i alerty</span><span class="sxs-lookup"><span data-stu-id="22fb9-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)