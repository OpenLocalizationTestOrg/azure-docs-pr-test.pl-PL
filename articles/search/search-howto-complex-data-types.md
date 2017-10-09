---
title: "aaaHow toomodel złożone typy danych w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Zagnieżdżone lub mogą być modelowane struktury hierarchicznej danych do indeksu usługi Azure Search przy użyciu spłaszczoną wierszy i typ danych kolekcji."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Jak typy danych złożonych toomodel w usłudze Azure Search
Zewnętrznych zestawów danych używane toopopulate indeksu usługi Azure Search czasami obejmują hierarchiczna lub zagnieżdżony struktur podrzędnych, które nie podzielić się starannie na tabelarycznych zestawu wierszy. Przykłady takich konstrukcji może obejmują wiele lokalizacji i numerów telefonów dla jednego klienta, wiele kolorów i rozmiary dla jednej jednostki SKU wielu autorów jednej książce i tak dalej. Modelowanie warunki, można napotkać tych struktur określonego tooas *złożone typy danych*, *złożone typy danych*, *złożone typy danych*, lub *agregacji typy danych*, tooname w kilku.

Złożone typy danych nie są natywnie obsługiwane w usłudze Azure Search, ale sprawdzonych obejście zawiera dwuetapowy proces spłaszczanie hello struktury, a następnie użyć **kolekcji** tooreconstitute hello wewnętrznej struktury typu danych. Następujące techniki hello opisane w tym artykule umożliwia toobe zawartości hello przeszukane aspektowej, filtrować i sortować.

## <a name="example-of-a-complex-data-structure"></a>Przykład struktury danych złożonych
Zazwyczaj w danych hello znajduje się jako zestaw dokumentów JSON i XML lub jako elementy w magazynie NoSQL, takie jak bazy danych Azure rozwiązania Cosmos. Strukturę Żądanie hello wynika z o wiele elementów podrzędnych wymagające toobe przeszukiwanie i filtrowane.  Jako punkt początkowy dla pokazujący hello obejście wykonaj powitania po dokument JSON, który zawiera zestaw kontaktów, na przykład:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Gdy hello pola o nazwie 'id', 'name' i 'firma' łatwo można mapować jeden do jednego jako pola w indeksie usługi Azure Search, hello "w lokalizacji" pole zawiera tablicę lokalizacje mających zarówno zestaw identyfikatorów lokalizacji, a także opisy lokalizacji. Biorąc pod uwagę, że usługi Azure Search nie ma typu danych, która obsługuje tę funkcję, toomodel inny sposób to potrzebne w usłudze Azure Search. 

> [!NOTE]
> Ta technika jest również przez Kirk Evans opisane w artykule w blogu [indeksowania usługi DocumentDB z usługi Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), który wskazuje technika o nazwie "spłaszczania hello dane", według których należy pole o nazwie `locationsID` i `locationsDescription` są takie [kolekcje](https://msdn.microsoft.com/library/azure/dn798938.aspx) (lub tablicą ciągów).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Część 1: Spłaszczanie hello tablicy do poszczególnych pól
toocreate indeksu usługi Azure Search, uwzględniający ten zestaw danych, Utwórz poszczególnych pól dla zagnieżdżonej konstrukcja hello: `locationsID` i `locationsDescription` z typem danych [kolekcje](https://msdn.microsoft.com/library/azure/dn798938.aspx) (lub tablicą ciągów). W tych polach czy indeksu hello wartości "1" i "2" do hello `locationsID` pole wartości Jan Kowalski i Witaj, "3" i "4" w hello `locationsID` dla Jen Campbell pole.  

Dane w usłudze Azure Search będzie wyglądać następująco: 

![Przykładowe dane 2 wierszy](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Część 2: Dodaj pole kolekcji w definicji indeksu hello
W schemacie indeksu hello definicje pól hello może wyglądać podobny przykład toothis.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Sprawdź poprawność zachowań wyszukiwania i opcjonalnie rozszerzono hello indeksu
Zakładając, że indeks utworzony hello i hello załadować dane, możesz sprawdzić hello wykonywania zapytania wyszukiwania tooverify rozwiązanie przed hello zestawu danych. Każdy **kolekcji** pole powinno być **wyszukiwanie**, **filtrowanie** i **aspektów**. Powinny być możliwe toorun kwerend, takich jak:

* Znajdź wszystkie osoby, które działają na powitania "Adventureworks centrali".
* Pobierz liczbę hello liczba osób pracujących w biurze głównej.  
* Hello osób, które działają w biurze głównej pokazują, jakie inne biura one działać wraz z liczbą osób hello w każdej lokalizacji.  

Gdy ta metoda znajduje się od siebie sposób można toodo wyszukiwania, które łączy zarówno hello identyfikator lokalizacji, a także opis lokalizacji hello. Na przykład:

* Znajdź wszystkie osoby, które mają Office głównej i ma identyfikator lokalizacji 4.  

Jeżeli pamiętasz hello oryginalnej zawartości po zapoznaniu się następująco:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Jednak teraz, możemy zostały rozdzielone hello danych na różnych pól, firma Microsoft nie ma możliwości wiedząc, jeśli hello sieć domowa dla Jen Campbell odnosi się zbyt`locationsID 3` lub `locationsID 4`.  

toohandle w tym przypadku definiowania innego pola w indeksie hello, który łączy wszystkie dane hello w jednej kolekcji.  W naszym przykładzie zostanie nazywamy to pole `locationsCombined` i będzie oddzielić hello zawartości za pomocą `||` Chociaż można wybrać żadnych separatora, które należy wziąć pod uwagę byłoby unikatowy zestaw znaków dla zawartości. Na przykład: 

![Przykładowe dane 2 wierszy z separatorem](./media/search-howto-complex-data-types/sample-data-2.png)

Za pomocą tej `locationsCombined` pola, firma Microsoft może teraz obsłużyć więcej zapytania, takie jak:

* Pokaż liczba osób pracujących w "Głównej urzędzie" z lokalizacją Id "4".  
* Wyszukaj osoby, które działają w biurze głównej z lokalizacją Id "4". 

## <a name="limitations"></a>Ograniczenia
Ta metoda jest przydatna do kilka scenariuszy, ale nie ma on zastosowania w każdym przypadku.  Na przykład:

1. Jeśli nie masz statycznego zestawu pól w Twojej złożonym typie danych i nie było żadnych toomap sposób wszystkich możliwych hello typy tooa jedno pole. 
2. Aktualizowanie hello zagnieżdżone obiekty wymaga niektórych toodetermine dodatkowej pracy dokładnie niezbędne toobe zaktualizowane w hello indeksu usługi Azure Search

## <a name="sample-code"></a>Przykładowy kod
Możesz wyświetlić przykład od tooindex złożone danych JSON konfiguracji do usługi Azure Search i wykonywać wiele zapytań za pośrednictwem tego elementu dataset w tej [repozytorium GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Następny krok
[Głos dla macierzystą obsługę złożonych typach danych](https://feedback.azure.com/forums/263029-azure-search) na hello Azure Search UserVoice strony i wprowadzania dodatkowych czy mamy tooconsider dotyczące implementacji funkcji. Można również dotrzeć toome bezpośrednio w serwisie Twitter na @liamca.

