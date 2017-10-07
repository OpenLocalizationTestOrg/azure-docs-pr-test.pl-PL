---
title: "punkty końcowe REST aaaCall z HTTP + Swagger connector dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Połącz tooREST punktów końcowych z aplikacji logiki za pośrednictwem programu Swagger z hello HTTP + łącznika programu Swagger"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="88026-103">Rozpoczynanie pracy z Witaj HTTP + akcji struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="88026-104">Można utworzyć punkt końcowy REST tooany łącznika najwyższej jakości za pomocą [dokumentu Swagger](https://swagger.io) korzystając Witaj HTTP + Swagger działania w przepływie pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="88026-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="88026-105">Toocall aplikacje logiki można rozszerzać dowolnego punktu końcowego REST o najwyższej jakości środowisko projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="88026-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="88026-106">aplikacje logiki toocreate z łączników, zobacz temat toolearn [Utwórz nową aplikację logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="88026-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="88026-107">Użyj protokołu HTTP + Swagger jako wyzwalacz lub akcji</span><span class="sxs-lookup"><span data-stu-id="88026-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="88026-108">Witaj HTTP + Swagger trigger i action pracy hello takie same jak hello [akcji HTTP](connectors-native-http.md) choć zapewnia lepsze środowisko pracy w Projektancie aplikacji logiki w przypadku wystawianego hello interfejsu API struktury i dane wyjściowe z hello [Swagger metadanych](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="88026-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="88026-109">Witaj HTTP + łącznika struktury Swagger można również używane jako wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="88026-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="88026-110">Tooimplement wyzwalacz sondowania, należy wykonać sondowanie hello wzorzec, który jest opisany w [Tworzenie niestandardowych interfejsów API toocall innych interfejsów API, usług i systemy z aplikacji logiki](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="88026-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="88026-111">Dowiedz się więcej o [logiki aplikacji wyzwalacze i akcje](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88026-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="88026-112">Poniżej przedstawiono przykład sposobu toouse hello HTTP + Swagger operacji jako akcja w przepływie pracy w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="88026-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="88026-113">Wybierz hello **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88026-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="88026-114">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="88026-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="88026-115">W hello akcji wyszukiwania wpisz **swagger** toolist Witaj HTTP + akcji struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="88026-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Wybierz opcję HTTP + Swagger akcji](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="88026-117">Wpisz adres URL dokumentu Swagger hello:</span><span class="sxs-lookup"><span data-stu-id="88026-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="88026-118">toowork z hello projektanta aplikacji logiki, hello adres URL musi być punkt końcowy HTTPS i włączono CORS.</span><span class="sxs-lookup"><span data-stu-id="88026-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="88026-119">Jeśli dokumentu Swagger hello nie spełnia tego wymagania, możesz użyć [magazynu Azure z włączonym mechanizmem CORS](#hosting-swagger-from-storage) toostore hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="88026-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="88026-120">Kliknij przycisk **dalej** tooread i renderowania z hello dokumentu Swagger.</span><span class="sxs-lookup"><span data-stu-id="88026-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="88026-121">Dodaj w żadnych parametrów, które są wymagane dla wywołania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="88026-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Zakończenie akcji HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="88026-123">toosave i publikowanie aplikacji logiki, kliknij przycisk **zapisać** na pasku narzędzi projektanta.</span><span class="sxs-lookup"><span data-stu-id="88026-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="88026-124">Swagger hosta z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="88026-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="88026-125">Możesz tooreference dokumentu Swagger nie jest obsługiwany lub który nie spełnia wymagania zabezpieczeń i cross-origin hello hello projektanta.</span><span class="sxs-lookup"><span data-stu-id="88026-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="88026-126">tooresolve ten problem, można przechowywać dokumentu Swagger hello w usłudze Azure Storage i Włącz dokument hello tooreference CORS.</span><span class="sxs-lookup"><span data-stu-id="88026-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="88026-127">Poniżej przedstawiono toocreate kroki hello, konfigurowanie i przechowywanie dokumentów struktury Swagger w usłudze Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="88026-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="88026-128">[Utwórz konto magazynu platformy Azure z magazynu obiektów Blob Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="88026-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="88026-129">tooperform ten krok, ustawianie uprawnień zbyt**dostępu publicznego**.</span><span class="sxs-lookup"><span data-stu-id="88026-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="88026-130">Włącz CORS na powitania obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="88026-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="88026-131">tooautomatically tego ustawienia, można użyć [ten skrypt programu PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="88026-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="88026-132">Przekaż hello Swagger pliku toohello blob.</span><span class="sxs-lookup"><span data-stu-id="88026-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="88026-133">Ten krok można wykonać z hello [portalu Azure](https://portal.azure.com) lub z narzędzia, takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="88026-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="88026-134">Odwołuje się do dokumentu toohello łącza HTTPS w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="88026-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="88026-135">łącze Hello używany format to:</span><span class="sxs-lookup"><span data-stu-id="88026-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="88026-136">Szczegóły techniczne</span><span class="sxs-lookup"><span data-stu-id="88026-136">Technical details</span></span>
<span data-ttu-id="88026-137">Poniżej przedstawiono hello szczegółów hello wyzwalacze i akcje tego HTTP + Swagger łącznik obsługuje.</span><span class="sxs-lookup"><span data-stu-id="88026-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="88026-138">HTTP + wyzwalaczy programu Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="88026-139">Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="88026-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="88026-140">Dowiedz się więcej na temat wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="88026-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="88026-141">Witaj HTTP + Swagger łącznik ma jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="88026-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="88026-142">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="88026-142">Trigger</span></span> | <span data-ttu-id="88026-143">Opis</span><span class="sxs-lookup"><span data-stu-id="88026-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88026-144">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-144">HTTP + Swagger</span></span> |<span data-ttu-id="88026-145">Wykonaj wywołanie HTTP i zwróć hello zawartości odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88026-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="88026-146">HTTP + akcje programu Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="88026-147">Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="88026-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="88026-148">Dowiedz się więcej na temat akcji.</span><span class="sxs-lookup"><span data-stu-id="88026-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="88026-149">Witaj HTTP + Swagger łącznik ma jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="88026-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="88026-150">Akcja</span><span class="sxs-lookup"><span data-stu-id="88026-150">Action</span></span> | <span data-ttu-id="88026-151">Opis</span><span class="sxs-lookup"><span data-stu-id="88026-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88026-152">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-152">HTTP + Swagger</span></span> |<span data-ttu-id="88026-153">Wykonaj wywołanie HTTP i zwróć hello zawartości odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88026-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="88026-154">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="88026-154">Action details</span></span>
<span data-ttu-id="88026-155">Witaj HTTP + Swagger łącznika jest dostarczany z jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="88026-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="88026-156">Poniżej znajdują się informacje o każdej akcji hello, wymaganych i opcjonalnych pól wejściowych i hello odpowiadającego szczegóły danych wyjściowych, które są skojarzone z ich użycia.</span><span class="sxs-lookup"><span data-stu-id="88026-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="88026-157">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="88026-157">HTTP + Swagger</span></span>
<span data-ttu-id="88026-158">Przesyłania żądania wychodzącego HTTP pomocy metadanych struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="88026-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="88026-159">Znak gwiazdki (*) oznacza wymaganego pola.</span><span class="sxs-lookup"><span data-stu-id="88026-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="88026-160">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="88026-160">Display name</span></span> | <span data-ttu-id="88026-161">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="88026-161">Property name</span></span> | <span data-ttu-id="88026-162">Opis</span><span class="sxs-lookup"><span data-stu-id="88026-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88026-163">Metoda *</span><span class="sxs-lookup"><span data-stu-id="88026-163">Method*</span></span> |<span data-ttu-id="88026-164">— Metoda</span><span class="sxs-lookup"><span data-stu-id="88026-164">method</span></span> |<span data-ttu-id="88026-165">Toouse zlecenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="88026-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="88026-166">IDENTYFIKATOR URI *</span><span class="sxs-lookup"><span data-stu-id="88026-166">URI*</span></span> |<span data-ttu-id="88026-167">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="88026-167">uri</span></span> |<span data-ttu-id="88026-168">Identyfikator URI dla żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="88026-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="88026-169">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="88026-169">Headers</span></span> |<span data-ttu-id="88026-170">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="88026-170">headers</span></span> |<span data-ttu-id="88026-171">Obiekt JSON tooinclude nagłówków HTTP.</span><span class="sxs-lookup"><span data-stu-id="88026-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="88026-172">Treść</span><span class="sxs-lookup"><span data-stu-id="88026-172">Body</span></span> |<span data-ttu-id="88026-173">Treści</span><span class="sxs-lookup"><span data-stu-id="88026-173">body</span></span> |<span data-ttu-id="88026-174">Witaj treści żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="88026-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="88026-175">Authentication</span><span class="sxs-lookup"><span data-stu-id="88026-175">Authentication</span></span> |<span data-ttu-id="88026-176">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="88026-176">authentication</span></span> |<span data-ttu-id="88026-177">Toouse uwierzytelniania dla żądania.</span><span class="sxs-lookup"><span data-stu-id="88026-177">Authentication toouse for request.</span></span> <span data-ttu-id="88026-178">Aby uzyskać więcej informacji, zobacz hello [łącznika HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="88026-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="88026-179">**Szczegóły danych wyjściowych**</span><span class="sxs-lookup"><span data-stu-id="88026-179">**Output details**</span></span>

<span data-ttu-id="88026-180">Odpowiedź HTTP</span><span class="sxs-lookup"><span data-stu-id="88026-180">HTTP response</span></span>

| <span data-ttu-id="88026-181">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="88026-181">Property Name</span></span> | <span data-ttu-id="88026-182">Typ danych</span><span class="sxs-lookup"><span data-stu-id="88026-182">Data type</span></span> | <span data-ttu-id="88026-183">Opis</span><span class="sxs-lookup"><span data-stu-id="88026-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88026-184">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="88026-184">Headers</span></span> |<span data-ttu-id="88026-185">Obiekt</span><span class="sxs-lookup"><span data-stu-id="88026-185">object</span></span> |<span data-ttu-id="88026-186">Nagłówki odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88026-186">Response headers</span></span> |
| <span data-ttu-id="88026-187">Treść</span><span class="sxs-lookup"><span data-stu-id="88026-187">Body</span></span> |<span data-ttu-id="88026-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="88026-188">object</span></span> |<span data-ttu-id="88026-189">Obiekt odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88026-189">Response object</span></span> |
| <span data-ttu-id="88026-190">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="88026-190">Status Code</span></span> |<span data-ttu-id="88026-191">int</span><span class="sxs-lookup"><span data-stu-id="88026-191">int</span></span> |<span data-ttu-id="88026-192">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="88026-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="88026-193">Odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="88026-193">HTTP responses</span></span>
<span data-ttu-id="88026-194">Podczas wprowadzania wywołania toovarious akcje, może pobrać niektórych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="88026-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="88026-195">Poniżej znajduje się tabela przedstawiono odpowiedzi odpowiedniego wraz z opisami.</span><span class="sxs-lookup"><span data-stu-id="88026-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="88026-196">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88026-196">Name</span></span> | <span data-ttu-id="88026-197">Opis</span><span class="sxs-lookup"><span data-stu-id="88026-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88026-198">200</span><span class="sxs-lookup"><span data-stu-id="88026-198">200</span></span> |<span data-ttu-id="88026-199">OK</span><span class="sxs-lookup"><span data-stu-id="88026-199">OK</span></span> |
| <span data-ttu-id="88026-200">202</span><span class="sxs-lookup"><span data-stu-id="88026-200">202</span></span> |<span data-ttu-id="88026-201">Zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="88026-201">Accepted</span></span> |
| <span data-ttu-id="88026-202">400</span><span class="sxs-lookup"><span data-stu-id="88026-202">400</span></span> |<span data-ttu-id="88026-203">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="88026-203">Bad request</span></span> |
| <span data-ttu-id="88026-204">401</span><span class="sxs-lookup"><span data-stu-id="88026-204">401</span></span> |<span data-ttu-id="88026-205">Brak autoryzacji</span><span class="sxs-lookup"><span data-stu-id="88026-205">Unauthorized</span></span> |
| <span data-ttu-id="88026-206">403</span><span class="sxs-lookup"><span data-stu-id="88026-206">403</span></span> |<span data-ttu-id="88026-207">Dostęp zabroniony</span><span class="sxs-lookup"><span data-stu-id="88026-207">Forbidden</span></span> |
| <span data-ttu-id="88026-208">404</span><span class="sxs-lookup"><span data-stu-id="88026-208">404</span></span> |<span data-ttu-id="88026-209">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="88026-209">Not Found</span></span> |
| <span data-ttu-id="88026-210">500</span><span class="sxs-lookup"><span data-stu-id="88026-210">500</span></span> |<span data-ttu-id="88026-211">Wewnętrzny błąd serwera.</span><span class="sxs-lookup"><span data-stu-id="88026-211">Internal server error.</span></span> <span data-ttu-id="88026-212">Wystąpił nieznany błąd.</span><span class="sxs-lookup"><span data-stu-id="88026-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="88026-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88026-213">Next steps</span></span>

* [<span data-ttu-id="88026-214">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="88026-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="88026-215">Znajdź inne łączniki</span><span class="sxs-lookup"><span data-stu-id="88026-215">Find other connectors</span></span>](apis-list.md)