---
title: "Zmiana źródła danych dla zasobów HL7 FHIR - DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować powiadomienia o zmianie dla HL7 FHIR pacjenta rekordów opieki zdrowotnej przy użyciu usługi Azure Logic Apps, bazy danych rozwiązania Cosmos Azure i usługi Service Bus."
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="49a82-104">Powiadamianie pacjentów HL7 FHIR opieki zdrowotnej rekord zmian za pomocą aplikacji logiki i bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="49a82-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="49a82-105">Azure MVP Howard Edidin ostatnio skontaktowała opieki zdrowotnej organizacja, która chce Dodawanie nowych funkcji do ich pacjenta portalu.</span><span class="sxs-lookup"><span data-stu-id="49a82-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="49a82-106">One potrzebne do wysyłania powiadomień do pacjentów po ich kondycji rekordów została zaktualizowana i zachodzi potrzeba pacjentów, aby można było do subskrybowania tych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="49a82-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="49a82-107">W tym artykule przedstawiono zmiany źródła danych rozwiązania powiadomień utworzone dla tej organizacji opieki zdrowotnej, przy użyciu bazy danych rozwiązania Cosmos Azure Logic Apps i usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a82-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="49a82-108">Wymagania dotyczące projektu</span><span class="sxs-lookup"><span data-stu-id="49a82-108">Project requirements</span></span>
- <span data-ttu-id="49a82-109">Dostawców wysłanie HL7 klinicznych skonsolidowanych architektury dokument (dysk CD C) dokumenty w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="49a82-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="49a82-110">Dysk CD C dokumenty obejmują o niemal każdego typu klinicznych dokumencie, łącznie z klinicznych dokumentów, takie jak Historia rodziny i rejestruje uodparniania również jako administracyjne, przepływu pracy i dokumentów finansowych.</span><span class="sxs-lookup"><span data-stu-id="49a82-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="49a82-111">Dysk CD C dokumenty są konwertowane na [zasobów FHIR HL7](http://hl7.org/fhir/2017Jan/resourcelist.html) w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="49a82-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="49a82-112">Zmodyfikowane dokumenty zasobów FHIR są wysyłane za pośrednictwem poczty e-mail w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="49a82-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="49a82-113">Rozwiązania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="49a82-113">Solution workflow</span></span> 

<span data-ttu-id="49a82-114">Na wysokim poziomie projektu wymagane czynności przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="49a82-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="49a82-115">Konwertuj dysk CD C dokumentów na FHIR zasobów.</span><span class="sxs-lookup"><span data-stu-id="49a82-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="49a82-116">Wykonaj cyklicznego wyzwalacza sondowanie zmodyfikowanych zasobów FHIR.</span><span class="sxs-lookup"><span data-stu-id="49a82-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="49a82-117">Wywołanie aplikacji niestandardowej FhirNotificationApi łączyć się z bazy danych Azure rozwiązania Cosmos i zapytanie o nowych lub zmodyfikowanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="49a82-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="49a82-118">Zapisz odpowiedzi do magistrali usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="49a82-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="49a82-119">Sondowania nowe wiadomości w kolejce usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a82-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="49a82-120">Pacjentów wysyłania powiadomień e-mail.</span><span class="sxs-lookup"><span data-stu-id="49a82-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="49a82-121">Architektura rozwiązania</span><span class="sxs-lookup"><span data-stu-id="49a82-121">Solution architecture</span></span>
<span data-ttu-id="49a82-122">To rozwiązanie wymaga trzech powyższych wymagań i ukończenia przepływu pracy rozwiązania do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="49a82-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="49a82-123">Trzy aplikacje logiki to:</span><span class="sxs-lookup"><span data-stu-id="49a82-123">The three logic apps are:</span></span>
1. <span data-ttu-id="49a82-124">**HL7 FHIR mapowania aplikacji**: dokumentu HL7 C-dysk CD, przekształca je do zasobu FHIR, a następnie zapisuje go do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="49a82-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="49a82-125">**Aplikacja EHR**: wysyła zapytanie do repozytorium FHIR DB rozwiązania Cosmos Azure i zapisuje odpowiedź do kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a82-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="49a82-126">Korzysta z tej aplikacji logiki [aplikacji interfejsu API](#api-app) do pobierania nowych i zmienionych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="49a82-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="49a82-127">**Proces powiadomienie aplikacji**: wysyła wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR w treści.</span><span class="sxs-lookup"><span data-stu-id="49a82-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Trzy Logic Apps używane w tym rozwiązaniu opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="49a82-129">Usługi platformy Azure, używane w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="49a82-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="49a82-130">Azure rozwiązania Cosmos bazy danych DocumentDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="49a82-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="49a82-131">Azure DB rozwiązania Cosmos jest repozytorium dla zasobów FHIR, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="49a82-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![Konto bazy danych Azure rozwiązania Cosmos używane w tym samouczku opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="49a82-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="49a82-133">Logic Apps</span></span>
<span data-ttu-id="49a82-134">Aplikacje logiki obsługi procesu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="49a82-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="49a82-135">Poniższe zrzuty ekranu pokazują Logic apps utworzone dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="49a82-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="49a82-136">**HL7 FHIR mapowania aplikacji**: odbierania dokumentu HL7 C-dysk CD i przetransformować je do zasobu FHIR, używając pakiet integracyjny dla przedsiębiorstw dla usługi Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="49a82-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="49a82-137">Pakiet integracyjny dla przedsiębiorstw obsługuje mapowanie dysk CD C FHIR zasobów.</span><span class="sxs-lookup"><span data-stu-id="49a82-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![Aplikację logiki, używany do odbierania HL7 FHIR opieki zdrowotnej rekordów](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="49a82-139">**Aplikacja EHR**: zapytanie w repozytorium Azure rozwiązania Cosmos DB FHIR i Zapisz odpowiedzi do kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a82-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="49a82-140">Kod aplikacji GetNewOrModifiedFHIRDocuments znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="49a82-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Aplikację logiki wykorzystywane do badania bazy danych Azure rozwiązania Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="49a82-142">**Proces powiadomienie aplikacji**: Wyślij wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR w treści.</span><span class="sxs-lookup"><span data-stu-id="49a82-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![Aplikację logiki, która wysyła pacjenta wiadomości e-mail z zasobem HL7 FHIR w treści](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="49a82-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="49a82-144">Service Bus</span></span>
<span data-ttu-id="49a82-145">Na poniższej ilustracji przedstawiono pacjentów kolejki.</span><span class="sxs-lookup"><span data-stu-id="49a82-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="49a82-146">Wartość właściwości tagu jest używany dla tematu wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="49a82-146">The Tag property value is used for the email subject.</span></span>

![Kolejki magistrali usług używanych w tym samouczku HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="49a82-148">Aplikacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="49a82-148">API app</span></span>
<span data-ttu-id="49a82-149">Aplikację interfejsu API nawiązanie połączenia bazy danych Azure rozwiązania Cosmos oraz zapytania dotyczące nowych lub zmodyfikowanych dokumentów FHIR według typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="49a82-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="49a82-150">Ta aplikacja ma jeden kontroler **FhirNotificationApi** z jednej operacji **GetNewOrModifiedFhirDocuments**, zobacz [źródła dla aplikacji interfejsu API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="49a82-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="49a82-151">Używamy [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasy z interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="49a82-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="49a82-152">Aby uzyskać więcej informacji, zobacz [zmiany źródła artykułu](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="49a82-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="49a82-153">Operacja GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="49a82-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="49a82-154">**Dane wejściowe**</span><span class="sxs-lookup"><span data-stu-id="49a82-154">**Inputs**</span></span>
- <span data-ttu-id="49a82-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="49a82-155">DatabaseId</span></span>
- <span data-ttu-id="49a82-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="49a82-156">CollectionId</span></span>
- <span data-ttu-id="49a82-157">Nazwa typu zasobu FHIR HL7</span><span class="sxs-lookup"><span data-stu-id="49a82-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="49a82-158">Wartość logiczna: Rozpocznij od początku</span><span class="sxs-lookup"><span data-stu-id="49a82-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="49a82-159">Int: Liczba zwracanych dokumentów</span><span class="sxs-lookup"><span data-stu-id="49a82-159">Int: Number of documents returned</span></span>

<span data-ttu-id="49a82-160">**Dane wyjściowe**</span><span class="sxs-lookup"><span data-stu-id="49a82-160">**Outputs**</span></span>
- <span data-ttu-id="49a82-161">Powodzenie: Kod stanu: odpowiedzi 200,: listy dokumentów (tablica JSON)</span><span class="sxs-lookup"><span data-stu-id="49a82-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="49a82-162">Błędu: Kod stanu: odpowiedzi 404,: "znaleziono żadnych dokumentów"*Nazwa zasobu "* typu zasobu"</span><span class="sxs-lookup"><span data-stu-id="49a82-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="49a82-163">**Źródła dla aplikacji interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="49a82-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="49a82-164">Testowanie FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="49a82-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="49a82-165">Poniższa ilustracja pokazuje, jak swagger użyto do do testowania [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="49a82-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![Plik struktury Swagger wykorzystywane do testowania aplikacji interfejsu API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="49a82-167">Pulpitu nawigacyjnego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="49a82-167">Azure portal dashboard</span></span>

<span data-ttu-id="49a82-168">Na poniższej ilustracji przedstawiono wszystkie usługi platformy Azure dla tego rozwiązania, w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="49a82-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![Wyświetlanie wszystkich usług, które są używane w tym samouczku HL7 FHIR portalu Azure](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="49a82-170">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="49a82-170">Summary</span></span>

- <span data-ttu-id="49a82-171">Wiesz już, że bazy danych Azure rozwiązania Cosmos ma obsługuje natywnych powiadomień o nowych lub zmodyfikowane dokumenty i jak łatwo jest użycie.</span><span class="sxs-lookup"><span data-stu-id="49a82-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="49a82-172">Dzięki wykorzystaniu Logic Apps, mogą tworzyć przepływy pracy bez pisania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="49a82-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="49a82-173">Do obsługi dystrybucji HL7 FHIR dokumentów za pomocą kolejek usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a82-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49a82-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49a82-174">Next steps</span></span>
<span data-ttu-id="49a82-175">Aby uzyskać więcej informacji na temat bazy danych Azure rozwiązania Cosmos, zobacz [strony głównej bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="49a82-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="49a82-176">Aby uzyskać więcej informaiton o Logic Apps, zobacz [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="49a82-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


