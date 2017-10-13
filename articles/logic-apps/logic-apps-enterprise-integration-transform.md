---
title: "Konwertowanie danych XML przy użyciu transformacji - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz transformacje lub mapps do konwersji danych XML między formatami w aplikacjach logiki przy użyciu zestawu SDK integracji przedsiębiorstwa"
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
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Integracja przedsiębiorstwa z transformacji XML
## <a name="overview"></a>Omówienie
Łącznik przekształcenia integracji przedsiębiorstwa konwertuje dane z jednego formatu do innego formatu. Przykładowo może istnieć wiadomości przychodzącej, która zawiera bieżącą datę w formacie YearMonthDay. Transformacja służy do ponownego formatowania daty w formacie MonthDayYear.

## <a name="what-does-a-transform-do"></a>Do czego służy transformacji?
Przekształcanie, który jest także znana jako mapy, składa się z schematu XML źródła (dane wejściowe) i schematu XML docelowego (dane wyjściowe). Różne funkcje wbudowane można użyć, aby manipulować i kontroli danych, tym działań na ciągach, warunkowego przypisania, wyrażeniach arytmetycznych elementy formatujące czasu daty, a nawet zapętlenia konstrukcje.

## <a name="how-to-create-a-transform"></a>Jak utworzyć transformację?
Przekształcanie/map można utworzyć za pomocą programu Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas). Po zakończeniu tworzenia i testowania transformacji możesz przekazać do konta integracji transformacji. 

## <a name="how-to-use-a-transform"></a>Jak używać przekształcania
Po wysłaniu przekształcenie/map na koncie integracji można służy do tworzenia aplikacji logiki. Aplikację logiki działa z przekształcenia po każdym wyzwoleniu aplikacji logiki (i Brak zawartości wejściowej, które muszą zostać przekształcone).

**Poniżej przedstawiono kroki, aby użyć transformacji**:

### <a name="prerequisites"></a>Wymagania wstępne

* Tworzenie konta usługi integracji i Dodaj mapę do niej  

Teraz, że zostały wykonane szczególną uwagę wymagania wstępne, jest czas, aby utworzyć aplikację logiki:  

1. Tworzenie aplikacji logiki i [połączyć go z kontem integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się połączyć konto integracji aplikacji logiki") zawierający mapy.
2. Dodaj **żądania** do aplikacji logiki wyzwalacza  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Dodaj **transformacji XML** akcji, wybierając najpierw **Dodaj akcję**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Wprowadź słowa *przekształcenie* w polu wyszukiwania, aby filtrować wszystkie akcje do tego, który ma być używany  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Wybierz **transformacji XML** akcji   
6. Dodanie pliku XML **zawartości** który transformacji. Można używać danych XML pojawi się w żądaniu HTTP jako **zawartości**. W tym przykładzie wybierz treści żądania HTTP, która wyzwoliła aplikacji logiki.
7. Wybierz nazwę **mapy** chcesz używać do wykonywania transformacji. Mapa musi być już na koncie integracji. W poprzednim kroku już udzielił Ci dostęp do aplikacji logiki do swojego konta integracji zawierającego mapy.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Zapisz swoją pracę  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

W tym momencie po zakończeniu konfigurowania mapy. W przypadku aplikacji rzeczywistych można przechowywać przekształcone dane w aplikacji biznesowych, takich jak SalesForce. Możesz z łatwością jako akcja wysyłane dane wyjściowe przekształcenia Salesforce. 

Teraz możesz przetestować z transformacji, wysyłając żądania do punktu końcowego HTTP.  

## <a name="features-and-use-cases"></a>Funkcje i przypadki użycia
* Transformacja utworzone na mapie może być prosty, takich jak kopiowanie nazwy i adresu z jednego dokumentu do innego. Alternatywnie można tworzyć bardziej złożone przekształcenia przy użyciu operacji poza pole mapy.  
* Wiele operacji mapy lub funkcje są łatwo dostępne, w tym ciągów, dat funkcje związane z czasem i tak dalej.  
* Możesz to zrobić kopię danych bezpośrednio między schematów. W mapowania dołączony do zestawu SDK jest tak proste, jak rysowania linii łączącej elementy w schemacie źródła z ich odpowiedniki w schemacie docelowego.  
* Podczas tworzenia mapy, możesz wyświetlić graficzną reprezentację mapa, która zawiera wszystkie relacje i tworzysz łącza.
* Funkcja testu mapy do dodania przykładowy komunikat XML. Pojedynczym kliknięciem można przetestować mapy, który został utworzony, a Zobacz wygenerowanych danych wyjściowych.  
* Przekazywanie istniejącej mapy  
* Obsługuje XML format.

## <a name="learn-more"></a>Dowiedz się więcej
* [Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [Dowiedz się więcej o mapy](../logic-apps/logic-apps-enterprise-integration-maps.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")  

