---
title: "aaaDeploy, wywołaj i uwierzytelniania sieci web API i interfejsów API REST dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="1c8ac-104">Wdrożenia, wywołaj i uwierzytelniania niestandardowych interfejsów API łączników dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="1c8ac-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="1c8ac-105">Po [Tworzenie niestandardowych interfejsów API](./logic-apps-create-api-app.md) zawierających akcji lub wyzwalaczy toouse logiki aplikacji przepływy pracy, swoje interfejsy API należy wdrożyć przed wywołaniem je.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="1c8ac-106">I chociaż jakiegokolwiek interfejsu API można wywołać z aplikacji logiki, aby hello najlepsze wyniki, Dodaj [Swagger metadanych](http://swagger.io/specification/) opisujący Twój interfejs API operacji i parametry.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="1c8ac-107">Ten plik struktury Swagger pomaga interfejsu API działa lepiej i łatwo zintegrować z usługą logic apps.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="1c8ac-108">Można wdrożyć swoje interfejsy API jako [sieci web apps](../app-service-web/app-service-web-overview.md), ale warto wdrożyć swoje interfejsy API jako [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md), które mogą ułatwić zadania podczas kompilacji, hosta i korzystanie z interfejsów API w chmurze hello i lokalnie.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="1c8ac-109">Nie można znaleźć toochange dowolny kod swoje interfejsy API — wystarczy go wdrożyć aplikację interfejsu API tooan kodu.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="1c8ac-110">Swoje interfejsy API mogą być hostowane na [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md), platformy jako — usługa (PaaS) oferta zapewnia sposoby najlepsze najprostszym i najbardziej skalowalny hello do obsługi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="1c8ac-111">wywołania tooauthenticate z tooyour aplikacje logiki interfejsów API, można ustawić usługę Azure Active Directory w hello portalu Azure dzięki czemu nie trzeba tooupdate kodu.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="1c8ac-112">Lub może wymagać i wymusić uwierzytelnianie za pomocą kodu Twój interfejs API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="1c8ac-113">Wdrażanie aplikacji sieci web lub aplikacji interfejsu API interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1c8ac-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="1c8ac-114">Przed wywołaniem niestandardowego interfejsu API z aplikacji logiki, należy wdrożyć jako aplikacji sieci web lub tooAzure aplikacji interfejsu API usługi aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="1c8ac-115">Ponadto toomake dokumentu Swagger mógłby odczytać hello projektanta aplikacji logiki, ustaw właściwości definicji hello interfejsu API i Włącz [współużytkowanie zasobów między źródłami (CORS) do udostępniania](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) dla aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="1c8ac-116">W portalu Azure hello wybierz aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="1c8ac-117">W bloku hello, który zostanie otwarty, w obszarze **interfejsu API**, wybierz **definicji interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="1c8ac-118">Zestaw hello **lokalizacji definicji interfejsu API** toohello adres URL pliku swagger.json.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="1c8ac-119">Zwykle adres URL hello pojawia się w następującym formacie:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="1c8ac-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Plik tooSwagger łącza do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="1c8ac-121">W obszarze **interfejsu API**, wybierz **CORS**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="1c8ac-122">Ustaw hello zasad CORS dla **dozwolone źródła** za**"*"** (Zezwalaj na wszystkie).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="1c8ac-123">Ustawienie to pozwala żądania przy użyciu projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-123">This setting permits requests from Logic App Designer.</span></span>

   ![Zezwala na żądania z projektanta aplikacji logiki tooyour niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="1c8ac-125">Aby uzyskać więcej informacji zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="1c8ac-126">Dodaj metadane programu Swagger dla interfejsów API sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c8ac-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="1c8ac-127">Wdrażanie programu ASP.NET web API tooAzure usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="1c8ac-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="1c8ac-128">Wywoływanie niestandardowego interfejsu API z logiki przepływów pracy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1c8ac-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="1c8ac-129">Po skonfigurowaniu właściwości definicji hello interfejsu API i mechanizmu CORS, niestandardowego interfejsu API wyzwalacze i akcje powinien być możliwy do tooinclude w przepływie pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="1c8ac-130">tooview hello witryn sieci Web programu Swagger URL, możesz wyszukać subskrypcji witryny sieci Web w hello projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="1c8ac-131">Dostępne akcje tooview i dane wejściowe, wskazując dokumentu Swagger, użyj hello [HTTP + Swagger akcji](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="1c8ac-132">toocall jakiegokolwiek interfejsu API, łącznie z interfejsów API, które nie mają lub udostępnianie dokumentu Swagger, zawsze można utworzyć żądania z hello [akcji HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="1c8ac-133">Niestandardowy interfejs API tooyour wywołania uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1c8ac-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="1c8ac-134">Możesz zabezpieczyć wywołania tooyour niestandardowego interfejsu API w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="1c8ac-135">[Nie zmian w kodzie](#no-code): interfejs API ochrony [usługi Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) za pośrednictwem hello portalu Azure, dlatego nie masz tooupdate kodu lub ponownego wdrażania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1c8ac-136">Domyślnie hello uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure hello nie zapewnia precyzyjną autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="1c8ac-137">Na przykład to uwierzytelnianie blokuje toojust Twojego interfejsu API określonego dzierżawy, nie tooa określonego użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="1c8ac-138">[Zaktualizuj kod Twój interfejs API](#update-code): ochrona interfejsu API przez wymuszenie [uwierzytelnianie certyfikatu](#certificate), [uwierzytelnianie podstawowe](#basic), lub [uwierzytelniania usługi Azure AD](#azure-ad-code) za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="1c8ac-139">Uwierzytelniania interfejsu API tooyour wywołania bez zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="1c8ac-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="1c8ac-140">Poniżej przedstawiono ogólne kroki hello tej metody:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="1c8ac-141">Utwórz dwa [tożsamości aplikacji usługi Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): jeden dla aplikacji logiki i jeden dla aplikacji sieci web (lub aplikacji interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="1c8ac-142">tooauthenticate tooyour wywołań interfejsu API, Użyj poświadczeń hello (identyfikator klienta i klucz tajny) dla hello [nazwy głównej usługi](../app-service-api/app-service-api-dotnet-service-principal-auth.md) która jest skojarzona z hello tożsamość aplikacji usługi Azure AD dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="1c8ac-143">Dołącz aplikacji hello identyfikatorów definicję aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="1c8ac-144">Część 1: Tworzenie aplikacji logiki tożsamość aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ac-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="1c8ac-145">Twoja aplikacja logiki korzysta z tego tooauthenticate tożsamość aplikacji usługi Azure AD w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="1c8ac-146">Masz tylko tooset się tej tożsamości jeden raz dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="1c8ac-147">Na przykład można wybrać toouse hello tej samej tożsamości dla wszystkich aplikacji logiki, mimo że można utworzyć unikatowych tożsamości dla każdej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="1c8ac-148">Możesz skonfigurować te tożsamości w hello portalu Azure, [klasycznego portalu Azure](#app-identity-logic-classic), lub użyj [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="1c8ac-149">**Utwórz tożsamość aplikacji hello aplikacji logiki w hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="1c8ac-150">W hello [portalu Azure](https://portal.azure.com "https://portal.azure.com"), wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="1c8ac-151">Upewnij się, że jesteś w hello tym samym katalogu co aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="1c8ac-152">katalogi tooswitch kliknij profilu i wybierz inny katalog.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="1c8ac-153">Lub wybierz **omówienie** > **katalogu przełącznika**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="1c8ac-154">Menu hello katalogu w obszarze **Zarządzaj**, wybierz **rejestracji aplikacji** > **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="1c8ac-155">Domyślnie listy rejestracji aplikacji hello zawiera wszystkich rejestracji aplikacji w katalogu.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="1c8ac-156">Wybierz tylko aplikacji rejestracji, toohello pola wyszukiwania i tooview **Moje aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Tworzenie nowej rejestracji aplikacji](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="1c8ac-158">Nadaj nazwę tożsamości aplikacji, pozostaw **typu aplikacji** ustawić także**aplikacji sieci Web / interfejsu API**, podaj unikatowy ciąg w formacie domeny dla **adres URL logowania**i wybierz polecenie  **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Podaj nazwę i logowania jednokrotnego adres URL dla tożsamości aplikacji](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="1c8ac-160">tożsamość aplikacji Hello utworzonej dla aplikacji logiki teraz pojawia się na liście rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Tożsamość aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="1c8ac-162">Na liście rejestracji aplikacji hello wybierz nowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="1c8ac-163">Skopiuj i Zapisz hello **identyfikator aplikacji** toouse jako Witaj "identyfikator klienta" aplikacji logiki w część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Skopiuj i Zapisz identyfikator aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="1c8ac-165">Jeśli ustawienia tożsamość aplikacji nie są widoczne, wybierz **ustawienia** lub **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="1c8ac-166">W obszarze **dostępu do interfejsu API**, wybierz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="1c8ac-167">W obszarze **opis**, podaj nazwę klucza.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="1c8ac-168">W obszarze **Expires**, wybierz czas trwania dla klucza.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="1c8ac-169">Witaj klucz, który tworzysz działa jako tożsamość aplikacji hello "tajny" lub hasła do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Utwórz klucz tożsamości aplikacji logiki](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="1c8ac-171">Na pasku narzędzi hello, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="1c8ac-172">W obszarze **wartość**, klucz zostanie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="1c8ac-173">**Upewnij się, że toocopy i zapisać klucz** do późniejszego użycia, ponieważ klucz hello jest ukryty wychodząc hello klucza bloku.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="1c8ac-174">Po skonfigurowaniu aplikacji logiki w części 3 Określ ten klucz jako Witaj "tajny" lub hasło.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Skopiuj i Zapisz klucz do użycia później](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="1c8ac-176">**Utwórz tożsamość aplikacji hello aplikacji logiki w hello klasycznego portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="1c8ac-177">W hello klasycznego portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="1c8ac-178">Wybierz hello tym samym katalogu, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="1c8ac-179">Na powitania **aplikacji** , wybierz pozycję **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="1c8ac-180">Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **dalej** (Strzałka w prawo).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="1c8ac-181">W obszarze **właściwości aplikacji**, podaj unikatowy ciąg w formacie domeny **adres URL logowania** i **identyfikator URI aplikacji**i wybierz polecenie **Complete** (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="1c8ac-182">Na powitania **Konfiguruj** karcie, skopiuj i Zapisz hello **identyfikator klienta** dla Twojego toouse aplikacji logiki w część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="1c8ac-183">W obszarze **klucze**, otwórz hello **wybierz czas trwania** listy.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="1c8ac-184">Wybierz czas trwania dla klucza.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-184">Select a duration for your key.</span></span>

   <span data-ttu-id="1c8ac-185">Witaj klucz, który tworzysz działa jako tożsamość aplikacji hello "tajny" lub hasła do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="1c8ac-186">U dołu hello hello strony, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="1c8ac-187">Toowait może mieć kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="1c8ac-188">W obszarze **klucze**, upewnij się, że toocopy i zapisać klucz hello, który pojawi się teraz.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="1c8ac-189">Po skonfigurowaniu aplikacji logiki w części 3 Określ ten klucz jako Witaj "tajny" lub hasło.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="1c8ac-190">Aby uzyskać więcej informacji, Dowiedz się, jak za [skonfigurować Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="1c8ac-191">**Utwórz tożsamość aplikacji hello aplikacji logiki w programie PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="1c8ac-192">Można wykonać tego zadania za pomocą usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="1c8ac-193">W programie PowerShell uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="1c8ac-194">Upewnij się, że hello toocopy **identyfikator dzierżawcy** hello (identyfikator GUID dla dzierżawy usługi Azure AD), **identyfikator aplikacji**i hello hasła, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="1c8ac-195">Aby uzyskać więcej informacji, Dowiedz się, jak za [utworzyć nazwy głównej usługi za pomocą programu PowerShell tooaccess zasobów](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="1c8ac-196">Część 2: Tworzenie tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1c8ac-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="1c8ac-197">Jeśli aplikację sieci web lub aplikacji interfejsu API jest już wdrożone, należy włączyć uwierzytelnianie i Utwórz tożsamość aplikacji hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="1c8ac-198">W przeciwnym razie można [włączyć uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="1c8ac-199">**Utwórz tożsamość aplikacji hello i włączyć uwierzytelnianie w portalu Azure do wdrożonych aplikacji hello**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="1c8ac-200">W hello [portalu Azure](https://portal.azure.com "https://portal.azure.com"), Znajdź i wybierz aplikację sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="1c8ac-201">W obszarze **ustawienia**, wybierz **uwierzytelniania/autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="1c8ac-202">W obszarze **aplikacji uwierzytelniania usługi**, Włącz uwierzytelnianie **na**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="1c8ac-203">W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Włączanie uwierzytelniania](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="1c8ac-205">Teraz należy utworzyć tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="1c8ac-206">Na powitania **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** za**Express**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="1c8ac-207">Wybierz **Utwórz nową aplikację usługi AD**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="1c8ac-208">Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Utwórz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="1c8ac-210">Na powitania **uwierzytelniania / autoryzacji bloku**, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="1c8ac-211">Teraz należy znaleźć hello identyfikator klienta i Identyfikatorem dzierżawy tożsamości aplikacji hello, który został skojarzony z aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="1c8ac-212">Należy użyć tych identyfikatorów w część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="1c8ac-213">Dlatego kontynuować czynności w celu hello portalu Azure lub [klasycznego portalu Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="1c8ac-214">**Znajdź identyfikator klienta tożsamości aplikacji i Identyfikatorem dzierżawy dla aplikacji sieci web lub aplikacji interfejsu API w hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="1c8ac-215">W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Wybierz polecenie "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="1c8ac-217">Na powitania **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** za**zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="1c8ac-218">Kopiuj hello **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="1c8ac-219">Jeśli **identyfikator klienta** i **adres Url wystawcy** nie są wyświetlane, spróbuj odświeżyć hello portalu Azure i powtórz krok 1.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="1c8ac-220">W obszarze **adres Url wystawcy**, skopiuj i Zapisz tylko hello identyfikatora GUID dla część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="1c8ac-221">Umożliwia także ten identyfikator GUID w aplikacji sieci web lub w szablonie wdrożenia aplikacji interfejsu API, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="1c8ac-222">Ten identyfikator GUID jest identyfikatorem GUID dzierżawy określonych ("identyfikator dzierżawy") i powinna być widoczna w tym adresem URL:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="1c8ac-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="1c8ac-223">Bez zapisywania zmian, zamknij hello **ustawień usługi Azure Active Directory** bloku.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="1c8ac-224">**Znajdź identyfikator klienta tożsamości aplikacji i Identyfikatorem dzierżawy dla aplikacji sieci web lub aplikacji interfejsu API w hello klasycznego portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="1c8ac-225">W hello klasycznego portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="1c8ac-226">Wybierz katalog hello, której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="1c8ac-227">W hello **wyszukiwania** , Znajdź i zaznacz hello tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="1c8ac-228">Na powitania **Konfiguruj** kartę, hello kopiowania **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="1c8ac-229">Po pobraniu Identyfikatora klienta hello, u dołu hello hello **Konfiguruj** , wybierz pozycję **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="1c8ac-230">Skopiuj adres URL hello **dokument metadanych usług federacyjnych**, a następnie przejdź do adresu URL toothat.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="1c8ac-231">W dokumencie metadanych hello otwiera, Znajdź głównego hello **identyfikator EntityDescriptor** element, który ma **entityID** atrybut w tym formularzu:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="1c8ac-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="1c8ac-232">Witaj identyfikator GUID w tym atrybucie jest dzierżawy określonego identyfikatora GUID (identyfikator dzierżawcy).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="1c8ac-233">Skopiuj identyfikator dzierżawcy hello i Zapisz ten identyfikator do użycia w część 3 i toouse w aplikacji sieci web lub aplikacji interfejsu API szablonu wdrażania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="1c8ac-234">Aby uzyskać więcej informacji zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="1c8ac-235">Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1c8ac-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="1c8ac-236">Uwierzytelnianie i autoryzację w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1c8ac-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="1c8ac-237">**Włącz uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="1c8ac-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="1c8ac-238">Nadal należy utworzyć tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, która różni się od tożsamości aplikacji hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="1c8ac-239">tożsamość aplikacji hello toocreate, hello wykonaj poprzednie kroki w część 2 dla hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="1c8ac-240">Możesz również kroków hello w części 1, ale upewnij się, że toouse Twojej aplikacji sieci web lub aplikacji interfejsu API rzeczywiste `https://{URL}` dla **adres URL logowania** i **identyfikator URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="1c8ac-241">Z tych kroków masz toosave zarówno powitania klienta identyfikator i identyfikator dzierżawcy do użytku w szablonie wdrożenia aplikacji, a także dla część 3.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="1c8ac-242">Podczas tworzenia tożsamości aplikacji hello Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, należy użyć hello portalu Azure lub klasycznego portalu Azure, a nie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="1c8ac-243">polecenia programu PowerShell Hello nie skonfigurować hello wymagane uprawnienia toosign użytkowników do witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="1c8ac-244">Po uzyskaniu hello Identyfikatora klienta oraz Identyfikatora dzierżawy obejmują tych identyfikatorów jako subresource aplikacji sieci web lub aplikacji interfejsu API w szablonie wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="1c8ac-245">tooautomatically wdrażanie aplikacji sieci web puste i aplikacji logiki wraz z uwierzytelniania usługi Azure Active Directory [Wyświetl hello pełny szablon tutaj](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), lub kliknij przycisk **wdrażanie tooAzure** tutaj:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="1c8ac-246">[![Wdrażanie tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1c8ac-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="1c8ac-247">Część 3: Wypełnić hello autoryzacji części aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1c8ac-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="1c8ac-248">Hello poprzedni szablon jest już w tej sekcji autoryzacji, konfigurowanie, ale są bezpośrednie tworzenie aplikacji logiki hello, należy dołączyć hello pełni autoryzowane sekcji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="1c8ac-249">Otwórz definicję aplikacji logiki w widoku kodu, przejdź toohello **HTTP** sekcji akcja, Znajdź hello **autoryzacji** , a następnie Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="1c8ac-250">Element</span><span class="sxs-lookup"><span data-stu-id="1c8ac-250">Element</span></span> | <span data-ttu-id="1c8ac-251">Opis</span><span class="sxs-lookup"><span data-stu-id="1c8ac-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="1c8ac-252">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="1c8ac-252">tenant</span></span> |<span data-ttu-id="1c8ac-253">Witaj identyfikatora GUID dla dzierżawcy hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ac-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="1c8ac-254">grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="1c8ac-254">audience</span></span> |<span data-ttu-id="1c8ac-255">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-255">Required.</span></span> <span data-ttu-id="1c8ac-256">Witaj identyfikatora GUID dla zasobu docelowego hello, które mają tooaccess - hello identyfikator klienta z hello tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1c8ac-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="1c8ac-257">clientId</span><span class="sxs-lookup"><span data-stu-id="1c8ac-257">clientId</span></span> |<span data-ttu-id="1c8ac-258">Witaj identyfikatora GUID dla klienta hello żądania access - hello identyfikator klienta z tożsamości aplikacji hello aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1c8ac-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="1c8ac-259">klucz tajny</span><span class="sxs-lookup"><span data-stu-id="1c8ac-259">secret</span></span> |<span data-ttu-id="1c8ac-260">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-260">Required.</span></span> <span data-ttu-id="1c8ac-261">Witaj klucza lub hasła z tożsamości aplikacji hello powitania klienta żąda hello token dostępu</span><span class="sxs-lookup"><span data-stu-id="1c8ac-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="1c8ac-262">type</span><span class="sxs-lookup"><span data-stu-id="1c8ac-262">type</span></span> |<span data-ttu-id="1c8ac-263">Typ uwierzytelniania Hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-263">hello authentication type.</span></span> <span data-ttu-id="1c8ac-264">W przypadku uwierzytelniania ActiveDirectoryOAuth wartość hello jest `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="1c8ac-265">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="1c8ac-266">Bezpieczne wywołania interfejsu API przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="1c8ac-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="1c8ac-267">Uwierzytelnianie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="1c8ac-267">Certificate authentication</span></span>

<span data-ttu-id="1c8ac-268">toovalidate hello przychodzących żądań od aplikacji sieci web tooyour aplikacji logiki lub aplikacji interfejsu API, można użyć certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="1c8ac-269">tooset się kodu, Dowiedz się [jak wzajemnego uwierzytelniania TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="1c8ac-270">W hello **autoryzacji** sekcji, Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="1c8ac-271">Element</span><span class="sxs-lookup"><span data-stu-id="1c8ac-271">Element</span></span> | <span data-ttu-id="1c8ac-272">Opis</span><span class="sxs-lookup"><span data-stu-id="1c8ac-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="1c8ac-273">type</span><span class="sxs-lookup"><span data-stu-id="1c8ac-273">type</span></span> |<span data-ttu-id="1c8ac-274">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-274">Required.</span></span> <span data-ttu-id="1c8ac-275">Typ uwierzytelniania Hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-275">hello authentication type.</span></span> <span data-ttu-id="1c8ac-276">W przypadku certyfikatów SSL klienta hello wartość musi być `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="1c8ac-277">hasło</span><span class="sxs-lookup"><span data-stu-id="1c8ac-277">password</span></span> |<span data-ttu-id="1c8ac-278">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-278">Required.</span></span> <span data-ttu-id="1c8ac-279">hasło Hello dla uzyskiwania dostępu do certyfikatu klienta hello (plik PFX)</span><span class="sxs-lookup"><span data-stu-id="1c8ac-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="1c8ac-280">PFX</span><span class="sxs-lookup"><span data-stu-id="1c8ac-280">pfx</span></span> |<span data-ttu-id="1c8ac-281">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-281">Required.</span></span> <span data-ttu-id="1c8ac-282">Zawartość algorytmem Base64 certyfikatu klienta hello (plik PFX)</span><span class="sxs-lookup"><span data-stu-id="1c8ac-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="1c8ac-283">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="1c8ac-283">Basic authentication</span></span>

<span data-ttu-id="1c8ac-284">toovalidate żądań przychodzących od aplikacji sieci web tooyour aplikacji logiki lub aplikacji interfejsu API, można użyć uwierzytelniania podstawowego, takie jak nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="1c8ac-285">Uwierzytelnianie podstawowe jest wspólnym wzorcem i użyć tego uwierzytelnienia w dowolnym toobuild język używany aplikacji sieci web lub aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="1c8ac-286">W hello **autoryzacji** sekcji, Dołącz tę linię:</span><span class="sxs-lookup"><span data-stu-id="1c8ac-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="1c8ac-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="1c8ac-288">Element</span><span class="sxs-lookup"><span data-stu-id="1c8ac-288">Element</span></span> | <span data-ttu-id="1c8ac-289">Opis</span><span class="sxs-lookup"><span data-stu-id="1c8ac-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c8ac-290">type</span><span class="sxs-lookup"><span data-stu-id="1c8ac-290">type</span></span> |<span data-ttu-id="1c8ac-291">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-291">Required.</span></span> <span data-ttu-id="1c8ac-292">Typ uwierzytelniania Hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-292">hello authentication type.</span></span> <span data-ttu-id="1c8ac-293">W przypadku uwierzytelniania podstawowego hello wartość musi być `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="1c8ac-294">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="1c8ac-294">username</span></span> |<span data-ttu-id="1c8ac-295">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-295">Required.</span></span> <span data-ttu-id="1c8ac-296">Witaj użytkownika dla uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1c8ac-296">hello username for authentication</span></span> |
| <span data-ttu-id="1c8ac-297">hasło</span><span class="sxs-lookup"><span data-stu-id="1c8ac-297">password</span></span> |<span data-ttu-id="1c8ac-298">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-298">Required.</span></span> <span data-ttu-id="1c8ac-299">Witaj hasła do uwierzytelnienia</span><span class="sxs-lookup"><span data-stu-id="1c8ac-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="1c8ac-300">Azure uwierzytelniania usługi Active Directory przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="1c8ac-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="1c8ac-301">Domyślnie hello uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure hello nie zapewnia precyzyjną autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="1c8ac-302">Na przykład to uwierzytelnianie blokuje toojust Twojego interfejsu API określonego dzierżawy, nie tooa określonego użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="1c8ac-303">Aplikacja logiki tooyour dostępu toorestrict interfejsu API za pomocą kodu, Wyodrębnij nagłówek hello tokenu web hello JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="1c8ac-304">Sprawdź tożsamość obiektu wywołującego hello i odrzucanie żądań, które nie są zgodne.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="1c8ac-305">Kontynuowanie tooimplement to uwierzytelnianie w całości własnego kodu i nie hello Użyj portalu Azure, Dowiedz się, jak za [uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ac-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="1c8ac-306">tożsamość aplikacji dla aplikacji logiki toocreate i korzystanie z interfejsu API toocall tej tożsamości, należy wykonać poprzednie kroki hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ac-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c8ac-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c8ac-307">Next steps</span></span>

* [<span data-ttu-id="1c8ac-308">Sprawdź wydajność aplikacji logiki z dzienników diagnostycznych i alerty</span><span class="sxs-lookup"><span data-stu-id="1c8ac-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)