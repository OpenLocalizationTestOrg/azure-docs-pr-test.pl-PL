---
title: "komunikaty EDIFACT aaaEncode — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie kodu XML za pomocą kodera wiadomości EDIFACT w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Kodowanie wiadomości EDIFACT dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw

Łącznik wiadomość hello kodowania EDIFACT zweryfikować EDI i właściwości specyficzne dla partnera, generowanie dokumentu XML dla każdego zestawu transakcji, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.
toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure. Musi mieć łącznika integracji konta toouse hello EDIFACT kodowania komunikatu. 
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji
* [Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji

## <a name="encode-edifact-messages"></a>Kodowanie EDIFACT wiadomości

1. [Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Hello EDIFACT kodowania komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania. W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.

3.  W polu wyszukiwania hello wprowadź "EDIFACT" jako filtr. Wybierz opcję **kodowania komunikatu EDIFACT przez Nazwa umowy** lub **Koduj tooEDIFACT komunikatu przez tożsamości**.
   
    ![Wyszukiwanie EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia. Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.

    ![Tworzenie połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Właściwości oznaczone gwiazdką są wymagane.

    | Właściwość | Szczegóły |
    | --- | --- |
    | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
    | Konta integracji * |Wprowadź nazwę konta integracji. Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure. |

5.  Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis. Wybierz toofinish Tworzenie połączenia **Utwórz**.

    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    Utworzono połączenie.

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Kodowanie komunikatu EDIFACT przez Nazwa umowy

Jeśli wybrano opcję tooencode EDIFACT wiadomości przez nazwę umowy, otwórz hello **umowy nazwa EDIFACT** listy, wprowadź lub wybierz nazwę umowy EDIFACT. Wprowadź tooencode wiadomości XML hello.

![Wprowadź nazwę umowy EDIFACT i tooencode wiadomości XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Kodowanie komunikatu EDIFACT przez tożsamości

Jeśli wybierzesz tooencode EDIFACT wiadomości przez tożsamości, wprowadź identyfikator nadawcy hello, Kwalifikator nadawcy identyfikator odbiornika i odbiornika kwalifikator zgodnie z konfiguracją umowy EDIFACT. Wybierz hello tooencode wiadomości XML.

![Podaj tożsamości dla nadawcy i odbiorcy, wybierz tooencode wiadomości XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Szczegóły EDIFACT kodowania

Łącznik kodowania EDIFACT Hello wykonuje te zadania: 

* Rozwiąż umowy hello przez dopasowanie kwalifikator nadawcy hello & Identyfikator kwalifikator odbiornik i identyfikator
* Serializuje hello EDI wymiany danych, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w hello wymiany.
* Stosuje zestaw transakcji nagłówka i przyczepy segmentów
* Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany
* Zastępuje separatorów hello ładunek danych
* Sprawdza poprawność właściwości specyficzne dla partnerów i EDI
  * Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello.
  * EDI Weryfikacja w przypadku elementów dane zestawu transakcji.
  * Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji
* Generuje dokument XML dla każdego zestawu transakcji.
* Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).
  * Jako potwierdzenie technicznych wiadomości powitania CONTRL wskazuje otrzymania wymiany.
  * Jako funkcjonalności potwierdzenie wiadomości powitania CONTRL wskazuje akceptacji lub odrzucenia wymiany hello odebrane, grupy lub wiadomości z listą błędów lub nieobsługiwanych funkcji

## <a name="view-swagger-file"></a>Plik struktury Swagger widoku
Szczegóły programu Swagger hello tooview hello EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

