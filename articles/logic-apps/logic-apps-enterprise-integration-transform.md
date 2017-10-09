---
title: "aaaConvert danych XML przy użyciu transformacji - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz transformacje lub mapps danych XML tooconvert między formatami w aplikacjach logiki przy użyciu hello SDK integracji przedsiębiorstwa"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Integracja przedsiębiorstwa z transformacji XML
## <a name="overview"></a>Omówienie
Łącznik przekształcenia integracji przedsiębiorstwa Hello konwertuje dane z jednego formatu tooanother format. Na przykład masz zawierający bieżącą datę w formacie YearMonthDay hello hello wiadomości przychodzącej. Przekształcanie tooreformat hello Data toobe można użyć w formacie MonthDayYear hello.

## <a name="what-does-a-transform-do"></a>Do czego służy transformacji?
Przekształcenia, która jest także znana jako mapy, składa się z schematu XML źródła (hello danych wejściowych) i schemat XML docelowego (hello dane wyjściowe). Różne funkcje wbudowane toohelp manipulować i kontroli danych hello służy tym działań na ciągach, warunkowego przypisania, wyrażeniach arytmetycznych elementy formatujące czasu Data oraz nawet zapętlenia konstrukcje.

## <a name="how-toocreate-a-transform"></a>Jak toocreate transformacji?
Przekształcanie/map można utworzyć za pomocą programu Visual Studio hello [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas). Po zakończeniu tworzenia i testowania hello przekształcania, możesz przekazać przekształcenia hello na koncie integracji. 

## <a name="how-toouse-a-transform"></a>Jak toouse transformacji
Po przekazaniu hello przekształcenie/map na koncie integracji, można użyć toocreate aplikacji logiki. aplikacji logiki Hello uruchamia przekształcenia użytkownika za każdym razem wyzwoleniu aplikacji logiki hello (i Brak zawartości wejściowej wymagające toobe przekształcone).

**Poniżej przedstawiono toouse kroki hello transformacji**:

### <a name="prerequisites"></a>Wymagania wstępne

* Tworzenie konta usługi integracji i Dodaj tooit mapy  

Teraz, że zostały wykonane szczególną uwagę hello wymagań wstępnych, jest toocreate czasu aplikację logiki:  

1. Tworzenie aplikacji logiki i [link jej konta integracji tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się toolink aplikacji logiki tooa konta integracji") zawierający hello mapy.
2. Dodaj **żądania** aplikacji logiki tooyour wyzwalacza  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Dodaj hello **transformacji XML** akcji, wybierając najpierw **Dodaj akcję**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Wprowadź słowa hello *przekształcenie* w toofilter pole wyszukiwania hello hello wszystkie akcje toohello, jednego, które mają toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Wybierz hello **transformacji XML** akcji   
6. Dodaj hello XML **zawartości** który transformacji. Można używać danych XML pojawi się w żądaniu hello HTTP jako hello **zawartości**. W tym przykładzie wybierz treści hello hello żądania HTTP, która wyzwoliła hello aplikacji logiki.
7. Wybierz hello nazwę hello **mapy** , które mają toouse tooperform hello transformacji. Mapa Hello musi być już na koncie integracji. W poprzednim kroku już udzielił logiki aplikacji dostępu tooyour integracji konta zawierającego mapy.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Zapisz swoją pracę  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

W tym momencie po zakończeniu konfigurowania mapy. W przypadku aplikacji rzeczywistych można toostore hello przekształcone dane w aplikacji biznesowych, takich jak SalesForce. Można łatwo jako akcja toosend hello dane wyjściowe hello przekształcać tooSalesforce. 

Teraz możesz przetestować użytkownika przekształcenia przez punkt końcowy HTTP toohello żądania.  

## <a name="features-and-use-cases"></a>Funkcje i przypadki użycia
* Transformacja Hello utworzone na mapie może być prosty, takich jak kopiowanie nazwy i adresu z jednego tooanother dokumentu. Alternatywnie można tworzyć bardziej złożone przekształcenia przy użyciu operacji poza pole mapy hello.  
* Wiele operacji mapy lub funkcje są łatwo dostępne, w tym ciągów, dat funkcje związane z czasem i tak dalej.  
* Możesz to zrobić kopię danych bezpośrednio między hello schematów. W hello mapowania uwzględnione w hello zestawu SDK jest tak proste, jak rysowania linii łączącego hello elementy w schemacie źródła hello z ich odpowiedniki w schemacie docelowego hello.  
* Podczas tworzenia mapy, możesz wyświetlić graficzną reprezentację hello mapa, która zawiera wszystkie relacje hello i tworzysz łącza.
* Użyj hello mapy testu funkcji tooadd przykładowy komunikat XML. Pojedynczym kliknięciem można przetestować mapy hello utworzone i wyświetlić hello wygenerowane dane wyjściowe.  
* Przekazywanie istniejącej mapy  
* Obsługuje hello XML format.

## <a name="learn-more"></a>Dowiedz się więcej
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [Dowiedz się więcej o mapy](../logic-apps/logic-apps-enterprise-integration-maps.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")  

