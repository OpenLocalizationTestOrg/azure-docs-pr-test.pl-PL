---
title: "Obsługa wyjątków i błędów rejestrowania scenariusz — aplikacje logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje przypadek użycia rzeczywistych o zaawansowanych wyjątków i rejestrowania błędów dla usługi Azure Logic Apps"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="ec23d-103">Scenariusz: Obsługa wyjątków i rejestrowania błędów dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="ec23d-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="ec23d-104">W tym scenariuszu opisano, jak można rozszerzyć aplikację logiki, aby lepiej obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="ec23d-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="ec23d-105">Odpowiedzi na pytanie użyliśmy przypadek użycia rzeczywistych: "Aplikacje logiki platformy Azure obsługuje wyjątek i obsługa błędów?"</span><span class="sxs-lookup"><span data-stu-id="ec23d-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="ec23d-106">Bieżący schemat Azure Logic Apps udostępnia standardowy szablon dla akcji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ec23d-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="ec23d-107">Ten szablon zawiera wewnętrznego sprawdzania poprawności i odpowiedzi na błędy zwrócone przez aplikację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ec23d-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="ec23d-108">Omówienie scenariusza i użyj case</span><span class="sxs-lookup"><span data-stu-id="ec23d-108">Scenario and use case overview</span></span>

<span data-ttu-id="ec23d-109">Oto wątku jako przypadek użycia dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="ec23d-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="ec23d-110">Dobrze znane organizacji opieki zdrowotnej zaangażowane w tworzenie Azure rozwiązania, które mogą utworzyć pacjenta portalu przy użyciu programu Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="ec23d-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="ec23d-111">One potrzebne do wysyłania rekordów termin Dynamics CRM Online pacjenta portalu i usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ec23d-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="ec23d-112">Firma Microsoft zostały poproszony [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standardowe dla wszystkich pacjenta rekordów.</span><span class="sxs-lookup"><span data-stu-id="ec23d-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="ec23d-113">Projekt ma dwa główne wymagania:</span><span class="sxs-lookup"><span data-stu-id="ec23d-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="ec23d-114">Metoda pod kątem rejestrowania rekordów wysyłane z portalu usługi Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="ec23d-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="ec23d-115">Można wyświetlić wszelkie błędy, które wystąpiły w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="ec23d-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="ec23d-116">Film wysokiego poziomu dotyczących tego projektu, zobacz [grupy użytkowników integracji](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="ec23d-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="ec23d-117">Jak możemy rozwiązuje problem</span><span class="sxs-lookup"><span data-stu-id="ec23d-117">How we solved the problem</span></span>

<span data-ttu-id="ec23d-118">Wybraliśmy [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/ "bazy danych Azure rozwiązania Cosmos") jako repozytorium dla rekordów dziennika i błąd (DB rozwiązania Cosmos odwołuje się do rekordów jako dokumentów).</span><span class="sxs-lookup"><span data-stu-id="ec23d-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="ec23d-119">Ponieważ aplikacje logiki platformy Azure ma standardowy szablon wszystkie odpowiedzi, nie mamy utworzyć schematu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ec23d-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="ec23d-120">Można utworzyć aplikację interfejsu API do **Wstaw** i **zapytania** rekordów zarówno błędu, jak i dziennika.</span><span class="sxs-lookup"><span data-stu-id="ec23d-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="ec23d-121">Również definiowania schematu dla każdego z nich w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ec23d-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="ec23d-122">Innym wymogiem było przeczyścić rekordów po określonej dacie.</span><span class="sxs-lookup"><span data-stu-id="ec23d-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="ec23d-123">Rozwiązania cosmos bazy danych ma właściwość o nazwie [czas wygaśnięcia](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "czas wygaśnięcia") (TTL), które mogą nam można ustawić **czas wygaśnięcia** wartość dla każdego rekordu lub kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ec23d-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="ec23d-124">Ta funkcja została wyeliminowana trzeba ręcznie usunąć rekordy w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ec23d-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec23d-125">Do ukończenia tego samouczka, należy utworzyć bazę danych DB rozwiązania Cosmos i dwie kolekcje (rejestrowania i błędów).</span><span class="sxs-lookup"><span data-stu-id="ec23d-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="ec23d-126">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ec23d-126">Create the logic app</span></span>

<span data-ttu-id="ec23d-127">Pierwszym krokiem jest utworzenie aplikacji logiki i Otwórz w Projektancie aplikacji logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec23d-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="ec23d-128">W tym przykładzie użyto aplikacje logiki nadrzędny podrzędny.</span><span class="sxs-lookup"><span data-stu-id="ec23d-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="ec23d-129">Załóżmy, że firma Microsoft utworzono już element nadrzędny, a aby utworzyć jedną aplikację logiki podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="ec23d-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="ec23d-130">Ponieważ zamierzamy rekord wystawała Dynamics CRM Online dziennika, Zacznijmy u góry.</span><span class="sxs-lookup"><span data-stu-id="ec23d-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="ec23d-131">Możemy użyć **żądania** wyzwolenia ponieważ aplikacji logiki nadrzędnego wyzwala tego dziecka.</span><span class="sxs-lookup"><span data-stu-id="ec23d-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="ec23d-132">Wyzwalaczem aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ec23d-132">Logic app trigger</span></span>

<span data-ttu-id="ec23d-133">Używamy **żądania** wyzwalania, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ec23d-133">We are using a **Request** trigger as shown in the following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="ec23d-134">Kroki</span><span class="sxs-lookup"><span data-stu-id="ec23d-134">Steps</span></span>

<span data-ttu-id="ec23d-135">Firma Microsoft muszą się logować źródła (żądanie) pacjenta rekordu z portalu usługi Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="ec23d-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="ec23d-136">Firma Microsoft musi uzyskać nowy rekord terminu z programu Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="ec23d-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="ec23d-137">Wyzwalacz pochodzące z CRM zapewnia nam z **CRM PatentId**, **typu rekordu**, **nowe lub zaktualizowane rekordu** (nowej lub zaktualizuj wartość logiczna), i **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="ec23d-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="ec23d-138">**SalesforceId** może mieć wartości null, ponieważ jest ona używana tylko dla aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ec23d-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="ec23d-139">Uzyskujemy rekordu CRM przy użyciu programu CRM **PatientID** i **typu rekordu**.</span><span class="sxs-lookup"><span data-stu-id="ec23d-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="ec23d-140">Następnie należy dodać naszej aplikacji interfejsu API usługi DocumentDB **InsertLogEntry** operacji, jak pokazano w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ec23d-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="ec23d-141">**Wstaw wpis dziennika**</span><span class="sxs-lookup"><span data-stu-id="ec23d-141">**Insert log entry**</span></span>

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="ec23d-143">**Wstaw wpis błędu**</span><span class="sxs-lookup"><span data-stu-id="ec23d-143">**Insert error entry**</span></span>

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="ec23d-145">**Sprawdź, czy utworzyć rekord błędu**</span><span class="sxs-lookup"><span data-stu-id="ec23d-145">**Check for create record failure**</span></span>

   ![Warunek](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="ec23d-147">Kod źródłowy aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ec23d-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="ec23d-148">Poniższe przykłady są tylko próbek.</span><span class="sxs-lookup"><span data-stu-id="ec23d-148">The following examples are samples only.</span></span> <span data-ttu-id="ec23d-149">Ponieważ w tym samouczku jest oparty na implementacji w środowisku produkcyjnym, wartość **węzeł źródłowy** może nie wyświetlać właściwości, które są związane z planowaniem terminu. ></span><span class="sxs-lookup"><span data-stu-id="ec23d-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="ec23d-150">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="ec23d-150">Logging</span></span>

<span data-ttu-id="ec23d-151">Poniższy przykład kodu aplikacji logiki pokazuje, jak do obsługi rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="ec23d-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="ec23d-152">Wpis dziennika</span><span class="sxs-lookup"><span data-stu-id="ec23d-152">Log entry</span></span>

<span data-ttu-id="ec23d-153">Oto kod źródłowy aplikacji logiki Wstawianie wpis dziennika.</span><span class="sxs-lookup"><span data-stu-id="ec23d-153">Here is the logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="ec23d-154">Żądanie dziennika</span><span class="sxs-lookup"><span data-stu-id="ec23d-154">Log request</span></span>

<span data-ttu-id="ec23d-155">Oto komunikat żądania dziennika opublikowane w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ec23d-155">Here is the log request message posted to the API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="ec23d-156">Odpowiedź dziennika</span><span class="sxs-lookup"><span data-stu-id="ec23d-156">Log response</span></span>

<span data-ttu-id="ec23d-157">Oto dziennika komunikat odpowiedzi z aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ec23d-157">Here is the log response message from the API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="ec23d-158">Teraz Przyjrzyjmy się kroków obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="ec23d-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="ec23d-159">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="ec23d-159">Error handling</span></span>

<span data-ttu-id="ec23d-160">Poniższy przykład kodu aplikacji logiki pokazuje, jak można zaimplementować obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="ec23d-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="ec23d-161">Utwórz rekord błędu</span><span class="sxs-lookup"><span data-stu-id="ec23d-161">Create error record</span></span>

<span data-ttu-id="ec23d-162">Oto kod źródłowy aplikacji logiki do tworzenia rekord błędu.</span><span class="sxs-lookup"><span data-stu-id="ec23d-162">Here is the logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="ec23d-163">Wstaw błędu w bazie danych rozwiązania Cosmos--żądania</span><span class="sxs-lookup"><span data-stu-id="ec23d-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="ec23d-164">Wstaw błędu w bazie danych rozwiązania Cosmos--odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ec23d-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="ec23d-165">Odpowiedzi na błąd SalesForce</span><span class="sxs-lookup"><span data-stu-id="ec23d-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="ec23d-166">Zwraca odpowiedź z powrotem do aplikacji logiki nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="ec23d-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="ec23d-167">Po uzyskaniu odpowiedzi, należy przekazać odpowiedź z powrotem do aplikacji logiki nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="ec23d-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="ec23d-168">Powodzenie odpowiedź zwrócona do aplikacji logiki nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="ec23d-168">Return success response to parent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="ec23d-169">Błąd odpowiedź zwrócona do aplikacji logiki nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="ec23d-169">Return error response to parent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="ec23d-170">Repozytorium rozwiązania cosmos bazy danych i portal</span><span class="sxs-lookup"><span data-stu-id="ec23d-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="ec23d-171">Nasze rozwiązanie dodane możliwości za pomocą [DB rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="ec23d-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="ec23d-172">Błąd portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="ec23d-172">Error management portal</span></span>

<span data-ttu-id="ec23d-173">Aby wyświetlić błędy, można utworzyć aplikacji sieci web MVC, aby wyświetlić błąd rekordy z bazy danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ec23d-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="ec23d-174">**Listy**, **szczegóły**, **Edytuj**, i **usunąć** operacji znajdują się w bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="ec23d-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="ec23d-175">Operacji edycji: rozwiązania Cosmos DB zamienia cały dokument.</span><span class="sxs-lookup"><span data-stu-id="ec23d-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="ec23d-176">Rejestruje pokazano **listy** i **szczegółów** widoki są tylko próbek.</span><span class="sxs-lookup"><span data-stu-id="ec23d-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="ec23d-177">Nie są one rzeczywiste termin pacjenta rekordów.</span><span class="sxs-lookup"><span data-stu-id="ec23d-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="ec23d-178">Poniżej przedstawiono przykłady naszych szczegóły aplikacji MVC utworzone za pomocą metody opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ec23d-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="ec23d-179">Błąd listy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="ec23d-179">Error management list</span></span>
![Lista błędów](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="ec23d-181">Błąd: widok szczegółów zarządzania</span><span class="sxs-lookup"><span data-stu-id="ec23d-181">Error management detail view</span></span>
![Szczegóły błędu](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="ec23d-183">Portal zarządzania dziennika</span><span class="sxs-lookup"><span data-stu-id="ec23d-183">Log management portal</span></span>

<span data-ttu-id="ec23d-184">Aby wyświetlić dzienniki, również utworzono aplikację sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="ec23d-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="ec23d-185">Poniżej przedstawiono przykłady naszych szczegóły aplikacji MVC utworzone za pomocą metody opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ec23d-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="ec23d-186">Przykładowy widok szczegółów dziennika</span><span class="sxs-lookup"><span data-stu-id="ec23d-186">Sample log detail view</span></span>
![Dziennik: widok szczegółów](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="ec23d-188">Szczegóły aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ec23d-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="ec23d-189">Zarządzanie wyjątkami logiki aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ec23d-189">Logic Apps exception management API</span></span>

<span data-ttu-id="ec23d-190">Open source aplikacji interfejsu API zarządzania wyjątek usługi Azure Logic Apps udostępnia funkcje, zgodnie z opisem w tym miejscu — istnieją dwa kontrolery:</span><span class="sxs-lookup"><span data-stu-id="ec23d-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="ec23d-191">**ErrorController** wstawia rekord błędu (dokument) w kolekcji usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ec23d-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="ec23d-192">**LogController** wstawia rekordu dziennika (dokument) w kolekcji usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ec23d-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="ec23d-193">Zarówno kontrolery `async Task<dynamic>` czynności operacji rozwiązywać w czasie wykonywania, dlatego utworzymy schematu usługi DocumentDB w treści operacji.</span><span class="sxs-lookup"><span data-stu-id="ec23d-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="ec23d-194">Każdy dokument w usłudze DocumentDB musi mieć unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ec23d-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="ec23d-195">Używamy `PatientId` i Dodawanie znaczników czasu, który jest konwertowany na wartość sygnatury czasowej systemu Unix (o podwójnej precyzji).</span><span class="sxs-lookup"><span data-stu-id="ec23d-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="ec23d-196">Firma Microsoft obciąć wartość na usuwanie ułamkowa wartość.</span><span class="sxs-lookup"><span data-stu-id="ec23d-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="ec23d-197">Można wyświetlić kodu źródłowego kontrolera błąd interfejsu API [z usługi GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="ec23d-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="ec23d-198">Nazywamy interfejsu API z aplikacji logiki przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="ec23d-198">We call the API from a logic app by using the following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="ec23d-199">Sprawdza, czy wyrażenie w poprzednim przykładzie kodu *Create_NewPatientRecord* stan ****.</span><span class="sxs-lookup"><span data-stu-id="ec23d-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="ec23d-200">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ec23d-200">Summary</span></span>

* <span data-ttu-id="ec23d-201">Można łatwo zaimplementować rejestrowania i obsługi błędów w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ec23d-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="ec23d-202">Usługi DocumentDB można użyć jako repozytorium rekordów dziennika i błąd (dokumentów).</span><span class="sxs-lookup"><span data-stu-id="ec23d-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="ec23d-203">MVC umożliwia tworzenie portalu do wyświetlania rekordów dziennika i błędów.</span><span class="sxs-lookup"><span data-stu-id="ec23d-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="ec23d-204">Kod źródłowy</span><span class="sxs-lookup"><span data-stu-id="ec23d-204">Source code</span></span>

<span data-ttu-id="ec23d-205">Kod źródłowy Zarządzanie wyjątkami aplikacje logiki aplikacji interfejsu API jest dostępna w tym [repozytorium GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API zarządzania wyjątków aplikacji logiki").</span><span class="sxs-lookup"><span data-stu-id="ec23d-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec23d-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec23d-206">Next steps</span></span>

* [<span data-ttu-id="ec23d-207">Wyświetl więcej logiki aplikacji przykłady i scenariusze</span><span class="sxs-lookup"><span data-stu-id="ec23d-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="ec23d-208">Więcej informacji na temat monitorowania aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ec23d-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="ec23d-209">Tworzenie szablonów automatycznego wdrażania dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="ec23d-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
