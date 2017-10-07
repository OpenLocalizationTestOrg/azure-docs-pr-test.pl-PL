---
title: "rozwiązania aaaCreate B2B - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Odbieranie danych w aplikacjach logiki za pomocą funkcji hello B2B w hello pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Odbieranie danych w aplikacjach logiki z funkcjami B2B hello w hello pakiet integracyjny dla przedsiębiorstw

Po utworzeniu konta integracji z partnerami i umów są gotowe toocreate biznesowego przepływu pracy toobusiness (B2B) dla aplikacji logiki z hello [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

Witaj toouse AS2 i X12 akcje, muszą mieć konta integracji przedsiębiorstwa. Dowiedz się [jak toocreate integracji przedsiębiorstwa konta](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Tworzenie aplikacji logiki z łączniki B2B

Wykonaj te kroki toocreate B2B logikę aplikacji, która używa hello AS2 i X12 akcje tooreceive danych z partnerem handlowym:

1. Tworzenie aplikacji logiki, następnie [połączone konto integracji aplikacji tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** aplikacji logiki tooyour wyzwalacza.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. Witaj tooadd **dekodowania AS2** akcji, wybierz opcję **Dodaj akcję**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **as2** hello pola wyszukiwania.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Wybierz hello **AS2 - AS2 zdekodować komunikatu** akcji.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Dodaj hello **treści** , które mają toouse jako dane wejściowe. W tym przykładzie wybierz hello treści żądania HTTP hello czy wyzwalaczy hello aplikacji logiki. Lub wprowadź wyrażenie danych wejściowych hello nagłówków hello **nagłówki** pola:

    @triggerOutputs() [nagłówki]

7. Dodaj wymagane hello **nagłówki** dla AS2, który można znaleźć w nagłówkach żądania hello HTTP. W tym przykładzie wybierz hello nagłówków żądania HTTP hello aplikacji logiki hello tego wyzwalacza.

8. Teraz Dodaj hello dekodowania X12 komunikat akcji. Wybierz **Dodaj akcję**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **x12** hello pola wyszukiwania.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Wybierz hello **X12-dekodowania X12 komunikat** akcji.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Teraz należy określić hello wejściowych toothis akcji. Tych danych wejściowych jest hello hello poprzedniej akcji AS2 dane wyjściowe.

    zawartości rzeczywiste wiadomość Hello jest w obiekcie JSON i kodowanie base64, dlatego należy określić wyrażenie jako dane wejściowe hello. 
    Wprowadź powitania po wyrażeniu w hello **X12 PŁASKIM tooDECODE komunikat pliku** pola wejściowego:
    
    @base64ToString(body('Decode_AS2_message')? ["AS2Message"]? ["Content"])

    Teraz dodać kroki toodecode hello X12 danych otrzymanych od partnera handlowego hello i dane wyjściowe elementów w obiekcie JSON. 
    Odebrano toonotify hello partnerów, którzy hello danych, możesz wysłać ponownie odpowiedzi zawierające hello AS2 komunikat dyspozycji powiadomienia (MDN) w celu wykonania akcji odpowiedzi HTTP.

12. Witaj tooadd **odpowiedzi** akcji, wybierz **Dodaj akcję**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **odpowiedzi** hello pola wyszukiwania.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Wybierz hello **odpowiedzi** akcji.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello MDN z danych wyjściowych hello hello **komunikat dekodowania X12** akcji, odpowiedź hello zestaw **treści** wartością tego wyrażenia:

    @base64ToString(body('Decode_AS2_message')? ["OutgoingMdn"]? ["Content"])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Zapisz swoją pracę.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Teraz po zakończeniu konfigurowania aplikacji logiki B2B. W przypadku aplikacji rzeczywistych można toostore hello zdekodować X12 danych w magazynie — biznesowych (LOB) aplikacji lub danych. tooconnect aplikacji biznesowych i użyć tych interfejsów API w aplikacji logiki, można dodać dodatkowe akcje lub zapisać niestandardowych interfejsów API.

## <a name="features-and-use-cases"></a>Funkcje i przypadki użycia

* Hello AS2 i X12 dekodowania i kodowania akcje let wymiany danych między partnerami handlowymi przy użyciu standardowych protokołach branżowych w aplikacjach logiki.
* tooexchange danych z partnerami handlowymi, używając AS2 i X12 z lub bez siebie nawzajem.
* Akcje B2B Hello pomóc łatwe tworzenie partnerów i umów w ramach konta integracji i używać ich w aplikacji logiki.
* Podczas rozszerzania aplikacji logiki z innymi działaniami umożliwia wysyłanie oraz odbieranie danych między innych aplikacji i usług, takich jak SalesForce.

## <a name="learn-more"></a>Dowiedz się więcej
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md)
