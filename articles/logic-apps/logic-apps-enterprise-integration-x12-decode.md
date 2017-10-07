---
title: "komunikaty aaaDecode X12 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z dekodera wiadomość hello X12 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Dekodowanie X12 komunikatów dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw

Łącznik wiadomość hello dekodowania X12 można zweryfikować koperty hello przed umowy z partnerem handlowym, sprawdzanie poprawności EDI i właściwości specyficzne dla partnera, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzenia dla przetworzonych transakcji. toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznik wiadomość hello dekodowania X12 integracji konta toouse.
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji

## <a name="decode-x12-messages"></a>Dekodowanie X12 wiadomości

1. [Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Hello dekodowania X12 komunikat łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3.  W polu wyszukiwania hello wprowadź "x12" filtru. Wybierz **X12-dekodowania X12 komunikat**.
   
    ![Wyszukaj "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect. 

    ![Podaj szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

5.  Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis. Wybierz toofinish Tworzenie połączenia **Utwórz**.
   
    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz toodecode komunikat pliku prostego powitania X12.

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Na przykład:

    ![Wybierz X12 płaskim komunikat pliku dekodowania](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>X12 dekodowania szczegóły

Łącznik dekodowania Hello X12 wykonuje te zadania:

* Weryfikuje koperty hello przed handlowymi umowy z partnerem
* Sprawdza poprawność właściwości specyficzne dla partnerów i EDI
  * Sprawdzanie poprawności strukturalnych EDI i rozszerzony schemat sprawdzania poprawności
  * Sprawdzanie poprawności hello struktury hello koperty wymiany.
  * Sprawdzanie poprawności schematu koperty hello schematem hello kontroli.
  * Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello.
  * EDI weryfikacji w przypadku elementów dane zestawu transakcji 
* Sprawdza, czy hello wymiany, grupy i transakcji zestaw numerów kontroli nie są duplikatami
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
* Generuje potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).
  * Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka. Hello techniczne potwierdzenia raporty hello stan przetwarzania hello wymiany nagłówka i przyczepy przez hello adres odbiorcy.
  * Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści. Witaj potwierdzenia funkcjonalności raporty każdy błąd podczas przetwarzania hello otrzymał dokument

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/x12/). 

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

