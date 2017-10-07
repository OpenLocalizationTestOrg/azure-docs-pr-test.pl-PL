---
title: "aaaScheduler uwierzytelniania połączeń wychodzących"
description: "Uwierzytelnianie połączeń wychodzących harmonogramu"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>Uwierzytelnianie połączeń wychodzących harmonogramu
Harmonogram zadań może być konieczne toocall limit tooservices, która wymaga uwierzytelniania. W ten sposób usługa o nazwie może określić, jeśli zadanie harmonogramu hello dostęp do jej zasobów. Niektóre z tych usług obejmują innych usług platformy Azure, witryny Salesforce.com, Facebook i bezpieczne niestandardowych witryn sieci Web.

## <a name="adding-and-removing-authentication"></a>Dodawanie i usuwanie uwierzytelniania
Dodawanie uwierzytelniania tooa harmonogramu zadania jest proste — dodawanie elementu podrzędnego JSON `authentication` toohello `request` elementu podczas tworzenia lub aktualizowania zadania. Klucze tajne przekazano usługa Harmonogram toohello żądania PUT, PATCH lub POST — jako część hello `authentication` obiektu — nigdy nie są zwracane w odpowiedzi. W odpowiedzi na tajnych informacji ustawiono toonull lub może mieć publicznych token, który reprezentuje jednostkę hello uwierzytelniony.

Uwierzytelnianie tooremove PUT lub poprawka zadania hello jawnie, ustawienie hello `authentication` obiekt toonull. Nie będą widzieć żadnych właściwości uwierzytelniania w odpowiedzi.

Obecnie hello obsługiwane tylko typy uwierzytelniania są hello `ClientCertificate` model (przy użyciu certyfikatów klienta SSL/TLS hello), hello `Basic` modelu (dla uwierzytelniania podstawowego) i hello `ActiveDirectoryOAuth` (dla OAuth usługi Active Directory uwierzytelnianie).

## <a name="request-body-for-clientcertificate-authentication"></a>Treść żądania uwierzytelniania ClientCertificate
Podczas dodawania uwierzytelnianie przy użyciu hello `ClientCertificate` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.  

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania za pomocą certyfikatu klienta SSL. |
| *Typ* |Wymagany. Typ uwierzytelniania. W przypadku certyfikatów SSL klienta hello wartość musi być `ClientCertificate`. |
| *PFX* |Wymagany. Algorytmem Base64 zawartość pliku PFX hello. |
| *hasło* |Wymagany. Plik PFX hello tooaccess hasła. |

## <a name="response-body-for-clientcertificate-authentication"></a>Treść odpowiedzi ClientCertificate uwierzytelniania
Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania za pomocą certyfikatu klienta SSL. |
| *Typ* |Typ uwierzytelniania. Dla certyfikatów klienta SSL, wartość hello jest `ClientCertificate`. |
| *certificateThumbprint* |Witaj odcisk palca certyfikatu hello. |
| *certificateSubjectName* |Witaj podmiotu nazwa wyróżniająca hello certyfikatu. |
| *certificateExpiration* |Data wygaśnięcia Hello hello certyfikatu. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Przykładowe żądanie REST ClientCertificate uwierzytelniania
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Przykładowa odpowiedź REST ClientCertificate uwierzytelniania
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>Treść żądania dla uwierzytelniania podstawowego
Podczas dodawania uwierzytelnianie przy użyciu hello `Basic` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania dla uwierzytelniania podstawowego. |
| *Typ* |Wymagany. Typ uwierzytelniania. W przypadku uwierzytelniania podstawowego hello wartość musi być `Basic`. |
| *Nazwa użytkownika* |Wymagany. Tooauthenticate nazwy użytkownika. |
| *hasło* |Wymagany. Tooauthenticate hasła. |

## <a name="response-body-for-basic-authentication"></a>Treść odpowiedzi dla uwierzytelniania podstawowego
Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania dla uwierzytelniania podstawowego. |
| *Typ* |Typ uwierzytelniania. W przypadku uwierzytelniania podstawowego jest wartość hello `Basic`. |
| *Nazwa użytkownika* |Witaj uwierzytelnić nazwę użytkownika. |

## <a name="sample-rest-request-for-basic-authentication"></a>Przykładowe żądanie REST dla uwierzytelniania podstawowego
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>Przykładowa odpowiedź REST dla uwierzytelniania podstawowego
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Treść żądania uwierzytelniania ActiveDirectoryOAuth
Podczas dodawania uwierzytelnianie przy użyciu hello `ActiveDirectoryOAuth` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania dla uwierzytelniania ActiveDirectoryOAuth. |
| *Typ* |Wymagany. Typ uwierzytelniania. W przypadku uwierzytelniania ActiveDirectoryOAuth hello wartość musi być `ActiveDirectoryOAuth`. |
| *dzierżawy* |Wymagany. Identyfikator dzierżawy Hello dzierżawy hello Azure AD. |
| *grupy odbiorców* |Wymagany. Ta opcja jest ustawiona toohttps://management.core.windows.net/. |
| *clientId* |Wymagany. Podaj identyfikator klienta hello hello aplikacji usługi Azure AD. |
| *klucz tajny* |Wymagany. Klucz tajny klienta hello, który żąda hello token. |

### <a name="determining-your-tenant-identifier"></a>Określanie identyfikatora dzierżawcy
Uzyskać identyfikator dzierżawy hello dzierżawy hello Azure AD, uruchamiając `Get-AzureAccount` w programie Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Treść odpowiedzi uwierzytelniania ActiveDirectoryOAuth
Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.

| Element | Opis |
|:--- |:--- |
| *uwierzytelnianie (element nadrzędny)* |Obiekt uwierzytelniania dla uwierzytelniania ActiveDirectoryOAuth. |
| *Typ* |Typ uwierzytelniania. W przypadku uwierzytelniania ActiveDirectoryOAuth wartość hello jest `ActiveDirectoryOAuth`. |
| *dzierżawy* |Identyfikator dzierżawy Hello dzierżawy hello Azure AD. |
| *grupy odbiorców* |Ta opcja jest ustawiona toohttps://management.core.windows.net/. |
| *clientId* |Witaj identyfikator klienta aplikacji hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Przykładowe żądanie REST ActiveDirectoryOAuth uwierzytelniania
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Przykładowa odpowiedź REST ActiveDirectoryOAuth uwierzytelniania
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

