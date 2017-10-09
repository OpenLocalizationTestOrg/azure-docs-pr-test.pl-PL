---
title: "aaaAzure wyszukiwania Obsługa wielu języków | Dokumentacja firmy Microsoft"
description: "Usługa Azure Search obsługuje języki 56 wykorzystaniu analizatorów języka z Lucene i przetwarzania języka naturalnego technologii firmy Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="219fb-103">Tworzenie indeksu dla dokumentów w wielu językach w usłudze Azure Search</span><span class="sxs-lookup"><span data-stu-id="219fb-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="219fb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="219fb-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="219fb-105">REST</span><span class="sxs-lookup"><span data-stu-id="219fb-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="219fb-106">.NET</span><span class="sxs-lookup"><span data-stu-id="219fb-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="219fb-107">Unleashing moc hello analizatorów języka jest tak proste, jak jedną właściwość ustawienia w polu wyszukiwania w definicji indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="219fb-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="219fb-108">Teraz można wykonać ten krok w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="219fb-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="219fb-109">Poniżej przedstawiono zrzuty ekranu hello bloków portalu Azure do usługi Azure Search, która pozwala toodefine użytkowników schematu indeksu.</span><span class="sxs-lookup"><span data-stu-id="219fb-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="219fb-110">W tym bloku użytkownicy mogą tworzyć wszystkich pól hello i ustaw właściwość analizatora powitania dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="219fb-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="219fb-111">Można ustawić tylko analizatora języka podczas definicję pola, podobnie jak w podczas tworzenia nowego indeksu z hello tła w lub podczas dodawania nowego pola tooan istniejącego indeksu.</span><span class="sxs-lookup"><span data-stu-id="219fb-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="219fb-112">Upewnij się, że w pełni określić wszystkie atrybuty, w tym analizatora hello podczas tworzenia hello pola.</span><span class="sxs-lookup"><span data-stu-id="219fb-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="219fb-113">Nie można tooedit stanie atrybuty hello lub zmień typ analizatora hello po zapisaniu zmian.</span><span class="sxs-lookup"><span data-stu-id="219fb-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="219fb-114">Zdefiniuj nową definicję pola</span><span class="sxs-lookup"><span data-stu-id="219fb-114">Define a new field definition</span></span>
1. <span data-ttu-id="219fb-115">Zaloguj się toohello [portalu Azure](https://portal.azure.com) i otwórz hello bloku usługi usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="219fb-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="219fb-116">Kliknij przycisk **Dodaj indeks** w poleceniu hello pasek u góry hello toostart pulpitu nawigacyjnego usługi hello nowego indeksu lub Otwórz istniejący tooset indeksu analizatora na nowe pola, które dodajesz tooan istniejący indeks.</span><span class="sxs-lookup"><span data-stu-id="219fb-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="219fb-117">zostanie wyświetlony blok pola Hello, opcjami do definiowania schematu hello indeksu hello, w tym karty analizatora hello używany do wybierania analizatora języka.</span><span class="sxs-lookup"><span data-stu-id="219fb-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="219fb-118">W polach należy uruchomić definicja pola podanie nazwy, wybierając typ danych hello i ustawienie pola hello toomark atrybuty jako pełnotekstowe wyszukiwanie, pobieranie w wynikach wyszukiwania, można go użyć w strukturach nawigacji zestawu reguł, można sortować itd.</span><span class="sxs-lookup"><span data-stu-id="219fb-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="219fb-119">Przed przejściem dalej pola toohello, otwórz hello **analizator** kartę.</span><span class="sxs-lookup"><span data-stu-id="219fb-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="219fb-120">![][1]
*tooselect analizatora, kliknij kartę analizatora hello na powitania pola bloku*</span><span class="sxs-lookup"><span data-stu-id="219fb-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="219fb-121">Wybierz analizatora</span><span class="sxs-lookup"><span data-stu-id="219fb-121">Choose an analyzer</span></span>
1. <span data-ttu-id="219fb-122">Przewiń toofind hello pola, które są definiowane.</span><span class="sxs-lookup"><span data-stu-id="219fb-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="219fb-123">Jeśli pole hello jako wyszukiwanie nie jest zaznaczone, kliknij przycisk toomark teraz wyboru hello go jako **wyszukiwanie**.</span><span class="sxs-lookup"><span data-stu-id="219fb-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="219fb-124">Kliknij hello analizatora obszaru toodisplay hello listę dostępnych analizatorów.</span><span class="sxs-lookup"><span data-stu-id="219fb-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="219fb-125">Wybierz hello analyzer ma toouse.</span><span class="sxs-lookup"><span data-stu-id="219fb-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="219fb-126">![][2]
*Wybierz jedną z analizatorów hello obsługiwane dla każdego pola*</span><span class="sxs-lookup"><span data-stu-id="219fb-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="219fb-127">Domyślnie wszystkie pola z możliwością przeszukiwania używają hello [analizator standardowe Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) którego jest niezależny od języka.</span><span class="sxs-lookup"><span data-stu-id="219fb-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="219fb-128">tooview hello pełną listę obsługiwanych analizatorów, zobacz [Obsługa języków w usłudze Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="219fb-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="219fb-129">Po wybraniu hello analizatora języków dla pola będzie używany przy każdym żądaniu indeksowanie i wyszukiwania dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="219fb-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="219fb-130">Jeśli zapytanie jest wystawiony na podstawie wielu pól za pomocą różnych analizatorów, hello zapytania będą przetwarzane niezależnie przez hello analizatorów prawo dla każdego pola.</span><span class="sxs-lookup"><span data-stu-id="219fb-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="219fb-131">Wiele sieci web i aplikacji dla urządzeń przenośnych obsługiwać użytkowników na całym świecie hello przy użyciu różnych języków.</span><span class="sxs-lookup"><span data-stu-id="219fb-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="219fb-132">Jest to możliwe toodefine indeksu dla scenariusza, takich jak ta, tworząc pola dla każdego z języków obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="219fb-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="219fb-133">![][3]
*Definicja indeksu za pomocą pola Opis dla każdego z języków obsługiwanych*</span><span class="sxs-lookup"><span data-stu-id="219fb-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="219fb-134">Jeśli język hello agenta hello zapytania jest znany, żądania wyszukiwania może być zakresami tooa określonego pola, używając hello **searchFields** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="219fb-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="219fb-135">Hello następującej kwerendy będą wystawiane tylko względem opis hello w Polski:</span><span class="sxs-lookup"><span data-stu-id="219fb-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="219fb-136">Można zbadać indeksu z portalu hello przy użyciu **Eksplorator wyszukiwania** toopaste w toohello podobne zapytania pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="219fb-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="219fb-137">Eksplorator wyszukiwania jest dostępna z hello paska poleceń w bloku usługi hello.</span><span class="sxs-lookup"><span data-stu-id="219fb-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="219fb-138">Zobacz [tworzenie zapytań względem indeksu usługi Azure Search w portalu hello](search-explorer.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="219fb-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="219fb-139">Czasami hello języka agenta hello zapytania nie jest znany, w których wielkość hello zapytania mogą być wystawiane dla wszystkich pól jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="219fb-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="219fb-140">W razie potrzeby preferencji wyników w niektórych języku mogą być definiowane przy użyciu [oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="219fb-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="219fb-141">W poniższym przykładzie hello dopasowań w opisie hello w języku angielskim będą oceniane wyższej toomatches względne w Polski i francuskim:</span><span class="sxs-lookup"><span data-stu-id="219fb-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="219fb-142">Jeśli jesteś deweloperem .NET, należy pamiętać, że można skonfigurować przy użyciu hello analizatorów języka [zestawu .NET SDK usługi Azure Search](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="219fb-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="219fb-143">Najnowsza wersja Hello obsługuje również analizatorów języka Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="219fb-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
