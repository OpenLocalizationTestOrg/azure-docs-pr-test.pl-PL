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
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="c7823-103">Jak typy danych złożonych toomodel w usłudze Azure Search</span><span class="sxs-lookup"><span data-stu-id="c7823-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="c7823-104">Zewnętrznych zestawów danych używane toopopulate indeksu usługi Azure Search czasami obejmują hierarchiczna lub zagnieżdżony struktur podrzędnych, które nie podzielić się starannie na tabelarycznych zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="c7823-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="c7823-105">Przykłady takich konstrukcji może obejmują wiele lokalizacji i numerów telefonów dla jednego klienta, wiele kolorów i rozmiary dla jednej jednostki SKU wielu autorów jednej książce i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c7823-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="c7823-106">Modelowanie warunki, można napotkać tych struktur określonego tooas *złożone typy danych*, *złożone typy danych*, *złożone typy danych*, lub *agregacji typy danych*, tooname w kilku.</span><span class="sxs-lookup"><span data-stu-id="c7823-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="c7823-107">Złożone typy danych nie są natywnie obsługiwane w usłudze Azure Search, ale sprawdzonych obejście zawiera dwuetapowy proces spłaszczanie hello struktury, a następnie użyć **kolekcji** tooreconstitute hello wewnętrznej struktury typu danych.</span><span class="sxs-lookup"><span data-stu-id="c7823-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="c7823-108">Następujące techniki hello opisane w tym artykule umożliwia toobe zawartości hello przeszukane aspektowej, filtrować i sortować.</span><span class="sxs-lookup"><span data-stu-id="c7823-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="c7823-109">Przykład struktury danych złożonych</span><span class="sxs-lookup"><span data-stu-id="c7823-109">Example of a complex data structure</span></span>
<span data-ttu-id="c7823-110">Zazwyczaj w danych hello znajduje się jako zestaw dokumentów JSON i XML lub jako elementy w magazynie NoSQL, takie jak bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c7823-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="c7823-111">Strukturę Żądanie hello wynika z o wiele elementów podrzędnych wymagające toobe przeszukiwanie i filtrowane.</span><span class="sxs-lookup"><span data-stu-id="c7823-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="c7823-112">Jako punkt początkowy dla pokazujący hello obejście wykonaj powitania po dokument JSON, który zawiera zestaw kontaktów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="c7823-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="c7823-113">Gdy hello pola o nazwie 'id', 'name' i 'firma' łatwo można mapować jeden do jednego jako pola w indeksie usługi Azure Search, hello "w lokalizacji" pole zawiera tablicę lokalizacje mających zarówno zestaw identyfikatorów lokalizacji, a także opisy lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c7823-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="c7823-114">Biorąc pod uwagę, że usługi Azure Search nie ma typu danych, która obsługuje tę funkcję, toomodel inny sposób to potrzebne w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c7823-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="c7823-115">Ta technika jest również przez Kirk Evans opisane w artykule w blogu [indeksowania usługi DocumentDB z usługi Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), który wskazuje technika o nazwie "spłaszczania hello dane", według których należy pole o nazwie `locationsID` i `locationsDescription` są takie [kolekcje](https://msdn.microsoft.com/library/azure/dn798938.aspx) (lub tablicą ciągów).</span><span class="sxs-lookup"><span data-stu-id="c7823-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="c7823-116">Część 1: Spłaszczanie hello tablicy do poszczególnych pól</span><span class="sxs-lookup"><span data-stu-id="c7823-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="c7823-117">toocreate indeksu usługi Azure Search, uwzględniający ten zestaw danych, Utwórz poszczególnych pól dla zagnieżdżonej konstrukcja hello: `locationsID` i `locationsDescription` z typem danych [kolekcje](https://msdn.microsoft.com/library/azure/dn798938.aspx) (lub tablicą ciągów).</span><span class="sxs-lookup"><span data-stu-id="c7823-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="c7823-118">W tych polach czy indeksu hello wartości "1" i "2" do hello `locationsID` pole wartości Jan Kowalski i Witaj, "3" i "4" w hello `locationsID` dla Jen Campbell pole.</span><span class="sxs-lookup"><span data-stu-id="c7823-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="c7823-119">Dane w usłudze Azure Search będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="c7823-119">Your data within Azure Search would look like this:</span></span> 

![Przykładowe dane 2 wierszy](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="c7823-121">Część 2: Dodaj pole kolekcji w definicji indeksu hello</span><span class="sxs-lookup"><span data-stu-id="c7823-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="c7823-122">W schemacie indeksu hello definicje pól hello może wyglądać podobny przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="c7823-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="c7823-123">Sprawdź poprawność zachowań wyszukiwania i opcjonalnie rozszerzono hello indeksu</span><span class="sxs-lookup"><span data-stu-id="c7823-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="c7823-124">Zakładając, że indeks utworzony hello i hello załadować dane, możesz sprawdzić hello wykonywania zapytania wyszukiwania tooverify rozwiązanie przed hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c7823-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="c7823-125">Każdy **kolekcji** pole powinno być **wyszukiwanie**, **filtrowanie** i **aspektów**.</span><span class="sxs-lookup"><span data-stu-id="c7823-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="c7823-126">Powinny być możliwe toorun kwerend, takich jak:</span><span class="sxs-lookup"><span data-stu-id="c7823-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="c7823-127">Znajdź wszystkie osoby, które działają na powitania "Adventureworks centrali".</span><span class="sxs-lookup"><span data-stu-id="c7823-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="c7823-128">Pobierz liczbę hello liczba osób pracujących w biurze głównej.</span><span class="sxs-lookup"><span data-stu-id="c7823-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="c7823-129">Hello osób, które działają w biurze głównej pokazują, jakie inne biura one działać wraz z liczbą osób hello w każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c7823-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="c7823-130">Gdy ta metoda znajduje się od siebie sposób można toodo wyszukiwania, które łączy zarówno hello identyfikator lokalizacji, a także opis lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="c7823-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="c7823-131">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c7823-131">For example:</span></span>

* <span data-ttu-id="c7823-132">Znajdź wszystkie osoby, które mają Office głównej i ma identyfikator lokalizacji 4.</span><span class="sxs-lookup"><span data-stu-id="c7823-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="c7823-133">Jeżeli pamiętasz hello oryginalnej zawartości po zapoznaniu się następująco:</span><span class="sxs-lookup"><span data-stu-id="c7823-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="c7823-134">Jednak teraz, możemy zostały rozdzielone hello danych na różnych pól, firma Microsoft nie ma możliwości wiedząc, jeśli hello sieć domowa dla Jen Campbell odnosi się zbyt`locationsID 3` lub `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="c7823-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="c7823-135">toohandle w tym przypadku definiowania innego pola w indeksie hello, który łączy wszystkie dane hello w jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c7823-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="c7823-136">W naszym przykładzie zostanie nazywamy to pole `locationsCombined` i będzie oddzielić hello zawartości za pomocą `||` Chociaż można wybrać żadnych separatora, które należy wziąć pod uwagę byłoby unikatowy zestaw znaków dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="c7823-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="c7823-137">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c7823-137">For example:</span></span> 

![Przykładowe dane 2 wierszy z separatorem](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="c7823-139">Za pomocą tej `locationsCombined` pola, firma Microsoft może teraz obsłużyć więcej zapytania, takie jak:</span><span class="sxs-lookup"><span data-stu-id="c7823-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="c7823-140">Pokaż liczba osób pracujących w "Głównej urzędzie" z lokalizacją Id "4".</span><span class="sxs-lookup"><span data-stu-id="c7823-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="c7823-141">Wyszukaj osoby, które działają w biurze głównej z lokalizacją Id "4".</span><span class="sxs-lookup"><span data-stu-id="c7823-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="c7823-142">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="c7823-142">Limitations</span></span>
<span data-ttu-id="c7823-143">Ta metoda jest przydatna do kilka scenariuszy, ale nie ma on zastosowania w każdym przypadku.</span><span class="sxs-lookup"><span data-stu-id="c7823-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="c7823-144">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c7823-144">For example:</span></span>

1. <span data-ttu-id="c7823-145">Jeśli nie masz statycznego zestawu pól w Twojej złożonym typie danych i nie było żadnych toomap sposób wszystkich możliwych hello typy tooa jedno pole.</span><span class="sxs-lookup"><span data-stu-id="c7823-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="c7823-146">Aktualizowanie hello zagnieżdżone obiekty wymaga niektórych toodetermine dodatkowej pracy dokładnie niezbędne toobe zaktualizowane w hello indeksu usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="c7823-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="c7823-147">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="c7823-147">Sample code</span></span>
<span data-ttu-id="c7823-148">Możesz wyświetlić przykład od tooindex złożone danych JSON konfiguracji do usługi Azure Search i wykonywać wiele zapytań za pośrednictwem tego elementu dataset w tej [repozytorium GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="c7823-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="c7823-149">Następny krok</span><span class="sxs-lookup"><span data-stu-id="c7823-149">Next step</span></span>
<span data-ttu-id="c7823-150">[Głos dla macierzystą obsługę złożonych typach danych](https://feedback.azure.com/forums/263029-azure-search) na hello Azure Search UserVoice strony i wprowadzania dodatkowych czy mamy tooconsider dotyczące implementacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="c7823-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="c7823-151">Można również dotrzeć toome bezpośrednio w serwisie Twitter na @liamca.</span><span class="sxs-lookup"><span data-stu-id="c7823-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

