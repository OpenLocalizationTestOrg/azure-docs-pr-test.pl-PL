---
title: aaaValidate XML - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Walidacja danych XML o schematach dla usługi Azure Logic Apps i scenariusze B2B przy użyciu hello pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Walidacja danych XML dla integracji przedsiębiorstwa

Często w scenariusze B2B hello partnerzy umowy należy się upewnić, wiadomości powitania wymieniają są prawidłowe, przed rozpoczęciem przetwarzania danych. Dokumenty schematem wstępnie zdefiniowanych można sprawdzić za pomocą łącznika sprawdzanie poprawności kodu XML hello Użyj hello w hello pakiet integracyjny dla przedsiębiorstw.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Sprawdź poprawność dokumentu hello łącznik sprawdzanie poprawności kodu XML

1. Tworzenie aplikacji logiki, i [połączenia konta integracji toohello aplikacji hello](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się toolink aplikacji logiki tooa konta integracji") mający schematu hello ma toouse sprawdzania poprawności danych XML.

2. Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** aplikacji logiki tooyour wyzwalacza.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. Witaj tooadd **sprawdzanie poprawności kodu XML** akcji, wybierz **Dodaj akcję**.

4. Wprowadź toofilter wszystkie hello toohello akcji, który chcesz, *xml* hello pola wyszukiwania. Wybierz **sprawdzanie poprawności kodu XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Wybierz hello toospecify zawartość XML, które mają toovalidate, **zawartości**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Wybierz znacznik treści hello hello zawartości, które mają toovalidate.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. Schemat hello toospecify ma toouse sprawdzania poprawności hello poprzedniej *zawartości* danych wejściowych, wybierz **nazwy SCHEMATU**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Zapisz swoją pracę  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Wykonuje się teraz w skonfigurowaniu łącznika z weryfikacji. W przypadku aplikacji rzeczywistych można toostore hello sprawdzania poprawności danych w aplikacji — biznesowych (LOB) takie jak SalesForce. toosend hello tooSalesforce zweryfikowanych danych wyjściowych, Dodaj akcję.

tootest Twoje działanie sprawdzania poprawności należy punktu końcowego toohello HTTP żądania.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")   

