---
title: "Śledzenie schematy B2B aaaCustom monitorowania - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz schematy śledzenia niestandardowych toomonitor B2B wiadomości transakcji na koncie integracji Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Włącz śledzenie toomonitor ukończenia przepływu pracy, end-to-end
Są wbudowane, śledzenie, możesz włączyć dla różnych części przepływu pracy business-to-business, takie jak śledzenie AS2 lub X12 wiadomości. Podczas tworzenia przepływów pracy, które zawiera aplikację logiki, BizTalk Server, SQL Server lub inną warstwę, można włączyć śledzenie niestandardowej, która zapisuje zdarzenia z hello początek toohello koniec przepływu pracy. 

Ten temat zawiera kod niestandardowy, który można użyć w warstwach hello poza aplikację logiki. 

## <a name="custom-tracking-schema"></a>Schemat niestandardowy śledzenia
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Właściwość | Typ | Opis |
| --- | --- | --- |
| Źródłowa |   | Typ źródła hello Uruchom. Dozwolone wartości to **Microsoft.Logic/workflows** i **niestandardowych**. (Wymagane) |
| Element źródłowy |   | Jeśli typ źródła hello jest **Microsoft.Logic/workflows**, informacje o źródle hello musi toofollow tego schematu. Jeśli typ źródła hello jest **niestandardowe**, schemat hello jest JToken. (Wymagane) |
| systemId | Ciąg | Identyfikator logiki aplikacji systemu. (Wymagane) |
| przebiegu | Ciąg | Uruchom identyfikatora aplikacji logiki (Wymagane) |
| operationName | Ciąg | Nazwa operacji hello (na przykład, akcji lub wyzwalacz). (Wymagane) |
| repeatItemScopeName | Ciąg | Powtórz nazwa elementu, jeśli akcja hello znajduje się wewnątrz `foreach` / `until` pętli. (Wymagane) |
| repeatItemIndex | Liczba całkowita | Czy hello akcji znajduje się wewnątrz `foreach` / `until` pętli. Wskazuje indeks elementu powtarzanego hello. (Wymagane) |
| trackingId | Ciąg | Identyfikator śledzenia wiadomości powitania toocorrelate. (Opcjonalnie) |
| correlationId | Ciąg | Identyfikator korelacji wiadomości powitania toocorrelate. (Opcjonalnie) |
| ClientRequestId | Ciąg | Klienta można umieścić w nim toocorrelate wiadomości. (Opcjonalnie) |
| eventLevel |   | Poziom hello zdarzeń. (Wymagane) |
| eventTime |   | Godzina zdarzenia hello w formacie UTC RRRR-MM-DDTHH:MM:SS.00000Z. (Wymagane) |
| recordType |   | Typ hello ścieżki. Dozwolone wartości to **niestandardowych**. (Wymagane) |
| rekord |   | Typ niestandardowy rekord. Dozwolony format to JToken. (Wymagane) |

## <a name="b2b-protocol-tracking-schemas"></a>Schematy śledzenia protokołu B2B
Aby uzyskać informacji na temat protokołu B2B śledzenia schematów zobacz:
* [Schematy śledzenia AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Schematy śledzenia X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [monitorowanie wiadomości B2B](logic-apps-monitor-b2b-message.md).   
* Dowiedz się więcej o [śledzenie wiadomości B2B w portalu usługi Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Dowiedz się więcej o hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).
