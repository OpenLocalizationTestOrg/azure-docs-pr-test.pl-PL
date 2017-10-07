---
title: aaaConnect tooan lokalnego systemu SAP w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft
description: "Połącz z przepływu pracy aplikacji logiki za pośrednictwem bramy danych lokalne powitania tooan lokalnego systemu SAP"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Połącz z aplikacji logiki z łącznikiem SAP hello tooan lokalnego systemu SAP 

Brama danych lokalne powitania pozwala toomanage danych i bezpieczny dostęp do zasobów, które znajdują się na obszarze. W tym temacie przedstawiono, jak można łączyć logic apps tooan lokalnego SAP systemu. W tym przykładzie aplikację logiki żądań IDOC za pośrednictwem protokołu HTTP i wysyła odpowiedź hello ponownie.    

> [!NOTE]
> Bieżące ograniczenia: 
> - Jeśli wszystkie kroki wymagane do odpowiedzi hello nie zakończy się w obrębie hello limitu czasu aplikację logiki [limit czasu żądania](./logic-apps-limits-and-config.md). W tym scenariuszu może pobrać zablokowane żądania. 
> - selektor plików Hello nie są wyświetlane wszystkie dostępne pola hello. W tym scenariuszu można ręcznie dodać ścieżki.

## <a name="prerequisites"></a>Wymagania wstępne

- Instalowanie i konfigurowanie hello najnowszych [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127) wersji 1.15.6150.1 lub nowszej. [Jak tooconnect toohello lokalną bramę danych w aplikacji logiki](http://aka.ms/logicapps-gateway) list hello kroki. Brama Hello musi zostać zainstalowana na maszynie lokalnej, zanim przejdziesz dalej.

- Pobierz i zainstaluj hello najnowsze SAP biblioteki klienta na powitania sam komputera, w którym zainstalowano bramę danych hello. Użyj dowolnej z hello następujące wersje programu SAP: 
    - Serwerem SAP
        - Dowolnego serwera SAP hello tej obsługi łącznika .NET (NCo) 3.0
 
    - Klient programu SAP
        - Łącznik .NET programu SAP (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Dodaj wyzwalacze i akcje podłączania tooyour systemu SAP

Łącznik programu SAP Hello ma działania, ale nie wyzwalaczy. Tak mamy toouse inny wyzwalacz na początku hello hello przepływu pracy. 

1. Dodaj hello wyzwalacza żądanie/odpowiedź, a następnie wybierz **nowy krok**.

2. Wybierz **Dodaj akcję**, a następnie wybierz łącznik SAP hello wpisując `SAP` w polu wyszukiwania hello:    

     ![Wybierz serwer aplikacji SAP lub serwer komunikatów SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. Wybierz [ **serwera aplikacji SAP** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) lub [ **serwer komunikatów SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), oparte na ustawieniach SAP. Jeśli nie masz istniejące połączenie, to zostanie wyświetlony monit o toocreate, jeden.

   1. Wybierz **Połącz za pośrednictwem bramy danych lokalnych**, a następnie wprowadź szczegóły hello systemu SAP:   

       ![Dodaj tooSAP ciąg połączenia](media/logic-apps-using-sap-connector/picture2.png)  

   2. W obszarze **bramy**, wybierz istniejącą bramę lub tooinstall nową bramę, wybierz **zainstalować bramę**.

        ![Instalowanie nowej bramy](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Po wprowadzeniu wszystkich szczegółów hello wybierz **Utwórz**. 
   Logic Apps konfiguruje i testuje połączenie hello, upewniając się, czy hello połączenie działa poprawnie.

4. Wprowadź nazwę dla połączenia SAP.

5. obecnie dostępne są różne opcje SAP Hello. toofind IDOC kategorii, wybierz z listy hello. Lub ręcznie wpisać ścieżkę hello i odpowiedź wybierz hello HTTP w hello **treści** pola:

     ![Akcja SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Dodaj akcję hello tworzenia **odpowiedzi HTTP**. komunikat odpowiedzi Hello powinien być z hello SAP w danych wyjściowych.

7. Zapisz aplikację logiki. Przetestować, wysyłając IDOC za pomocą adresu URL wyzwalacza hello HTTP. Po hello wysłania IDOC poczekaj, aż hello odpowiedzi z aplikacji logiki hello:   

     > [!TIP]
     > Sprawdź, jak za[Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Teraz, gdy łącznik SAP hello jest dodawany tooyour aplikacji logiki, rozpocząć eksplorowanie inne funkcje:

- BAPI
- RFC

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak toovalidate, przekształcanie i inne funkcje BizTalk przypominającej hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Połącz dane lokalne tooon](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki
