---
title: "aaaException Obsługa & Błąd rejestrowania scenariusz — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="169c8-103">Scenariusz: Obsługa wyjątków i rejestrowania błędów dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="169c8-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="169c8-104">W tym scenariuszu opisano, jak można rozszerzyć obsługi logiki aplikacji toobetter obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="169c8-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="169c8-105">Firma Microsoft używano pytanie hello tooanswer przypadków użycia rzeczywistych: "Aplikacje logiki platformy Azure obsługuje wyjątek i obsługa błędów?"</span><span class="sxs-lookup"><span data-stu-id="169c8-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="169c8-106">bieżący schemat Azure Logic Apps Hello udostępnia standardowy szablon dla akcji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="169c8-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="169c8-107">Ten szablon zawiera wewnętrznego sprawdzania poprawności i odpowiedzi na błędy zwrócone przez aplikację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="169c8-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="169c8-108">Omówienie scenariusza i użyj case</span><span class="sxs-lookup"><span data-stu-id="169c8-108">Scenario and use case overview</span></span>

<span data-ttu-id="169c8-109">Oto wątku hello jako hello przypadek użycia dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="169c8-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="169c8-110">Dobrze znane organizacji opieki zdrowotnej zaangażowane nam toodevelop Azure rozwiązania, które spowoduje utworzenie pacjenta portalu przy użyciu programu Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="169c8-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="169c8-111">Zachodzi potrzeba toosend termin rekordów hello Dynamics CRM Online pacjenta portalu i Salesforce.</span><span class="sxs-lookup"><span data-stu-id="169c8-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="169c8-112">Firma Microsoft zostały zadawane toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standardowe dla wszystkich pacjenta rekordów.</span><span class="sxs-lookup"><span data-stu-id="169c8-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="169c8-113">Projekt Hello ma dwa główne wymagania:</span><span class="sxs-lookup"><span data-stu-id="169c8-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="169c8-114">Rekordy toolog metody wysyłane z hello portalu Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="169c8-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="169c8-115">Tooview sposób wszelkie błędy, które wystąpiły w przepływie pracy hello</span><span class="sxs-lookup"><span data-stu-id="169c8-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="169c8-116">Film wysokiego poziomu dotyczących tego projektu, zobacz [grupy użytkowników integracji](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupy użytkowników integracji").</span><span class="sxs-lookup"><span data-stu-id="169c8-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="169c8-117">Jak możemy rozwiązać hello problem</span><span class="sxs-lookup"><span data-stu-id="169c8-117">How we solved hello problem</span></span>

<span data-ttu-id="169c8-118">Wybraliśmy [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/ "bazy danych Azure rozwiązania Cosmos") jako repozytorium rekordów dziennika i błąd hello (DB rozwiązania Cosmos odwołuje się toorecords jako dokumentów).</span><span class="sxs-lookup"><span data-stu-id="169c8-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="169c8-119">Ponieważ aplikacje logiki platformy Azure ma standardowy szablon wszystkie odpowiedzi, firma Microsoft nie będzie zawierało toocreate schematu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="169c8-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="169c8-120">Można utworzyć aplikację interfejsu API za**Wstaw** i **zapytania** rekordów zarówno błędu, jak i dziennika.</span><span class="sxs-lookup"><span data-stu-id="169c8-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="169c8-121">Również definiowania schematu dla każdego poziomu hello aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="169c8-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="169c8-122">Innym wymogiem jest rekordów toopurge po określonej dacie.</span><span class="sxs-lookup"><span data-stu-id="169c8-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="169c8-123">Rozwiązania cosmos bazy danych ma właściwość o nazwie [czasu tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "czasu tooLive") (TTL), które mogą nam tooset **czasu tooLive** wartość dla każdego rekordu lub kolekcji.</span><span class="sxs-lookup"><span data-stu-id="169c8-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="169c8-124">Ta funkcja została wyeliminowana hello muszą toomanually usuwania rekordów w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="169c8-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="169c8-125">toocomplete tego samouczka potrzebne toocreate bazy danych DB rozwiązania Cosmos i dwie kolekcje (rejestrowania i błędów).</span><span class="sxs-lookup"><span data-stu-id="169c8-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="169c8-126">Tworzenie aplikacji logiki hello</span><span class="sxs-lookup"><span data-stu-id="169c8-126">Create hello logic app</span></span>

<span data-ttu-id="169c8-127">Witaj pierwszym krokiem jest aplikacji logiki hello toocreate i aplikacji hello Otwórz w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="169c8-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="169c8-128">W tym przykładzie użyto aplikacje logiki nadrzędny podrzędny.</span><span class="sxs-lookup"><span data-stu-id="169c8-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="169c8-129">Załóżmy, że firma Microsoft hello nadrzędnego jest już utworzony i będzie toocreate jeden podrzędny logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="169c8-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="169c8-130">Ponieważ zamierzamy rekordu hello toolog wystawała Dynamics CRM Online, Zacznijmy u góry hello.</span><span class="sxs-lookup"><span data-stu-id="169c8-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="169c8-131">Możemy użyć **żądania** wyzwolenia ponieważ aplikacji logiki nadrzędnego hello wyzwala tego dziecka.</span><span class="sxs-lookup"><span data-stu-id="169c8-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="169c8-132">Wyzwalaczem aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="169c8-132">Logic app trigger</span></span>

<span data-ttu-id="169c8-133">Używamy **żądania** wyzwalania, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="169c8-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="169c8-134">Kroki</span><span class="sxs-lookup"><span data-stu-id="169c8-134">Steps</span></span>

<span data-ttu-id="169c8-135">Firma Microsoft musi zarejestrować hello źródła (żądanie) rekordu pacjenta hello hello portalu Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="169c8-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="169c8-136">Firma Microsoft musi uzyskać nowy rekord terminu z programu Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="169c8-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="169c8-137">wyzwalacz Hello pochodzące z CRM zapewnia hello **CRM PatentId**, **typu rekordu**, **nowe lub zaktualizowane rekordu** (nowej lub zaktualizuj wartość logiczna), i ** SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="169c8-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="169c8-138">Witaj **SalesforceId** może mieć wartości null, ponieważ jest ona używana tylko dla aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="169c8-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="169c8-139">Uzyskujemy hello CRM rekordu przy użyciu hello CRM **PatientID** i hello **typu rekordu**.</span><span class="sxs-lookup"><span data-stu-id="169c8-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="169c8-140">Następnie należy tooadd aplikacji interfejsu API usługi DocumentDB **InsertLogEntry** operacji, jak pokazano w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="169c8-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="169c8-141">**Wstaw wpis dziennika**</span><span class="sxs-lookup"><span data-stu-id="169c8-141">**Insert log entry**</span></span>

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="169c8-143">**Wstaw wpis błędu**</span><span class="sxs-lookup"><span data-stu-id="169c8-143">**Insert error entry**</span></span>

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="169c8-145">**Sprawdź, czy utworzyć rekord błędu**</span><span class="sxs-lookup"><span data-stu-id="169c8-145">**Check for create record failure**</span></span>

   ![Warunek](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="169c8-147">Kod źródłowy aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="169c8-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="169c8-148">Następujące przykłady Hello są tylko próbek.</span><span class="sxs-lookup"><span data-stu-id="169c8-148">hello following examples are samples only.</span></span> <span data-ttu-id="169c8-149">Ponieważ w tym samouczku jest oparty na implementacji teraz w środowisku produkcyjnym, hello wartość **węzeł źródłowy** może nie wyświetlać właściwości, które są powiązane tooscheduling terminu. ></span><span class="sxs-lookup"><span data-stu-id="169c8-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="169c8-150">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="169c8-150">Logging</span></span>

<span data-ttu-id="169c8-151">jak przedstawiono przykładowe Hello następującego kodu aplikacji logiki toohandle rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="169c8-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="169c8-152">Wpis dziennika</span><span class="sxs-lookup"><span data-stu-id="169c8-152">Log entry</span></span>

<span data-ttu-id="169c8-153">Oto kod źródłowy aplikacji hello logikę wstawiania wpis dziennika.</span><span class="sxs-lookup"><span data-stu-id="169c8-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="169c8-154">Żądanie dziennika</span><span class="sxs-lookup"><span data-stu-id="169c8-154">Log request</span></span>

<span data-ttu-id="169c8-155">Oto komunikat żądania dziennika hello zaksięgowany toohello aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="169c8-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="169c8-156">Odpowiedź dziennika</span><span class="sxs-lookup"><span data-stu-id="169c8-156">Log response</span></span>

<span data-ttu-id="169c8-157">Oto komunikat odpowiedzi dziennika hello z hello aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="169c8-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="169c8-158">Teraz Przyjrzyjmy się obsługi kroki hello błędów.</span><span class="sxs-lookup"><span data-stu-id="169c8-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="169c8-159">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="169c8-159">Error handling</span></span>

<span data-ttu-id="169c8-160">Witaj Poniższy przykładowy kod aplikacji logiki pokazuje sposoby implementowania obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="169c8-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="169c8-161">Utwórz rekord błędu</span><span class="sxs-lookup"><span data-stu-id="169c8-161">Create error record</span></span>

<span data-ttu-id="169c8-162">Oto kod źródłowy aplikacji logiki hello tworzenia rekord błędu.</span><span class="sxs-lookup"><span data-stu-id="169c8-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="169c8-163">Wstaw błędu w bazie danych rozwiązania Cosmos--żądania</span><span class="sxs-lookup"><span data-stu-id="169c8-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="169c8-164">Wstaw błędu w bazie danych rozwiązania Cosmos--odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="169c8-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="169c8-165">Odpowiedzi na błąd SalesForce</span><span class="sxs-lookup"><span data-stu-id="169c8-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="169c8-166">Zwraca hello odpowiedzi wstecz tooparent logiki aplikacji</span><span class="sxs-lookup"><span data-stu-id="169c8-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="169c8-167">Po uzyskaniu odpowiedzi hello można przekazać odpowiedź hello aplikacji logiki nadrzędnej toohello Wstecz.</span><span class="sxs-lookup"><span data-stu-id="169c8-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="169c8-168">Zwraca sukces odpowiedzi tooparent logiki aplikacji</span><span class="sxs-lookup"><span data-stu-id="169c8-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="169c8-169">Aplikacja logiki tooparent odpowiedzi zwróciła błąd</span><span class="sxs-lookup"><span data-stu-id="169c8-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="169c8-170">Repozytorium rozwiązania cosmos bazy danych i portal</span><span class="sxs-lookup"><span data-stu-id="169c8-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="169c8-171">Nasze rozwiązanie dodane możliwości za pomocą [DB rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="169c8-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="169c8-172">Błąd portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="169c8-172">Error management portal</span></span>

<span data-ttu-id="169c8-173">tooview hello błędy, można tworzyć MVC sieci web aplikacji toodisplay hello błąd rekordy z bazy danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="169c8-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="169c8-174">Hello **listy**, **szczegóły**, **Edytuj**, i **usunąć** operacji znajdują się w bieżącej wersji powitania.</span><span class="sxs-lookup"><span data-stu-id="169c8-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="169c8-175">Operacji edycji: rozwiązania Cosmos DB zastępuje hello całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="169c8-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="169c8-176">Witaj rekordów wyświetlanych w hello **listy** i **szczegółów** widoki są tylko próbek.</span><span class="sxs-lookup"><span data-stu-id="169c8-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="169c8-177">Nie są one rzeczywiste termin pacjenta rekordów.</span><span class="sxs-lookup"><span data-stu-id="169c8-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="169c8-178">Poniżej przedstawiono przykłady naszej aplikacji MVC szczegóły wcześniej utworzony hello opisane podejście.</span><span class="sxs-lookup"><span data-stu-id="169c8-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="169c8-179">Błąd listy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="169c8-179">Error management list</span></span>
![Lista błędów](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="169c8-181">Błąd: widok szczegółów zarządzania</span><span class="sxs-lookup"><span data-stu-id="169c8-181">Error management detail view</span></span>
![Szczegóły błędu](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="169c8-183">Portal zarządzania dziennika</span><span class="sxs-lookup"><span data-stu-id="169c8-183">Log management portal</span></span>

<span data-ttu-id="169c8-184">Dzienniki hello tooview, również utworzono aplikację sieci web MVC.</span><span class="sxs-lookup"><span data-stu-id="169c8-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="169c8-185">Poniżej przedstawiono przykłady naszej aplikacji MVC szczegóły wcześniej utworzony hello opisane podejście.</span><span class="sxs-lookup"><span data-stu-id="169c8-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="169c8-186">Przykładowy widok szczegółów dziennika</span><span class="sxs-lookup"><span data-stu-id="169c8-186">Sample log detail view</span></span>
![Dziennik: widok szczegółów](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="169c8-188">Szczegóły aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="169c8-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="169c8-189">Zarządzanie wyjątkami logiki aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="169c8-189">Logic Apps exception management API</span></span>

<span data-ttu-id="169c8-190">Open source aplikacji interfejsu API zarządzania wyjątek usługi Azure Logic Apps udostępnia funkcje, zgodnie z opisem w tym miejscu — istnieją dwa kontrolery:</span><span class="sxs-lookup"><span data-stu-id="169c8-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="169c8-191">**ErrorController** wstawia rekord błędu (dokument) w kolekcji usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="169c8-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="169c8-192">**LogController** wstawia rekordu dziennika (dokument) w kolekcji usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="169c8-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="169c8-193">Zarówno kontrolery `async Task<dynamic>` czynności tooresolve operacji w czasie wykonywania, więc można utworzyć hello schematu usługi DocumentDB w treści hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="169c8-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="169c8-194">Każdy dokument w usłudze DocumentDB musi mieć unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="169c8-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="169c8-195">Używamy `PatientId` i Dodawanie znaczników czasu, który jest przekonwertować wartość sygnatury czasowej systemu Unix tooa (o podwójnej precyzji).</span><span class="sxs-lookup"><span data-stu-id="169c8-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="169c8-196">Firma Microsoft obciąć hello tooremove hello ułamkowych wartość.</span><span class="sxs-lookup"><span data-stu-id="169c8-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="169c8-197">Można wyświetlić kodu źródłowego hello błąd kontrolera interfejsu API [z usługi GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="169c8-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="169c8-198">Nazywamy hello interfejsu API z aplikacji logiki przy użyciu hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="169c8-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="169c8-199">Witaj wyrażenie w hello poprzedzających sprawdza przykładowy kod hello *Create_NewPatientRecord* stan ****.</span><span class="sxs-lookup"><span data-stu-id="169c8-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="169c8-200">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="169c8-200">Summary</span></span>

* <span data-ttu-id="169c8-201">Można łatwo zaimplementować rejestrowania i obsługi błędów w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="169c8-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="169c8-202">Usługi DocumentDB można użyć jako repozytorium hello rekordów dziennika i błąd (dokumentów).</span><span class="sxs-lookup"><span data-stu-id="169c8-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="169c8-203">Można użyć toocreate MVC dziennika toodisplay portalu i rejestruje błąd.</span><span class="sxs-lookup"><span data-stu-id="169c8-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="169c8-204">Kod źródłowy</span><span class="sxs-lookup"><span data-stu-id="169c8-204">Source code</span></span>

<span data-ttu-id="169c8-205">Kod źródłowy Hello hello Zarządzanie wyjątkami aplikacje logiki aplikacji interfejsu API jest dostępna w tym [repozytorium GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API zarządzania wyjątków aplikacji logiki").</span><span class="sxs-lookup"><span data-stu-id="169c8-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="169c8-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="169c8-206">Next steps</span></span>

* [<span data-ttu-id="169c8-207">Wyświetl więcej logiki aplikacji przykłady i scenariusze</span><span class="sxs-lookup"><span data-stu-id="169c8-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="169c8-208">Więcej informacji na temat monitorowania aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="169c8-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="169c8-209">Tworzenie szablonów automatycznego wdrażania dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="169c8-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
