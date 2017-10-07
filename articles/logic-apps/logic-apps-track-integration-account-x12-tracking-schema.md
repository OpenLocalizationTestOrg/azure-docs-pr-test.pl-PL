---
title: "schematy śledzenia aaaX12 B2B monitorowania - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Użyj X12 śledzenie wiadomości toomonitor B2B schematów z transakcji na koncie Azure integracji."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Początkowy lub Włącz śledzenie X12 wiadomości toomonitor sukces, błędy i właściwości wiadomości
Można użyć tych X12 śledzenia schematów w Twojej toohelp konta Azure integracji monitorowania transakcji między firmami (B2B):

* X12 transakcji ustawić schematu śledzenia
* X12 transakcji ustawić potwierdzenia śledzenia schematu
* X12 interchange schematu śledzenia
* X12 interchange potwierdzenia śledzenia schematu
* X12 funkcjonalności grupy schematu śledzenia
* X12 funkcjonalności grupy potwierdzenia śledzenia schematu

## <a name="x12-transaction-set-tracking-schema"></a>X12 transakcji ustawić schematu śledzenia
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany formantu. (Opcjonalnie) |
| functionalGroupControlNumber | Ciąg | Numer funkcjonalności formantu. (Opcjonalnie) |
| transactionSetControlNumber | Ciąg | Transakcja Ustaw numer formantu. (Opcjonalnie) |
| correlationMessageId | Ciąg | Identyfikator korelacji wiadomości. Kombinacja {AgreementName} {*GroupControlNumber*} {TransactionSetControlNumber}. (Opcjonalnie) |
| messageType | Ciąg | Transakcja ustawić lub typ dokumentu. (Opcjonalnie) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane) |
| isTechnicalAcknowledgmentExpected | Wartość logiczna | Określa, czy potwierdzenia techniczne hello jest skonfigurowany w hello X12 umowy. (Wymagane) |
| isFunctionalAcknowledgmentExpected | Wartość logiczna | Określa, czy potwierdzenia funkcjonalności hello jest skonfigurowany w umowie hello X12. (Wymagane) |
| needAk2LoopForValidMessages | Wartość logiczna | Określa, czy hello AK2 pętli jest wymagany dla prawidłowego elementu message. (Wymagane) |
| segmentsCount | Liczba całkowita | Ustaw liczbę segmentów w hello X12 transakcji. (Opcjonalnie) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>X12 transakcji ustawić potwierdzenia śledzenia schematu
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany kontroli liczba hello funkcjonalności potwierdzenia. Wypełnia wartość tylko dla hello wysyłania strony, których Odebrano potwierdzenie funkcjonalności toopartner wiadomości powitania. (Opcjonalnie) |
| functionalGroupControlNumber | Ciąg | Grupy funkcjonalnej sterowania liczba hello funkcjonalności potwierdzenia. Wypełnia wartość tylko dla hello wysyłania strony, których Odebrano potwierdzenie funkcjonalności toopartner wiadomości powitania. (Opcjonalnie) |
| isaSegment | Ciąg | Segment ISA wiadomość hello. Wypełnia wartość tylko dla hello wysyłania strony, których Odebrano potwierdzenie funkcjonalności toopartner wiadomości powitania. (Opcjonalnie) |
| gsSegment | Ciąg | Segment GS wiadomość hello. Wypełnia wartość tylko dla hello wysyłania strony, których Odebrano potwierdzenie funkcjonalności toopartner wiadomości powitania. (Opcjonalnie) |
| respondingfunctionalGroupControlNumber | Ciąg | Odpowiada numer formantu wymiany. (Opcjonalnie) |
| respondingFunctionalGroupId | Ciąg | Odpowiada identyfikator grupy funkcjonalne, która mapuje tooAK101 hello potwierdzenia. (Opcjonalnie) |
| respondingtransactionSetControlNumber | Ciąg | Odpowiada transakcji Ustaw numer formantu. (Opcjonalnie) |
| respondingTransactionSetId | Ciąg | Odpowiada transakcji ustawiony identyfikator, który mapuje tooAK201 w hello potwierdzenia. (Opcjonalnie) |
| statusCode | Wartość logiczna | Transakcja Ustaw kod stanu potwierdzenia. (Wymagane) |
| segmentsCount | wyliczenia | Kod stanu potwierdzenia. Dozwolone wartości to **zaakceptowane**, **odrzucone**, i **AcceptedWithErrors**. (Wymagane) |
| processingStatus | wyliczenia | Stan przetwarzania hello potwierdzenia. Dozwolone wartości to **odebrane**, **Generated**, i **wysłane**. (Wymagane) |
| correlationMessageId | Ciąg | Identyfikator korelacji wiadomości. Kombinacja {AgreementName} {*GroupControlNumber*} {TransactionSetControlNumber}. (Opcjonalnie) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane) |
| ak2Segment | Ciąg | Potwierdzenia w grupy funkcjonalnej hello odebranych transakcji. (Opcjonalnie) |
| ak3Segment | Ciąg | Raporty błędów w segmencie danych. (Opcjonalnie) |
| ak5Segment | Ciąg | Raporty, czy ustawić zidentyfikowanych w segmencie hello AK2 transakcji hello jest zaakceptowane lub odrzucone i dlaczego. (Opcjonalnie) |

## <a name="x12-interchange-tracking-schema"></a>X12 interchange schematu śledzenia
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany formantu. (Opcjonalnie) |
| isaSegment | Ciąg | Segment ISA wiadomości. (Opcjonalnie) |
| isTechnicalAcknowledgmentExpected | Wartość logiczna | Określa, czy potwierdzenia techniczne hello jest skonfigurowany w hello X12 umowy. (Wymagane) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane) |
| isa09 | Ciąg | X12 dokumentu wymiany daty. (Opcjonalnie) |
| isa10 | Ciąg | X12 dokumentu czasu wymiany. (Opcjonalnie) |
| isa11 | Ciąg | X12 interchange kontroli identyfikator standardów. (Opcjonalnie) |
| isa12 | Ciąg | Formant interchange X12 numer wersji. (Opcjonalnie) |
| isa14 | Ciąg | X12 żądania potwierdzenia. (Opcjonalnie) |
| isa15 | Ciąg | Wskaźnik do testu lub produkcji. (Opcjonalnie) |
| isa16 | Ciąg | Element separatora. (Opcjonalnie) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>X12 interchange potwierdzenia śledzenia schematu
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany kontroli liczba hello potwierdzenia technicznych, odebrany od partnerów. (Opcjonalnie) |
| isaSegment | Ciąg | Segment ISA hello potwierdzenia technicznych, odebrany od partnerów. (Opcjonalnie) |
| respondingInterchangeControlNumber |Ciąg | Wymiany numer formantu hello potwierdzenia technicznych, odebrany od partnerów. (Opcjonalnie) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane) |
| statusCode | wyliczenia | Wymiany kod stanu potwierdzenia. Dozwolone wartości to **zaakceptowane**, **odrzucone**, i **AcceptedWithErrors**. (Wymagane) |
| processingStatus | wyliczenia | Stan potwierdzenia. Dozwolone wartości to **odebrane**, **Generated**, i **wysłane**. (Wymagane) |
| TA102 | Ciąg | Wymiany daty. (Opcjonalnie) |
| ta103 | Ciąg | Wymiany czasu. (Opcjonalnie) |
| ta105 | Ciąg | Wymiany Uwaga kodu. (Opcjonalnie) |

## <a name="x12-functional-group-tracking-schema"></a>X12 funkcjonalności grupy schematu śledzenia
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany formantu. (Opcjonalnie) |
| functionalGroupControlNumber | Ciąg | Numer funkcjonalności formantu. (Opcjonalnie) |
| gsSegment | Ciąg | Komunikat GS segment. (Opcjonalnie) |
| isTechnicalAcknowledgmentExpected | Wartość logiczna | Określa, czy potwierdzenia techniczne hello jest skonfigurowany w hello X12 umowy. (Wymagane) |
| isFunctionalAcknowledgmentExpected | Wartość logiczna | Określa, czy potwierdzenia funkcjonalności hello jest skonfigurowany w umowie hello X12. (Wymagane) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane)|
| gs01 | Ciąg | Kod identyfikatora funkcjonalności. (Opcjonalnie) |
| gs02 | Ciąg | Kod aplikacji nadawcy. (Opcjonalnie) |
| gs03 | Ciąg | Kod aplikacji odbiornika. (Opcjonalnie) |
| gs04 | Ciąg | Data grupy funkcjonalne. (Opcjonalnie) |
| gs05 | Ciąg | Czas grupy funkcjonalne. (Opcjonalnie) |
| gs07 | Ciąg | Kod właściwej agencji. (Opcjonalnie) |
| gs08 | Ciąg | Identyfikator wersji/wydania/branży kodu. (Opcjonalnie) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>X12 funkcjonalności grupy potwierdzenia śledzenia schematu
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| senderPartnerName | Ciąg | X12 komunikatów nadawcę partnera. (Opcjonalnie) |
| receiverPartnerName | Ciąg | X12 komunikatów Nazwa partnera odbiorcy. (Opcjonalnie) |
| senderQualifier | Ciąg | Wyślij kwalifikator partnera. (Wymagane) |
| senderIdentifier | Ciąg | Wyślij identyfikator partnera. (Wymagane) |
| receiverQualifier | Ciąg | Odbieranie kwalifikator partnera. (Wymagane) |
| receiverIdentifier | Ciąg | Wyświetlony identyfikator partnera. (Wymagane) |
| agreementName | Ciąg | Nazwa hello X12 wiadomości powitania toowhich umowy zostaną rozwiązane. (Opcjonalnie) |
| Kierunek | wyliczenia | Kierunek przepływu wiadomość hello, odbierać lub wysyłać. (Wymagane) |
| interchangeControlNumber | Ciąg | Wymiany numer formant, który wypełnia dla strony wysyłania powitania po otrzymaniu potwierdzenia techniczne od partnerów. (Opcjonalnie) |
| functionalGroupControlNumber | Ciąg | Numer formantu grupy funkcjonalnej hello techniczne potwierdzenia, które wypełnia dla hello wysyłać po stronie, gdy techniczne potwierdzenia partnerów. (Opcjonalnie) |
| isaSegment | Ciąg | Identyczny wymiany kontrolować numerem, ale tylko w szczególnych przypadkach wypełnione. (Opcjonalnie) |
| gsSegment | Ciąg | Grupą funkcjonalne kontrolować numerem, ale tylko w szczególnych przypadkach wypełnione. (Opcjonalnie) |
| respondingfunctionalGroupControlNumber | Ciąg | Liczba kontroli oryginalnego grupy funkcjonalnej hello. (Opcjonalnie) |
| respondingFunctionalGroupId | Ciąg | Mapuje tooAK101 w identyfikatorze hello potwierdzenia grupy funkcjonalne. (Opcjonalnie) |
| isMessageFailed | Wartość logiczna | Określa, czy wiadomość hello X12 nie powiodło się. (Wymagane) |
| statusCode | wyliczenia | Kod stanu potwierdzenia. Dozwolone wartości to **zaakceptowane**, **odrzucone**, i **AcceptedWithErrors**. (Wymagane) |
| processingStatus | wyliczenia | Stan przetwarzania hello potwierdzenia. Dozwolone wartości to **odebrane**, **Generated**, i **wysłane**. (Wymagane) |
| ak903 | Ciąg | Liczba odebranych zestawy transakcji. (Opcjonalnie) |
| ak904 | Ciąg | Liczba transakcji zestawów akceptowane hello zidentyfikowane funkcjonalne grupy. (Opcjonalnie) |
| ak9Segment | Ciąg | Czy grupy funkcjonalne hello określonych w segmencie hello AK1 jest zaakceptowane lub odrzucone i dlaczego. (Opcjonalnie) |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [monitorowanie wiadomości B2B](logic-apps-monitor-b2b-message.md).
* Dowiedz się więcej o [AS2 śledzenia schematy](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Dowiedz się więcej o [B2B niestandardowych schematów śledzenia](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Dowiedz się więcej o [śledzenie wiadomości B2B w portalu usługi Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Dowiedz się więcej o hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).  
