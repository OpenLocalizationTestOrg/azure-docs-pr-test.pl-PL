---
title: "komunikaty aaaEncode X12 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i przekonwertować kodowany w formacie XML komunikaty z X12 komunikatu kodera w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Kodowanie X12 komunikatów dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw

Łącznik wiadomość hello Koduj X12 zweryfikować EDI i właściwości specyficzne dla partnera, przekonwertować wiadomości w formacie XML na EDI zestawów transakcji w hello wymiany, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.
toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznik wiadomość hello Koduj X12 integracji konta toouse.
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji

## <a name="encode-x12-messages"></a>Kodowanie X12 wiadomości

1. [Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Hello Koduj X12 komunikat łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3.  W polu wyszukiwania hello wprowadź "x12" filtru. Wybierz opcję **X12-kodowania komunikatu tooX12 według nazwy umowy** lub **X12-kodowania komunikatu tooX12 przez tożsamości**.
   
    ![Wyszukaj "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect. 
   
    ![Integracja połączenia konta](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

5.  Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis. Wybierz toofinish Tworzenie połączenia **Utwórz**.

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    Utworzono połączenie.

    ![Szczegóły połączenia konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Kodowanie X12 wiadomości przez Nazwa umowy

Jeśli została wybrana opcja tooencode X12 wiadomości przez nazwę umowy, otwórz hello **nazwa X12 umowy** listy, wpisz lub wybierz Twoje istniejące X12 umowy. Wprowadź tooencode wiadomości XML hello.

![Wprowadź X12 umowy, nazwę i XML komunikatu tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Kodowanie X12 wiadomości przez tożsamości

Wybranie tooencode X12 wiadomości przez tożsamości, wprowadź identyfikator nadawcy hello, Kwalifikator nadawcy, odbiorcy identyfikator i kwalifikator odbiornika zgodnie z konfiguracją sieci X12 umowy. Wybierz hello tooencode wiadomości XML.
   
![Podaj tożsamości dla nadawcy i odbiorcy, wybierz tooencode wiadomości XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 kodowania szczegóły

Łącznik Koduj Hello X12 wykonuje te zadania:

* Rozwiązanie umowy przez nadawcę i odbiorcę właściwości kontekstu dopasowywania.
* Serializuje hello EDI wymiany danych, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w hello wymiany.
* Stosuje zestaw transakcji nagłówka i przyczepy segmentów
* Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany
* Zastępuje separatorów hello ładunek danych
* Sprawdza poprawność właściwości specyficzne dla partnerów i EDI
  * Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello przed wiadomość hello schematu
  * EDI Weryfikacja w przypadku elementów dane zestawu transakcji.
  * Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji
* Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).
  * Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka. Stan hello raportów technicznych potwierdzenia Hello hello przetwarzania nagłówka wymiany i przyczepy przez hello adres odbiorcy
  * Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści. Witaj potwierdzenia funkcjonalności raporty każdy błąd podczas przetwarzania hello otrzymał dokument

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/x12/). 

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

