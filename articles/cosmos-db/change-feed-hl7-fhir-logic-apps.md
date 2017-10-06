---
title: "dla zasobów HL7 FHIR — bazy danych Azure rozwiązania Cosmos aaaChange | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się zmienić powiadomienia dla HL7 FHIR pacjenta rekordów opieki zdrowotnej przy użyciu usługi Azure Logic Apps, bazy danych rozwiązania Cosmos Azure i usługi Service Bus."
keywords: HL7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="94907-104">Powiadamianie pacjentów HL7 FHIR opieki zdrowotnej rekord zmian za pomocą aplikacji logiki i bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="94907-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="94907-105">Ostatnio Azure MVP Howard Edidin skontaktowała się organizacji opieki zdrowotnej, firmę tooadd nowe funkcje tootheir pacjenta portalu.</span><span class="sxs-lookup"><span data-stu-id="94907-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="94907-106">Toopatients powiadomienia toosend one potrzebne podczas ich kondycji rekordów została zaktualizowana i zachodzi potrzeba pacjentów toobe stanie toosubscribe toothese aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="94907-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="94907-107">W tym artykule przedstawiono rozwiązanie kanału powiadomień zmiany hello utworzony dla tej organizacji opieki zdrowotnej, przy użyciu bazy danych rozwiązania Cosmos Azure Logic Apps i usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="94907-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="94907-108">Wymagania dotyczące projektu</span><span class="sxs-lookup"><span data-stu-id="94907-108">Project requirements</span></span>
- <span data-ttu-id="94907-109">Dostawców wysłanie HL7 klinicznych skonsolidowanych architektury dokument (dysk CD C) dokumenty w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="94907-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="94907-110">Dysk CD C dokumenty obejmują o niemal każdego typu klinicznych dokumencie, łącznie z klinicznych dokumentów, takie jak Historia rodziny i rejestruje uodparniania również jako administracyjne, przepływu pracy i dokumentów finansowych.</span><span class="sxs-lookup"><span data-stu-id="94907-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="94907-111">Dysk CD C dokumenty są konwertowane za[zasobów FHIR HL7](http://hl7.org/fhir/2017Jan/resourcelist.html) w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="94907-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="94907-112">Zmodyfikowane dokumenty zasobów FHIR są wysyłane za pośrednictwem poczty e-mail w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="94907-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="94907-113">Rozwiązania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="94907-113">Solution workflow</span></span> 

<span data-ttu-id="94907-114">Na wysokim poziomie projektu hello wymagane hello następujące kroki przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="94907-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="94907-115">Konwertuj dysk CD C dokumenty tooFHIR zasobów.</span><span class="sxs-lookup"><span data-stu-id="94907-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="94907-116">Wykonaj cyklicznego wyzwalacza sondowanie zmodyfikowanych zasobów FHIR.</span><span class="sxs-lookup"><span data-stu-id="94907-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="94907-117">Wywołania niestandardowych aplikacji, FhirNotificationApi, tooAzure tooconnect rozwiązania Cosmos bazy danych i zapytania dla nowych lub zmodyfikowanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="94907-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="94907-118">Zapisz kolejki usługi Service Bus tootoohello hello w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="94907-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="94907-119">Sondowania nowe wiadomości powitania kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="94907-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="94907-120">Wyślij toopatients powiadomienia e-mail.</span><span class="sxs-lookup"><span data-stu-id="94907-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="94907-121">Architektura rozwiązania</span><span class="sxs-lookup"><span data-stu-id="94907-121">Solution architecture</span></span>
<span data-ttu-id="94907-122">To rozwiązanie wymaga trzech hello toomeet Logic Apps powyżej wymagań i hello kompletne rozwiązania w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="94907-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="94907-123">są trzy aplikacje logiki Hello:</span><span class="sxs-lookup"><span data-stu-id="94907-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="94907-124">**HL7 FHIR mapowania aplikacji**: odbiera hello HL7 C-dysk CD dokumentu, przekształca je toohello FHIR zasobów, a następnie zapisuje on tooAzure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="94907-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="94907-125">**Aplikacja EHR**: wysyła zapytanie do repozytorium Azure rozwiązania Cosmos DB FHIR hello i zapisuje kolejki usługi Service Bus tooa hello w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="94907-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="94907-126">Korzysta z tej aplikacji logiki [aplikacji interfejsu API](#api-app) tooretrieve nowych i zmienionych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="94907-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="94907-127">**Proces powiadomienie aplikacji**: wysyła wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR hello w treści hello.</span><span class="sxs-lookup"><span data-stu-id="94907-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Aplikacje logiki Hello trzech używane w tym rozwiązaniu opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="94907-129">Używany w rozwiązaniu hello usług platformy Azure</span><span class="sxs-lookup"><span data-stu-id="94907-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="94907-130">Azure rozwiązania Cosmos bazy danych DocumentDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="94907-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="94907-131">Azure DB rozwiązania Cosmos to repozytorium hello hello FHIR zasobów, jak pokazano w powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="94907-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![konto bazy danych Azure rozwiązania Cosmos Hello używane w tym samouczku opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="94907-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="94907-133">Logic Apps</span></span>
<span data-ttu-id="94907-134">Aplikacje logiki obsługiwać hello procesu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="94907-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="94907-135">Witaj poniższe zrzuty ekranu pokazują hello Logic apps utworzone dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="94907-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="94907-136">**HL7 FHIR mapowania aplikacji**: odbieranie hello HL7 C-dysk CD dokumentu i przetransformować je tooan FHIR zasobów dla usługi Logic Apps za pomocą hello pakiet integracyjny dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="94907-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="94907-137">Pakiet integracyjny dla przedsiębiorstw Hello obsługuje hello mapowanie z hello dysk CD C tooFHIR zasobów.</span><span class="sxs-lookup"><span data-stu-id="94907-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Witaj aplikacji logiki używane tooreceive HL7 FHIR opieki zdrowotnej rekordów](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="94907-139">**Aplikacja EHR**: zapytania hello Azure rozwiązania Cosmos DB FHIR repozytorium i Zapisz hello tooa odpowiedzi usługi Service Bus w kolejce.</span><span class="sxs-lookup"><span data-stu-id="94907-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="94907-140">Witaj kodu dla aplikacji GetNewOrModifiedFHIRDocuments hello jest niższa.</span><span class="sxs-lookup"><span data-stu-id="94907-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![tooquery aplikacji logiki używane Hello Azure DB rozwiązania Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="94907-142">**Proces powiadomienie aplikacji**: Wyślij wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR hello w treści hello.</span><span class="sxs-lookup"><span data-stu-id="94907-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Witaj aplikację logiki, która wysyła pacjenta wiadomości e-mail z zasobem HL7 FHIR hello w treści hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="94907-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="94907-144">Service Bus</span></span>
<span data-ttu-id="94907-145">Witaj następujący rysunek przedstawia hello pacjentów kolejki.</span><span class="sxs-lookup"><span data-stu-id="94907-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="94907-146">wartość właściwości tagu Hello jest używany dla hello temat wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="94907-146">hello Tag property value is used for hello email subject.</span></span>

![Witaj używane w tym samouczku HL7 FHIR kolejką usługi Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="94907-148">Aplikacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="94907-148">API app</span></span>
<span data-ttu-id="94907-149">Aplikację interfejsu API łączy tooAzure rozwiązania Cosmos bazy danych i zapytania dotyczące nowych lub zmodyfikowanych dokumentów FHIR według typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="94907-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="94907-150">Ta aplikacja ma jeden kontroler **FhirNotificationApi** z jednej operacji **GetNewOrModifiedFhirDocuments**, zobacz [źródła dla aplikacji interfejsu API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="94907-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="94907-151">Używamy hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasy z hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="94907-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="94907-152">Aby uzyskać więcej informacji, zobacz hello [zmiany źródła artykułu](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="94907-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="94907-153">Operacja GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="94907-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="94907-154">**Dane wejściowe**</span><span class="sxs-lookup"><span data-stu-id="94907-154">**Inputs**</span></span>
- <span data-ttu-id="94907-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="94907-155">DatabaseId</span></span>
- <span data-ttu-id="94907-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="94907-156">CollectionId</span></span>
- <span data-ttu-id="94907-157">Nazwa typu zasobu FHIR HL7</span><span class="sxs-lookup"><span data-stu-id="94907-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="94907-158">Wartość logiczna: Rozpocznij od początku</span><span class="sxs-lookup"><span data-stu-id="94907-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="94907-159">Int: Liczba zwracanych dokumentów</span><span class="sxs-lookup"><span data-stu-id="94907-159">Int: Number of documents returned</span></span>

<span data-ttu-id="94907-160">**Dane wyjściowe**</span><span class="sxs-lookup"><span data-stu-id="94907-160">**Outputs**</span></span>
- <span data-ttu-id="94907-161">Powodzenie: Kod stanu: odpowiedzi 200,: listy dokumentów (tablica JSON)</span><span class="sxs-lookup"><span data-stu-id="94907-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="94907-162">Błędu: Kod stanu: odpowiedzi 404,: "znaleziono żadnych dokumentów"*Nazwa zasobu "* typu zasobu"</span><span class="sxs-lookup"><span data-stu-id="94907-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="94907-163">**Źródła dla aplikacji hello interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="94907-163">**Source for hello API app**</span></span>

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="94907-164">Testowanie hello FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="94907-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="94907-165">Witaj Poniższa ilustracja pokazuje sposób swagger został hello tootootest używane [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="94907-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![Plik Swagger Hello używany aplikacji interfejsu API hello tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="94907-167">Pulpitu nawigacyjnego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="94907-167">Azure portal dashboard</span></span>

<span data-ttu-id="94907-168">powitania po obrazu są wyświetlane wszystkie hello usług platformy Azure dla tego rozwiązania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="94907-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Witaj portalu Azure pokazujący wszystkie usługi hello używane w tym samouczku HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="94907-170">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="94907-170">Summary</span></span>

- <span data-ttu-id="94907-171">Wiesz już, że bazy danych Azure rozwiązania Cosmos ma obsługuje natywnych powiadomień o nowych lub zmodyfikowane dokumenty i jak łatwo jest toouse.</span><span class="sxs-lookup"><span data-stu-id="94907-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="94907-172">Dzięki wykorzystaniu Logic Apps, mogą tworzyć przepływy pracy bez pisania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="94907-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="94907-173">Za pomocą kolejek usługi Azure Service Bus toohandle hello dystrybucji hello HL7 FHIR dokumentów.</span><span class="sxs-lookup"><span data-stu-id="94907-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94907-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94907-174">Next steps</span></span>
<span data-ttu-id="94907-175">Aby uzyskać więcej informacji na temat bazy danych Azure rozwiązania Cosmos Zobacz hello [strony głównej bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="94907-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="94907-176">Aby uzyskać więcej informaiton o Logic Apps, zobacz [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="94907-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


