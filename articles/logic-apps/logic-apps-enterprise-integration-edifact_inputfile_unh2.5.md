---
title: "aaaLogic B2B aplikacje dekodowania edifact rozwiązać UNH2.5 - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Azure B2B aplikacje logiki dekodowania edifact rozwiązać UNH2.5"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Jak toohandle EDIFACT dokumentów o UNH2.5 segmentu
Gdy UNH2.5 znajduje się w dokumencie EDIFACT hello, jest używany do wyszukiwania schematu. 

Przykład: pole UNH hello jest **EAN008** w wiadomości powitania EDIFACT  
UNH + SSDD1 + ZAMÓWIEŃ: D: 03B: UN:**EAN008**"  

Wiadomości powitania toohandle toofollow kroki 
1. Aktualizacja schematu hello
2. Sprawdź ustawienia umowy hello  

## <a name="update-hello-schema"></a>Aktualizacja schematu hello
wiadomości powitania tooprocess, należy toodeploy schematu z nazwa węzła głównego UNH2.5 hello.  Dla danego przykładem, nazwa głównego schematu hello jest **EFACT_D03B_ORDERS_EAN008**  

Dla każdego D03B_ORDERS inny segment UNH2.5 trzeba toodeploy poszczególnych schematu.  

## <a name="add-schema-toohello-edifact-agreement"></a>Dodawanie umowy EDIFACT toohello schematu
### <a name="edifact-decode"></a>Dekodowanie EDIFACT
tooDecode przychodząca wiadomość hello, skonfiguruj hello schematu w hello EDIFACT umowy odbierają ustawienia
1. Dodaj konto integracji toohello schematu hello    
2. Konfigurowanie schematu hello w hello EDIFACT umowy odbierają ustawienia. 
3. Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.  Dodaj wartość UNH2.5 w hello umowy Receive **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Kodowanie EDIFACT
tooEncode przychodząca wiadomość hello, skonfiguruj hello schematu w ustawieniach wysyłania umowy EDIFACT hello
1. Dodaj konto integracji toohello schematu hello    
2. Skonfiguruj hello schematu w ustawieniach wysyłania umowy EDIFACT hello. 
3. Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.  Dodaj wartość UNH2.5 w hello wysyłania umowy **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o integracji konta umów](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  