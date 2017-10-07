---
title: "komunikaty EDIFACT aaaDecode — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z dekodera komunikat EDIFACT hello w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Dekodowanie EDIFACT wiadomości dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw

Łącznik wiadomość hello dekodowania EDIFACT można zweryfikować właściwości specyficzne dla partnerów i EDI, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzeń przetworzonych transakcji. toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznika integracji konta toouse hello EDIFACT dekodowanie komunikatu. 
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji

## <a name="decode-edifact-messages"></a>Dekodowanie EDIFACT wiadomości

1. [Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Hello EDIFACT zdekodować komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3. W polu wyszukiwania hello wprowadź "EDIFACT" jako filtr. Wybierz **zdekodować komunikatu EDIFACT**.
   
    ![Wyszukiwanie EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.
   
    ![Tworzenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

4. Po zakończeniu tworzenia połączenia toofinish wybierz **Utwórz**. Szczegóły połączenia powinien wyglądać podobnie przykład toothis:

    ![Szczegóły konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz hello EDIFACT pliku prostego komunikatu toodecode.

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Na przykład:

    ![Wybierz EDIFACT pliku prostego komunikatu dekodowania](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Szczegóły dekodera EDIFACT

Łącznik dekodowania EDIFACT Hello wykonuje te zadania: 

* Weryfikuje koperty hello przed handlowymi umowy z partnerem.
* Rozpoznaje umowy hello przez dopasowanie hello kwalifikator nadawcy i identyfikator oraz kwalifikator odbiornik i identyfikator.
* Dzieli wymiany na wiele transakcji, gdy wymiany hello ma więcej niż jednej transakcji na podstawie umowy hello odbierać konfigurację ustawień.
* Rozkłada hello wymiany.
* Weryfikuje EDI i właściwości specyficzne dla partnera, w tym:
  * Sprawdzanie poprawności hello wymiany koperty struktury
  * Sprawdzanie poprawności schematu koperty hello schematem kontroli hello
  * Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello
  * EDI weryfikacji w przypadku elementów dane zestawu transakcji
* Sprawdza, czy hello wymiany, grupy i transakcji zestaw numerów kontroli nie są duplikatami (jeśli jest skonfigurowane) 
  * Sprawdza hello wymiany kontroli numer przed wymianę wcześniej odebrane. 
  * Sprawdza hello grupy kontroli numer względem innych numery kontroli grupy w hello wymiany. 
  * Sprawdza, czy transakcja hello Ustaw numer kontroli względem innych numery kontroli zestawu transakcji w tej grupie.
* Dzieli wymiany hello w zestawy transakcji lub zachowuje hello całego wymiany:
  * Wymiany podziału jako zestawy transakcji - zawiesić zestawy transakcji o błędzie: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji. 
  Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.
  * Podziel wymiany jako zestawy transakcji - zawiesić wymiany na błąd: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji. 
  Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.
  * Zachowaj wymiany — zawiesza zestawy transakcji na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany. 
  Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.
  * Zachowaj wymiany — zawiesza wymiany na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany. 
  Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.
* Generuje Technical (kontrola) i/lub funkcjonalności potwierdzenia (jeśli jest skonfigurowane).
  * Techniczne potwierdzeń lub hello potwierdzenia CONTRL wyświetla wyniki hello syntaktycznych sprawdzenia hello zakończenie Odebrano wymiany.
  * Potwierdzenie funkcjonalności potwierdza zaakceptować lub odrzucić odebrane wymiany lub grupy

## <a name="view-swagger-file"></a>Plik struktury Swagger widoku
Szczegóły programu Swagger hello tooview hello EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

