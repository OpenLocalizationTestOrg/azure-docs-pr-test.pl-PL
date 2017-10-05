---
title: "Wywołaj punkty końcowe REST z HTTP + Swagger connector dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia z aplikacji logiki za pośrednictwem programu Swagger z HTTP + programu Swagger do punkty końcowe REST łącznika"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="a69a8-103">Wprowadzenie do protokołu HTTP + Swagger akcji</span><span class="sxs-lookup"><span data-stu-id="a69a8-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="a69a8-104">Można utworzyć biletu łącznika do dowolnego punktu końcowego REST za pośrednictwem [dokumentu Swagger](https://swagger.io) korzystając HTTP + Swagger działań w przepływie pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a69a8-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="a69a8-105">Można również rozszerzyć zasięg aplikacji logiki, aby wywołać dowolnego punktu końcowego REST o najwyższej jakości środowisko projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a69a8-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="a69a8-106">Aby dowiedzieć się, jak tworzyć aplikacje logiki z łączników, zobacz [Utwórz nową aplikację logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a69a8-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="a69a8-107">Użyj protokołu HTTP + Swagger jako wyzwalacz lub akcji</span><span class="sxs-lookup"><span data-stu-id="a69a8-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="a69a8-108">HTTP + Swagger wyzwolenia i akcji w taki sam, jak działają [akcji HTTP](connectors-native-http.md) choć zapewnia lepsze środowisko pracy w Projektancie aplikacji logiki w przypadku wystawianego interfejsu API struktury i dane wyjściowe z [Swagger metadanych](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="a69a8-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="a69a8-109">Można również użyć HTTP + łącznika programu Swagger jako wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="a69a8-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="a69a8-110">Do zaimplementowania wyzwalacz sondowania, należy wykonać wzorzec sondowania, który jest opisany w [Tworzenie niestandardowych interfejsów API do wywoływania z aplikacji logiki innych interfejsów API, usług i systemy](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="a69a8-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="a69a8-111">Dowiedz się więcej o [logiki aplikacji wyzwalacze i akcje](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a69a8-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="a69a8-112">Oto przykład tego, jak to użycie HTTP + operacji programu Swagger jako akcja w przepływie pracy w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a69a8-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="a69a8-113">Wybierz **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a69a8-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="a69a8-114">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="a69a8-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="a69a8-115">W polu wyszukiwania akcji wpisz **swagger** do listy HTTP + akcji struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="a69a8-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Wybierz opcję HTTP + Swagger akcji](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="a69a8-117">Wpisz adres URL dokumentu Swagger:</span><span class="sxs-lookup"><span data-stu-id="a69a8-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="a69a8-118">Aby pracować przy użyciu projektanta aplikacji logiki, adres URL musi być punkt końcowy HTTPS i włączono CORS.</span><span class="sxs-lookup"><span data-stu-id="a69a8-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="a69a8-119">Jeśli dokumentu Swagger nie spełnia tego wymagania, możesz użyć [magazynu Azure z włączonym mechanizmem CORS](#hosting-swagger-from-storage) do przechowywania dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a69a8-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="a69a8-120">Kliknij przycisk **dalej** do odczytu i renderowania z dokumentu programu Swagger.</span><span class="sxs-lookup"><span data-stu-id="a69a8-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="a69a8-121">Dodaj w żadnych parametrów, które są wymagane dla połączenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="a69a8-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Zakończenie akcji HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="a69a8-123">Kliknij, aby zapisać i publikowanie aplikacji logiki **zapisać** na pasku narzędzi projektanta.</span><span class="sxs-lookup"><span data-stu-id="a69a8-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="a69a8-124">Swagger hosta z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a69a8-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="a69a8-125">Możesz chcieć odwołuje się do dokumentu Swagger, który nie jest obsługiwany lub który nie spełnia wymagań dotyczących cross-origin projektanta zabezpieczeń i.</span><span class="sxs-lookup"><span data-stu-id="a69a8-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="a69a8-126">Aby rozwiązać ten problem, można przechowywać dokumentu Swagger w usłudze Azure Storage i włączyć mechanizm CORS do odwołania dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a69a8-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="a69a8-127">Poniżej przedstawiono procedurę tworzenia, konfigurowania i przechowywanie dokumentów struktury Swagger w usłudze Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="a69a8-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="a69a8-128">[Utwórz konto magazynu platformy Azure z magazynu obiektów Blob Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a69a8-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a69a8-129">Aby wykonać ten krok, ustaw uprawnienia **dostępu publicznego**.</span><span class="sxs-lookup"><span data-stu-id="a69a8-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="a69a8-130">Włączanie mechanizmu CORS w obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="a69a8-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="a69a8-131">Aby automatycznie skonfigurować to ustawienie, można użyć [ten skrypt programu PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="a69a8-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="a69a8-132">Przekaż plik struktury Swagger do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="a69a8-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="a69a8-133">Można wykonać ten krok z [portalu Azure](https://portal.azure.com) lub z narzędzia, takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="a69a8-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="a69a8-134">Odwołanie łącza HTTPS do dokumentu w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a69a8-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="a69a8-135">Łącze używany format to:</span><span class="sxs-lookup"><span data-stu-id="a69a8-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="a69a8-136">Szczegóły techniczne</span><span class="sxs-lookup"><span data-stu-id="a69a8-136">Technical details</span></span>
<span data-ttu-id="a69a8-137">Poniżej przedstawiono szczegóły wyzwalacze i akcje który to HTTP + Swagger łącznik obsługuje.</span><span class="sxs-lookup"><span data-stu-id="a69a8-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="a69a8-138">HTTP + wyzwalaczy programu Swagger</span><span class="sxs-lookup"><span data-stu-id="a69a8-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="a69a8-139">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a69a8-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="a69a8-140">Dowiedz się więcej na temat wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="a69a8-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="a69a8-141">HTTP + Swagger łącznik ma jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="a69a8-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="a69a8-142">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="a69a8-142">Trigger</span></span> | <span data-ttu-id="a69a8-143">Opis</span><span class="sxs-lookup"><span data-stu-id="a69a8-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a69a8-144">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="a69a8-144">HTTP + Swagger</span></span> |<span data-ttu-id="a69a8-145">Wywoływania HTTP i zwrócić zawartość zgodnie z odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a69a8-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="a69a8-146">HTTP + akcje programu Swagger</span><span class="sxs-lookup"><span data-stu-id="a69a8-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="a69a8-147">Akcja jest operacja odbywa się przez przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a69a8-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="a69a8-148">Dowiedz się więcej na temat akcji.</span><span class="sxs-lookup"><span data-stu-id="a69a8-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="a69a8-149">HTTP + Swagger łącznik ma jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="a69a8-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="a69a8-150">Akcja</span><span class="sxs-lookup"><span data-stu-id="a69a8-150">Action</span></span> | <span data-ttu-id="a69a8-151">Opis</span><span class="sxs-lookup"><span data-stu-id="a69a8-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a69a8-152">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="a69a8-152">HTTP + Swagger</span></span> |<span data-ttu-id="a69a8-153">Wywoływania HTTP i zwrócić zawartość zgodnie z odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a69a8-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="a69a8-154">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="a69a8-154">Action details</span></span>
<span data-ttu-id="a69a8-155">HTTP + Swagger łącznika jest dostarczany z jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="a69a8-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="a69a8-156">Poniżej znajdują się informacje o poszczególnych działań, ich wymaganych i opcjonalnych pól wejściowych i odpowiednie szczegóły danych wyjściowych skojarzonych z ich użycia.</span><span class="sxs-lookup"><span data-stu-id="a69a8-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="a69a8-157">HTTP + struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="a69a8-157">HTTP + Swagger</span></span>
<span data-ttu-id="a69a8-158">Przesyłania żądania wychodzącego HTTP pomocy metadanych struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="a69a8-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="a69a8-159">Znak gwiazdki (*) oznacza wymaganego pola.</span><span class="sxs-lookup"><span data-stu-id="a69a8-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="a69a8-160">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="a69a8-160">Display name</span></span> | <span data-ttu-id="a69a8-161">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="a69a8-161">Property name</span></span> | <span data-ttu-id="a69a8-162">Opis</span><span class="sxs-lookup"><span data-stu-id="a69a8-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a69a8-163">Metoda *</span><span class="sxs-lookup"><span data-stu-id="a69a8-163">Method*</span></span> |<span data-ttu-id="a69a8-164">— Metoda</span><span class="sxs-lookup"><span data-stu-id="a69a8-164">method</span></span> |<span data-ttu-id="a69a8-165">Zlecenie HTTP do użycia.</span><span class="sxs-lookup"><span data-stu-id="a69a8-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="a69a8-166">IDENTYFIKATOR URI *</span><span class="sxs-lookup"><span data-stu-id="a69a8-166">URI*</span></span> |<span data-ttu-id="a69a8-167">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="a69a8-167">uri</span></span> |<span data-ttu-id="a69a8-168">Identyfikator URI dla żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a69a8-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="a69a8-169">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="a69a8-169">Headers</span></span> |<span data-ttu-id="a69a8-170">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="a69a8-170">headers</span></span> |<span data-ttu-id="a69a8-171">Obiekt JSON nagłówków HTTP w celu uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="a69a8-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="a69a8-172">Treść</span><span class="sxs-lookup"><span data-stu-id="a69a8-172">Body</span></span> |<span data-ttu-id="a69a8-173">Treści</span><span class="sxs-lookup"><span data-stu-id="a69a8-173">body</span></span> |<span data-ttu-id="a69a8-174">Treść żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a69a8-174">The HTTP request body.</span></span> |
| <span data-ttu-id="a69a8-175">Authentication</span><span class="sxs-lookup"><span data-stu-id="a69a8-175">Authentication</span></span> |<span data-ttu-id="a69a8-176">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="a69a8-176">authentication</span></span> |<span data-ttu-id="a69a8-177">Uwierzytelniania dla żądania.</span><span class="sxs-lookup"><span data-stu-id="a69a8-177">Authentication to use for request.</span></span> <span data-ttu-id="a69a8-178">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="a69a8-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="a69a8-179">**Szczegóły danych wyjściowych**</span><span class="sxs-lookup"><span data-stu-id="a69a8-179">**Output details**</span></span>

<span data-ttu-id="a69a8-180">Odpowiedź HTTP</span><span class="sxs-lookup"><span data-stu-id="a69a8-180">HTTP response</span></span>

| <span data-ttu-id="a69a8-181">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="a69a8-181">Property Name</span></span> | <span data-ttu-id="a69a8-182">Typ danych</span><span class="sxs-lookup"><span data-stu-id="a69a8-182">Data type</span></span> | <span data-ttu-id="a69a8-183">Opis</span><span class="sxs-lookup"><span data-stu-id="a69a8-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a69a8-184">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="a69a8-184">Headers</span></span> |<span data-ttu-id="a69a8-185">Obiekt</span><span class="sxs-lookup"><span data-stu-id="a69a8-185">object</span></span> |<span data-ttu-id="a69a8-186">Nagłówki odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a69a8-186">Response headers</span></span> |
| <span data-ttu-id="a69a8-187">Treść</span><span class="sxs-lookup"><span data-stu-id="a69a8-187">Body</span></span> |<span data-ttu-id="a69a8-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="a69a8-188">object</span></span> |<span data-ttu-id="a69a8-189">Obiekt odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a69a8-189">Response object</span></span> |
| <span data-ttu-id="a69a8-190">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="a69a8-190">Status Code</span></span> |<span data-ttu-id="a69a8-191">int</span><span class="sxs-lookup"><span data-stu-id="a69a8-191">int</span></span> |<span data-ttu-id="a69a8-192">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="a69a8-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="a69a8-193">Odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="a69a8-193">HTTP responses</span></span>
<span data-ttu-id="a69a8-194">Podczas wykonywania wywołań do różnych działań, może pobrać niektórych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a69a8-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="a69a8-195">Poniżej znajduje się tabela przedstawiono odpowiedzi odpowiedniego wraz z opisami.</span><span class="sxs-lookup"><span data-stu-id="a69a8-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="a69a8-196">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a69a8-196">Name</span></span> | <span data-ttu-id="a69a8-197">Opis</span><span class="sxs-lookup"><span data-stu-id="a69a8-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a69a8-198">200</span><span class="sxs-lookup"><span data-stu-id="a69a8-198">200</span></span> |<span data-ttu-id="a69a8-199">OK</span><span class="sxs-lookup"><span data-stu-id="a69a8-199">OK</span></span> |
| <span data-ttu-id="a69a8-200">202</span><span class="sxs-lookup"><span data-stu-id="a69a8-200">202</span></span> |<span data-ttu-id="a69a8-201">Zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="a69a8-201">Accepted</span></span> |
| <span data-ttu-id="a69a8-202">400</span><span class="sxs-lookup"><span data-stu-id="a69a8-202">400</span></span> |<span data-ttu-id="a69a8-203">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a69a8-203">Bad request</span></span> |
| <span data-ttu-id="a69a8-204">401</span><span class="sxs-lookup"><span data-stu-id="a69a8-204">401</span></span> |<span data-ttu-id="a69a8-205">Brak autoryzacji</span><span class="sxs-lookup"><span data-stu-id="a69a8-205">Unauthorized</span></span> |
| <span data-ttu-id="a69a8-206">403</span><span class="sxs-lookup"><span data-stu-id="a69a8-206">403</span></span> |<span data-ttu-id="a69a8-207">Dostęp zabroniony</span><span class="sxs-lookup"><span data-stu-id="a69a8-207">Forbidden</span></span> |
| <span data-ttu-id="a69a8-208">404</span><span class="sxs-lookup"><span data-stu-id="a69a8-208">404</span></span> |<span data-ttu-id="a69a8-209">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="a69a8-209">Not Found</span></span> |
| <span data-ttu-id="a69a8-210">500</span><span class="sxs-lookup"><span data-stu-id="a69a8-210">500</span></span> |<span data-ttu-id="a69a8-211">Wewnętrzny błąd serwera.</span><span class="sxs-lookup"><span data-stu-id="a69a8-211">Internal server error.</span></span> <span data-ttu-id="a69a8-212">Wystąpił nieznany błąd.</span><span class="sxs-lookup"><span data-stu-id="a69a8-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="a69a8-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a69a8-213">Next steps</span></span>

* [<span data-ttu-id="a69a8-214">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="a69a8-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="a69a8-215">Znajdź inne łączniki</span><span class="sxs-lookup"><span data-stu-id="a69a8-215">Find other connectors</span></span>](apis-list.md)