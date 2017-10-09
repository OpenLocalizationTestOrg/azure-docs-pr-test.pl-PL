---
title: "komunikaty aaaEncode AS2 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak toouse hello kodera AS2 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Kodowanie wiadomości AS2 dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw

tooestablish bezpieczeństwa i niezawodności podczas przesyłania wiadomości, należy użyć hello AS2 kodowania komunikatu łącznika. Ten łącznik umożliwia cyfrowe podpisywanie, szyfrowanie i potwierdzeń za pośrednictwem wiadomości dyspozycji powiadomienia (MDN), które również prowadzi toosupport dla Niemożność wyparcia się.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznika integracji konta toouse hello AS2 kodowania komunikatu.
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [Umowy AS2](logic-apps-enterprise-integration-as2.md) jest już zdefiniowany w ramach konta integracji

## <a name="encode-as2-messages"></a>Kodowanie wiadomości AS2

1. [Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Hello AS2 kodowania komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3.  W polu wyszukiwania hello wprowadź "AS2" filtru. Wybierz **AS2 - AS2 kodowania komunikatu**.
   
    ![Wyszukaj "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect. 
   
    ![Utwórz konto toointegration połączeń](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

5.  Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis. Wybierz toofinish Tworzenie połączenia **Utwórz**.
   
    ![Szczegóły połączenia integracji](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, podaj szczegóły **AS2 — od**, **AS2 tooidentifiers** zgodnie z konfiguracją w umowie, i **treści**, który jest Witaj ładunek komunikatu.
   
    ![Podaj wymagane pola](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Szczegóły kodera AS2

Łącznik AS2 kodowania Hello wykonuje te zadania: 

* Stosuje nagłówków AS2/HTTP
* Znaki wychodzących wiadomości (jeśli jest skonfigurowane)
* Szyfruje komunikaty wychodzące (jeśli jest skonfigurowane)
* Kompresuje wiadomość hello (jeśli jest skonfigurowane)

## <a name="try-this-sample"></a>Spróbuj w tym przykładzie

tootry wdrażanie logiki pełnej funkcjonalności aplikacji oraz przykładowy AS2 scenariusza, zobacz hello [AS2 szablon aplikacji logiki oraz scenariusz](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/as2/). 

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

