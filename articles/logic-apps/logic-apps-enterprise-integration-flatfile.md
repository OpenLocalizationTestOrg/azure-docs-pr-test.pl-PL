---
title: "aaaEncode lub dekodowania plików prostych w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak toouse hello pliku plik encoder lub dekodera w hello pakiet integracyjny dla przedsiębiorstw w aplikacjach logiki"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Omówienie integracji przedsiębiorstwa z plików prostych

Możesz tooencode XML zawartości przed wysłaniem partnerom biznesowym tooa w scenariuszu między firmami (B2B). W aplikacji logiki można użyć pliku prostego powitania to kodowanie toodo łącznika. Witaj aplikacji logiki, który utworzono można uzyskać jego XML zawartości z różnych źródeł, łącznie z wyzwalacz żądania HTTP z innej aplikacji lub nawet z hello wiele [łączniki](../connectors/apis-list.md). Aby uzyskać więcej informacji na temat aplikacji logiki, zobacz hello [dokumentacji aplikacje logiki](logic-apps-what-are-logic-apps.md "Dowiedz się więcej o aplikacjach Logic apps").  

## <a name="create-hello-flat-file-encoding-connector"></a>Tworzenie łącznika kodowania pliku prostego powitania
Wykonaj tooadd te kroki plik prosty kodowanie aplikacji logiki tooyour łącznika.

1. Tworzenie aplikacji logiki i [link jej konta integracji tooyour](logic-apps-enterprise-integration-accounts.md "Dowiedz się toolink aplikacji logiki integracji konta tooa"). To konto zawiera schemat hello użyje hello tooencode danych XML.  
2. Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** aplikacji logiki tooyour wyzwalacza.  
   ![Zrzut ekranu przedstawiający tooselect wyzwalacza](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Dodawanie pliku prostego powitania kodowanie akcji, w następujący sposób:
   
    a. Wybierz hello **plus** logowania.
   
    b. Wybierz hello **Dodaj akcję** łącza (pojawia się po wybraniu znak plus hello).
   
    c. W polu wyszukiwania hello wpisz *płaskiej* toofilter hello wszystkie akcje toohello, jednego, które mają toouse.
   
    d. Wybierz hello **płaskiej kodowanie pliku** opcji z listy hello.   
   ![Opcja Zrzut ekranu z płaskim kodowanie pliku](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Na powitania **płaskiej kodowanie pliku** okno dialogowe, wybierz opcję hello **zawartości** pola tekstowego.  
   ![Zrzut ekranu zawartości pola tekstowego](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Wybierz znacznik treści hello hello zawartości, które mają tooencode. tag treści Hello są powielane hello zawartości pola.     
   ![Zrzut ekranu przedstawiający znacznik treści](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Wybierz hello **nazwy schematu** pole listy i wybierz polecenie schematu hello ma toouse tooencode hello wejściowych zawartości.    
   ![Zrzut ekranu Nazwa schematu pola listy](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Zapisz swoją pracę.   
   ![Zrzut ekranu zapisać ikony](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

W tym momencie po zakończeniu konfigurowania łącznika kodowania z pliku prostego. W przypadku aplikacji rzeczywistych można toostore hello zakodowanych danych w aplikacji — biznesowych, takich jak Salesforce. Lub możesz wysłać tego tooa dane zakodowane partnera handlowego. Możesz łatwo dodać akcję toosend hello dane wyjściowe hello kodowanie tooSalesforce akcji lub partnerem handlowym tooyour, za pomocą jednego z hello innych łączników, pod warunkiem.

Teraz możesz przetestować Twojego łącznika wybierając punkt końcowy HTTP toohello żądania, a tym hello zawartości XML w treści hello hello żądania.  

## <a name="create-hello-flat-file-decoding-connector"></a>Tworzenie pliku prostego powitania dekodowania łącznika

> [!NOTE]
> toocomplete tych kroków, należy toohave plik schematu już przekazany do konta integracji.

1. Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** aplikacji logiki tooyour wyzwalacza.  
   ![Zrzut ekranu przedstawiający tooselect wyzwalacza](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Dodawanie pliku prostego powitania dekodowania akcji, w następujący sposób:
   
    a. Wybierz hello **plus** logowania.
   
    b. Wybierz hello **Dodaj akcję** łącza (pojawia się po wybraniu znak plus hello).
   
    c. W polu wyszukiwania hello wpisz *płaskiej* toofilter hello wszystkie akcje toohello, jednego, które mają toouse.
   
    d. Wybierz hello **płaskiej dekodowania pliku** opcji z listy hello.   
   ![Zrzut ekranu z płaskim pliku dekodowania opcji](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Wybierz hello **zawartości** formantu. To tworzy listę zawartości hello z wcześniejszych krokach, których można użyć jako hello toodecode zawartości. Zwróć uwagę, że hello *treści* z hello przychodzące żądanie HTTP jest dostępne toobe używany jako hello toodecode zawartości. Możesz też wprowadzić hello toodecode zawartości bezpośrednio do hello **zawartości** formantu.     
4. Wybierz hello *treści* tagu. Powiadomienie hello treści tag znajduje się teraz w hello **zawartości** formantu.
5. Wybierz nazwę hello hello schematu, które mają toouse toodecode hello zawartości. Witaj Poniższy zrzut ekranu pokazuje, że *OrderFile* jest nazwa wybranego schematu hello. Ta nazwa schematu była wcześniej przekazany pod uwagę integracji hello.
   
   ![Zrzut ekranu z płaskim pliku dekodowania — okno dialogowe](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Zapisz swoją pracę.  
   ![Zrzut ekranu zapisać ikony](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

W tym momencie po zakończeniu konfigurowania pliku płaskiej dekodowania łącznika. W przypadku aplikacji rzeczywistych można toostore hello zdekodować danych w aplikacji biznesowych — takie jak Salesforce. Możesz łatwo dodać akcję toosend hello dane wyjściowe hello dekodowania tooSalesforce akcji.

Teraz możesz przetestować Twojego łącznika przez punkt końcowy HTTP toohello żądania i tym hello zawartości XML mają toodecode w treści hello hello żądania.  

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw").  

