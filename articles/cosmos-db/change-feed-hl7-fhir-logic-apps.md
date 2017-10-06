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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Powiadamianie pacjentów HL7 FHIR opieki zdrowotnej rekord zmian za pomocą aplikacji logiki i bazy danych Azure rozwiązania Cosmos

Ostatnio Azure MVP Howard Edidin skontaktowała się organizacji opieki zdrowotnej, firmę tooadd nowe funkcje tootheir pacjenta portalu. Toopatients powiadomienia toosend one potrzebne podczas ich kondycji rekordów została zaktualizowana i zachodzi potrzeba pacjentów toobe stanie toosubscribe toothese aktualizacji. 

W tym artykule przedstawiono rozwiązanie kanału powiadomień zmiany hello utworzony dla tej organizacji opieki zdrowotnej, przy użyciu bazy danych rozwiązania Cosmos Azure Logic Apps i usługi Service Bus. 

## <a name="project-requirements"></a>Wymagania dotyczące projektu
- Dostawców wysłanie HL7 klinicznych skonsolidowanych architektury dokument (dysk CD C) dokumenty w formacie XML. Dysk CD C dokumenty obejmują o niemal każdego typu klinicznych dokumencie, łącznie z klinicznych dokumentów, takie jak Historia rodziny i rejestruje uodparniania również jako administracyjne, przepływu pracy i dokumentów finansowych. 
- Dysk CD C dokumenty są konwertowane za[zasobów FHIR HL7](http://hl7.org/fhir/2017Jan/resourcelist.html) w formacie JSON.
- Zmodyfikowane dokumenty zasobów FHIR są wysyłane za pośrednictwem poczty e-mail w formacie JSON.

## <a name="solution-workflow"></a>Rozwiązania przepływu pracy 

Na wysokim poziomie projektu hello wymagane hello następujące kroki przepływu pracy: 
1. Konwertuj dysk CD C dokumenty tooFHIR zasobów.
2. Wykonaj cyklicznego wyzwalacza sondowanie zmodyfikowanych zasobów FHIR. 
2. Wywołania niestandardowych aplikacji, FhirNotificationApi, tooAzure tooconnect rozwiązania Cosmos bazy danych i zapytania dla nowych lub zmodyfikowanych dokumentów.
3. Zapisz kolejki usługi Service Bus tootoohello hello w odpowiedzi.
4. Sondowania nowe wiadomości powitania kolejki usługi Service Bus.
5. Wyślij toopatients powiadomienia e-mail.

## <a name="solution-architecture"></a>Architektura rozwiązania
To rozwiązanie wymaga trzech hello toomeet Logic Apps powyżej wymagań i hello kompletne rozwiązania w przepływie pracy. są trzy aplikacje logiki Hello:
1. **HL7 FHIR mapowania aplikacji**: odbiera hello HL7 C-dysk CD dokumentu, przekształca je toohello FHIR zasobów, a następnie zapisuje on tooAzure DB rozwiązania Cosmos.
2. **Aplikacja EHR**: wysyła zapytanie do repozytorium Azure rozwiązania Cosmos DB FHIR hello i zapisuje kolejki usługi Service Bus tooa hello w odpowiedzi. Korzysta z tej aplikacji logiki [aplikacji interfejsu API](#api-app) tooretrieve nowych i zmienionych dokumentów.
3. **Proces powiadomienie aplikacji**: wysyła wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR hello w treści hello.

![Aplikacje logiki Hello trzech używane w tym rozwiązaniu opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Używany w rozwiązaniu hello usług platformy Azure

#### <a name="azure-cosmos-db-documentdb-api"></a>Azure rozwiązania Cosmos bazy danych DocumentDB interfejsu API
Azure DB rozwiązania Cosmos to repozytorium hello hello FHIR zasobów, jak pokazano w powitania po rysunku.

![konto bazy danych Azure rozwiązania Cosmos Hello używane w tym samouczku opieki zdrowotnej HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Aplikacje logiki obsługiwać hello procesu przepływu pracy. Witaj poniższe zrzuty ekranu pokazują hello Logic apps utworzone dla tego rozwiązania. 


1. **HL7 FHIR mapowania aplikacji**: odbieranie hello HL7 C-dysk CD dokumentu i przetransformować je tooan FHIR zasobów dla usługi Logic Apps za pomocą hello pakiet integracyjny dla przedsiębiorstw. Pakiet integracyjny dla przedsiębiorstw Hello obsługuje hello mapowanie z hello dysk CD C tooFHIR zasobów.

    ![Witaj aplikacji logiki używane tooreceive HL7 FHIR opieki zdrowotnej rekordów](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Aplikacja EHR**: zapytania hello Azure rozwiązania Cosmos DB FHIR repozytorium i Zapisz hello tooa odpowiedzi usługi Service Bus w kolejce. Witaj kodu dla aplikacji GetNewOrModifiedFHIRDocuments hello jest niższa.

    ![tooquery aplikacji logiki używane Hello Azure DB rozwiązania Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Proces powiadomienie aplikacji**: Wyślij wiadomość e-mail z powiadomieniem z dokumentami zasobów FHIR hello w treści hello.

    ![Witaj aplikację logiki, która wysyła pacjenta wiadomości e-mail z zasobem HL7 FHIR hello w treści hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Service Bus
Witaj następujący rysunek przedstawia hello pacjentów kolejki. wartość właściwości tagu Hello jest używany dla hello temat wiadomości e-mail.

![Witaj używane w tym samouczku HL7 FHIR kolejką usługi Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>Aplikacja interfejsu API
Aplikację interfejsu API łączy tooAzure rozwiązania Cosmos bazy danych i zapytania dotyczące nowych lub zmodyfikowanych dokumentów FHIR według typów zasobów. Ta aplikacja ma jeden kontroler **FhirNotificationApi** z jednej operacji **GetNewOrModifiedFhirDocuments**, zobacz [źródła dla aplikacji interfejsu API](#api-app-source).

Używamy hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasy z hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB platformy .NET. Aby uzyskać więcej informacji, zobacz hello [zmiany źródła artykułu](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Operacja GetNewOrModifiedFhirDocuments

**Dane wejściowe**
- DatabaseId
- CollectionId
- Nazwa typu zasobu FHIR HL7
- Wartość logiczna: Rozpocznij od początku
- Int: Liczba zwracanych dokumentów

**Dane wyjściowe**
- Powodzenie: Kod stanu: odpowiedzi 200,: listy dokumentów (tablica JSON)
- Błędu: Kod stanu: odpowiedzi 404,: "znaleziono żadnych dokumentów"*Nazwa zasobu "* typu zasobu"

<a id="api-app-source"></a>

**Źródła dla aplikacji hello interfejsu API**

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

### <a name="testing-hello-fhirnotificationapi"></a>Testowanie hello FhirNotificationApi 

Witaj Poniższa ilustracja pokazuje sposób swagger został hello tootootest używane [FhirNotificationApi](#api-app-source).

![Plik Swagger Hello używany aplikacji interfejsu API hello tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Pulpitu nawigacyjnego portalu Azure

powitania po obrazu są wyświetlane wszystkie hello usług platformy Azure dla tego rozwiązania w hello portalu Azure.

![Witaj portalu Azure pokazujący wszystkie usługi hello używane w tym samouczku HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Podsumowanie

- Wiesz już, że bazy danych Azure rozwiązania Cosmos ma obsługuje natywnych powiadomień o nowych lub zmodyfikowane dokumenty i jak łatwo jest toouse. 
- Dzięki wykorzystaniu Logic Apps, mogą tworzyć przepływy pracy bez pisania żadnego kodu.
- Za pomocą kolejek usługi Azure Service Bus toohandle hello dystrybucji hello HL7 FHIR dokumentów.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat bazy danych Azure rozwiązania Cosmos Zobacz hello [strony głównej bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/). Aby uzyskać więcej informaiton o Logic Apps, zobacz [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


