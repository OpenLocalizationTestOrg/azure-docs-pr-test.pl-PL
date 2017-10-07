---
title: "schematy śledzenia aaaAS2 B2B monitorowania - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Użyj AS2 śledzenie wiadomości toomonitor B2B schematów z transakcji na koncie Azure integracji."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Uruchom lub włączyć śledzenie wiadomości AS2 MDNs toomonitor sukces, błędy i właściwości wiadomości
Można użyć tych schematów śledzenia AS2 w Twojej toohelp konta Azure integracji monitorowania transakcji między firmami (B2B):

* AS2 komunikatów śledzenia schematu
* Schemat śledzenia AS2 MDN

## <a name="as2-message-tracking-schema"></a>AS2 komunikatów śledzenia schematu
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | Nazwa partnera nadawcy wiadomości AS2. (Opcjonalnie) |
| receiverPartnerName | Ciąg | Nazwa partnera AS2 komunikat odbiornika. (Opcjonalnie) |
| as2To | Ciąg | Nazwa odbiornika AS2 wiadomości z nagłówków hello wiadomości powitania AS2. (Wymagane) |
| as2From | Ciąg | Nazwa nadawcy wiadomości AS2 z nagłówków hello wiadomości powitania AS2. (Wymagane) |
| agreementName | Ciąg | Nazwa wiadomości powitania toowhich umowy AS2 hello są rozpoznawane. (Opcjonalnie) |
| Kierunek | Ciąg | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| Identyfikator komunikatu | Ciąg | Identyfikator komunikatu AS2, z nagłówków hello wiadomości powitania AS2 (opcjonalnie) |
| dispositionType |Ciąg | Wartość typu dyspozycji dyspozycji powiadomienia (MDN) wiadomości. (Opcjonalnie) |
| fileName | Ciąg | Nazwa pliku z hello nagłówka wiadomości powitania AS2. (Opcjonalnie) |
| isMessageFailed |Wartość logiczna | Określa, czy wiadomość hello AS2 nie powiodło się. (Wymagane) |
| isMessageSigned | Wartość logiczna | Określa, czy wiadomość hello AS2 została podpisana. (Wymagane) |
| isMessageEncrypted | Wartość logiczna | Określa, czy wiadomość hello AS2 została zaszyfrowana. (Wymagane) |
| isMessageCompressed |Wartość logiczna | Określa, czy wiadomość hello AS2 został poddany kompresji. (Wymagane) |
| correlationMessageId | Ciąg | Identyfikator komunikatu AS2, toocorrelate wiadomości z MDNs. (Opcjonalnie) |
| incomingHeaders |Słownik JToken | Szczegóły nagłówka komunikatu przychodzącego AS2. (Opcjonalnie) |
| outgoingHeaders |Słownik JToken | Szczegóły nagłówka wiadomości wychodzącej AS2. (Opcjonalnie) |
| isNrrEnabled | Wartość logiczna | Użyj wartości domyślnej, jeśli wartość hello jest nieznana. (Wymagane) |
| isMdnExpected | Wartość logiczna | Użyj wartości domyślnej, jeśli wartość hello jest nieznana. (Wymagane) |
| mdnType | wyliczenia | Dozwolone wartości to **NotConfigured**, **synchronizacji**, i **Async**. (Wymagane) |

## <a name="as2-mdn-tracking-schema"></a>Schemat śledzenia AS2 MDN
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | Nazwa partnera nadawcy wiadomości AS2. (Opcjonalnie) |
| receiverPartnerName | Ciąg | Nazwa partnera AS2 komunikat odbiornika. (Opcjonalnie) |
| as2To | Ciąg | Nazwa partnera, który odbiera wiadomość hello AS2. (Wymagane) |
| as2From | Ciąg | Nazwa partnera, który wysyła wiadomości powitania AS2. (Wymagane) |
| agreementName | Ciąg | Nazwa wiadomości powitania toowhich umowy AS2 hello są rozpoznawane. (Opcjonalnie) |
| Kierunek |Ciąg | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| Identyfikator komunikatu | Ciąg | Identyfikator komunikatu AS2. (Opcjonalnie) |
| originalMessageId |Ciąg | Identyfikator AS2 oryginalnej wiadomości. (Opcjonalnie) |
| dispositionType | Ciąg | Wartość typu dyspozycji MDN. (Opcjonalnie) |
| isMessageFailed |Wartość logiczna | Określa, czy wiadomość hello AS2 nie powiodło się. (Wymagane) |
| isMessageSigned |Wartość logiczna | Określa, czy wiadomość hello AS2 została podpisana. (Wymagane) |
| isNrrEnabled | Wartość logiczna | Użyj wartości domyślnej, jeśli wartość hello jest nieznana. (Wymagane) |
| statusCode | wyliczenia | Dozwolone wartości to **zaakceptowane**, **odrzucone**, i **AcceptedWithErrors**. (Wymagane) |
| micVerificationStatus | wyliczenia | Dozwolone wartości to **NotApplicable**, **zakończyło się pomyślnie**, i ****. (Wymagane) |
| correlationMessageId | Ciąg | Identyfikator korelacji. Identyfikator messaged Hello oryginalnego (hello identyfikator komunikatu wiadomości powitania, dla której skonfigurowano MDN). (Opcjonalnie) |
| incomingHeaders | Słownik JToken | Wskazuje szczegóły nagłówka komunikatu przychodzącego. (Opcjonalnie) |
| outgoingHeaders |Słownik JToken | Wskazuje szczegóły nagłówka komunikatu wychodzącego. (Opcjonalnie) |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Dowiedz się więcej o [monitorowanie wiadomości B2B](logic-apps-monitor-b2b-message.md).   
* Dowiedz się więcej o [B2B niestandardowych schematów śledzenia](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Dowiedz się więcej o [X12 śledzenia schematy](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Dowiedz się więcej o [śledzenie wiadomości B2B w portalu usługi Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
