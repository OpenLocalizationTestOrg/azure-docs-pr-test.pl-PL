---
title: "komunikaty aaaDecode AS2 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak toouse hello dekodera AS2 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Dekodowanie AS2 wiadomości dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw 

tooestablish bezpieczeństwa i niezawodności podczas przesyłania wiadomości, należy użyć hello AS2 zdekodować komunikatu łącznika. Ten łącznik umożliwia cyfrowe podpisywanie, odszyfrowywania i potwierdzeń za pośrednictwem komunikatu powiadomienia dyspozycji (MDN).

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznika integracji konta toouse hello AS2 dekodowanie komunikatu.
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [Umowy AS2](logic-apps-enterprise-integration-as2.md) jest już zdefiniowany w ramach konta integracji

## <a name="decode-as2-messages"></a>Dekodowanie AS2 wiadomości

1. [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

2. Hello AS2 zdekodować komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3.  W polu wyszukiwania hello wprowadź "AS2" filtru. Wybierz **AS2 - AS2 zdekodować komunikatu**.
   
    ![Wyszukaj "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.
   
    ![Utwórz połączenie integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

5.  Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis. Wybierz toofinish Tworzenie połączenia **Utwórz**.

    ![Szczegóły połączenia integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz **treści** i **nagłówki** z hello żądania danych wyjściowych.
   
    ![utworzone połączenie integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Na przykład:

    ![Wybierz treści i nagłówków z danych wyjściowych żądań](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Szczegóły dekodera AS2

Łącznik AS2 dekodowania Hello wykonuje te zadania: 

* Przetwarza nagłówków AS2/HTTP
* Sprawdza, czy podpis hello (jeśli jest skonfigurowane)
* Odszyfrowuje wiadomości powitania (jeśli jest skonfigurowane)
* Dekompresuje wiadomość hello (jeśli jest skonfigurowane)
* Uzgadnia odebrane MDN z oryginalnej wiadomości wychodzących hello
* Aktualizacje i są powiązane rekordy w bazie danych bez odrzucania hello
* Zapisuje rekordy AS2 raportowania stanu
* zawartość ładunek danych wyjściowych Hello jest kodowany w standardzie base64
* Określa, czy MDN jest wymagana i czy hello MDN powinna być synchroniczne czy asynchroniczne na podstawie konfiguracji umowy AS2
* Generuje MDN synchroniczna lub asynchroniczna, (na podstawie konfiguracji umów)
* Ustawia właściwości i tokenów korelacji hello na powitania MDN

## <a name="try-this-sample"></a>Spróbuj w tym przykładzie

tootry wdrażanie logiki pełnej funkcjonalności aplikacji oraz przykładowy AS2 scenariusza, zobacz hello [AS2 szablon aplikacji logiki oraz scenariusz](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/as2/). 

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md) 

