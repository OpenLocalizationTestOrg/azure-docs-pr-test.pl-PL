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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Scenariusz: Obsługa wyjątków i rejestrowania błędów dla usługi logic apps

W tym scenariuszu opisano, jak można rozszerzyć obsługi logiki aplikacji toobetter obsługi wyjątków. Firma Microsoft używano pytanie hello tooanswer przypadków użycia rzeczywistych: "Aplikacje logiki platformy Azure obsługuje wyjątek i obsługa błędów?"

> [!NOTE]
> bieżący schemat Azure Logic Apps Hello udostępnia standardowy szablon dla akcji odpowiedzi. Ten szablon zawiera wewnętrznego sprawdzania poprawności i odpowiedzi na błędy zwrócone przez aplikację interfejsu API.

## <a name="scenario-and-use-case-overview"></a>Omówienie scenariusza i użyj case

Oto wątku hello jako hello przypadek użycia dla tego scenariusza: 

Dobrze znane organizacji opieki zdrowotnej zaangażowane nam toodevelop Azure rozwiązania, które spowoduje utworzenie pacjenta portalu przy użyciu programu Microsoft Dynamics CRM Online. Zachodzi potrzeba toosend termin rekordów hello Dynamics CRM Online pacjenta portalu i Salesforce. Firma Microsoft zostały zadawane toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standardowe dla wszystkich pacjenta rekordów.

Projekt Hello ma dwa główne wymagania:  

* Rekordy toolog metody wysyłane z hello portalu Dynamics CRM Online
* Tooview sposób wszelkie błędy, które wystąpiły w przepływie pracy hello

> [!TIP]
> Film wysokiego poziomu dotyczących tego projektu, zobacz [grupy użytkowników integracji](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupy użytkowników integracji").

## <a name="how-we-solved-hello-problem"></a>Jak możemy rozwiązać hello problem

Wybraliśmy [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/ "bazy danych Azure rozwiązania Cosmos") jako repozytorium rekordów dziennika i błąd hello (DB rozwiązania Cosmos odwołuje się toorecords jako dokumentów). Ponieważ aplikacje logiki platformy Azure ma standardowy szablon wszystkie odpowiedzi, firma Microsoft nie będzie zawierało toocreate schematu niestandardowego. Można utworzyć aplikację interfejsu API za**Wstaw** i **zapytania** rekordów zarówno błędu, jak i dziennika. Również definiowania schematu dla każdego poziomu hello aplikacji interfejsu API.  

Innym wymogiem jest rekordów toopurge po określonej dacie. Rozwiązania cosmos bazy danych ma właściwość o nazwie [czasu tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "czasu tooLive") (TTL), które mogą nam tooset **czasu tooLive** wartość dla każdego rekordu lub kolekcji. Ta funkcja została wyeliminowana hello muszą toomanually usuwania rekordów w bazie danych rozwiązania Cosmos.

> [!IMPORTANT]
> toocomplete tego samouczka potrzebne toocreate bazy danych DB rozwiązania Cosmos i dwie kolekcje (rejestrowania i błędów).

## <a name="create-hello-logic-app"></a>Tworzenie aplikacji logiki hello

Witaj pierwszym krokiem jest aplikacji logiki hello toocreate i aplikacji hello Otwórz w Projektancie aplikacji logiki. W tym przykładzie użyto aplikacje logiki nadrzędny podrzędny. Załóżmy, że firma Microsoft hello nadrzędnego jest już utworzony i będzie toocreate jeden podrzędny logiki aplikacji.

Ponieważ zamierzamy rekordu hello toolog wystawała Dynamics CRM Online, Zacznijmy u góry hello. Możemy użyć **żądania** wyzwolenia ponieważ aplikacji logiki nadrzędnego hello wyzwala tego dziecka.

### <a name="logic-app-trigger"></a>Wyzwalaczem aplikacji logiki

Używamy **żądania** wyzwalania, jak pokazano w hello poniższy przykład:

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


## <a name="steps"></a>Kroki

Firma Microsoft musi zarejestrować hello źródła (żądanie) rekordu pacjenta hello hello portalu Dynamics CRM Online.

1. Firma Microsoft musi uzyskać nowy rekord terminu z programu Dynamics CRM Online.

   wyzwalacz Hello pochodzące z CRM zapewnia hello **CRM PatentId**, **typu rekordu**, **nowe lub zaktualizowane rekordu** (nowej lub zaktualizuj wartość logiczna), i ** SalesforceId**. Witaj **SalesforceId** może mieć wartości null, ponieważ jest ona używana tylko dla aktualizacji.
   Uzyskujemy hello CRM rekordu przy użyciu hello CRM **PatientID** i hello **typu rekordu**.

2. Następnie należy tooadd aplikacji interfejsu API usługi DocumentDB **InsertLogEntry** operacji, jak pokazano w Projektancie aplikacji logiki.

   **Wstaw wpis dziennika**

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Wstaw wpis błędu**

   ![Wstaw wpis dziennika](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Sprawdź, czy utworzyć rekord błędu**

   ![Warunek](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Kod źródłowy aplikacji logiki

> [!NOTE]
> Następujące przykłady Hello są tylko próbek. Ponieważ w tym samouczku jest oparty na implementacji teraz w środowisku produkcyjnym, hello wartość **węzeł źródłowy** może nie wyświetlać właściwości, które są powiązane tooscheduling terminu. > 

### <a name="logging"></a>Rejestrowanie

jak przedstawiono przykładowe Hello następującego kodu aplikacji logiki toohandle rejestrowania.

#### <a name="log-entry"></a>Wpis dziennika

Oto kod źródłowy aplikacji hello logikę wstawiania wpis dziennika.

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

#### <a name="log-request"></a>Żądanie dziennika

Oto komunikat żądania dziennika hello zaksięgowany toohello aplikacji interfejsu API.

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


#### <a name="log-response"></a>Odpowiedź dziennika

Oto komunikat odpowiedzi dziennika hello z hello aplikacji interfejsu API.

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

Teraz Przyjrzyjmy się obsługi kroki hello błędów.

### <a name="error-handling"></a>Obsługa błędów

Witaj Poniższy przykładowy kod aplikacji logiki pokazuje sposoby implementowania obsługi błędów.

#### <a name="create-error-record"></a>Utwórz rekord błędu

Oto kod źródłowy aplikacji logiki hello tworzenia rekord błędu.

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

#### <a name="insert-error-into-cosmos-db--request"></a>Wstaw błędu w bazie danych rozwiązania Cosmos--żądania

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

#### <a name="insert-error-into-cosmos-db--response"></a>Wstaw błędu w bazie danych rozwiązania Cosmos--odpowiedzi

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

#### <a name="salesforce-error-response"></a>Odpowiedzi na błąd SalesForce

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

### <a name="return-hello-response-back-tooparent-logic-app"></a>Zwraca hello odpowiedzi wstecz tooparent logiki aplikacji

Po uzyskaniu odpowiedzi hello można przekazać odpowiedź hello aplikacji logiki nadrzędnej toohello Wstecz.

#### <a name="return-success-response-tooparent-logic-app"></a>Zwraca sukces odpowiedzi tooparent logiki aplikacji

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

#### <a name="return-error-response-tooparent-logic-app"></a>Aplikacja logiki tooparent odpowiedzi zwróciła błąd

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


## <a name="cosmos-db-repository-and-portal"></a>Repozytorium rozwiązania cosmos bazy danych i portal

Nasze rozwiązanie dodane możliwości za pomocą [DB rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Błąd portalu zarządzania

tooview hello błędy, można tworzyć MVC sieci web aplikacji toodisplay hello błąd rekordy z bazy danych rozwiązania Cosmos. Hello **listy**, **szczegóły**, **Edytuj**, i **usunąć** operacji znajdują się w bieżącej wersji powitania.

> [!NOTE]
> Operacji edycji: rozwiązania Cosmos DB zastępuje hello całego dokumentu. Witaj rekordów wyświetlanych w hello **listy** i **szczegółów** widoki są tylko próbek. Nie są one rzeczywiste termin pacjenta rekordów.

Poniżej przedstawiono przykłady naszej aplikacji MVC szczegóły wcześniej utworzony hello opisane podejście.

#### <a name="error-management-list"></a>Błąd listy zarządzania.
![Lista błędów](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Błąd: widok szczegółów zarządzania
![Szczegóły błędu](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Portal zarządzania dziennika

Dzienniki hello tooview, również utworzono aplikację sieci web MVC. Poniżej przedstawiono przykłady naszej aplikacji MVC szczegóły wcześniej utworzony hello opisane podejście.

#### <a name="sample-log-detail-view"></a>Przykładowy widok szczegółów dziennika
![Dziennik: widok szczegółów](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Szczegóły aplikacji interfejsu API

#### <a name="logic-apps-exception-management-api"></a>Zarządzanie wyjątkami logiki aplikacji interfejsu API

Open source aplikacji interfejsu API zarządzania wyjątek usługi Azure Logic Apps udostępnia funkcje, zgodnie z opisem w tym miejscu — istnieją dwa kontrolery:

* **ErrorController** wstawia rekord błędu (dokument) w kolekcji usługi DocumentDB.
* **LogController** wstawia rekordu dziennika (dokument) w kolekcji usługi DocumentDB.

> [!TIP]
> Zarówno kontrolery `async Task<dynamic>` czynności tooresolve operacji w czasie wykonywania, więc można utworzyć hello schematu usługi DocumentDB w treści hello hello operacji. 
> 

Każdy dokument w usłudze DocumentDB musi mieć unikatowy identyfikator. Używamy `PatientId` i Dodawanie znaczników czasu, który jest przekonwertować wartość sygnatury czasowej systemu Unix tooa (o podwójnej precyzji). Firma Microsoft obciąć hello tooremove hello ułamkowych wartość.

Można wyświetlić kodu źródłowego hello błąd kontrolera interfejsu API [z usługi GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Nazywamy hello interfejsu API z aplikacji logiki przy użyciu hello następującej składni:

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

Witaj wyrażenie w hello poprzedzających sprawdza przykładowy kod hello *Create_NewPatientRecord* stan ****.

## <a name="summary"></a>Podsumowanie

* Można łatwo zaimplementować rejestrowania i obsługi błędów w aplikacji logiki.
* Usługi DocumentDB można użyć jako repozytorium hello rekordów dziennika i błąd (dokumentów).
* Można użyć toocreate MVC dziennika toodisplay portalu i rejestruje błąd.

### <a name="source-code"></a>Kod źródłowy

Kod źródłowy Hello hello Zarządzanie wyjątkami aplikacje logiki aplikacji interfejsu API jest dostępna w tym [repozytorium GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API zarządzania wyjątków aplikacji logiki").

## <a name="next-steps"></a>Następne kroki

* [Wyświetl więcej logiki aplikacji przykłady i scenariusze](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Więcej informacji na temat monitorowania aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Tworzenie szablonów automatycznego wdrażania dla usługi logic apps](../logic-apps/logic-apps-create-deploy-template.md)
