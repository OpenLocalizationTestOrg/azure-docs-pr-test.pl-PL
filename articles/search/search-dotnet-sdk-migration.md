---
title: "toohello aaaUpgrading zestawu .NET SDK w wersji 1.1 dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Uaktualnianie toohello zestawu SDK usługi Azure Search .NET w wersji 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="4793a-103">Uaktualnianie toohello zestawu SDK usługi Azure Search .NET w wersji 3</span><span class="sxs-lookup"><span data-stu-id="4793a-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="4793a-104">Jeśli używasz wersji 2.0 — wersja zapoznawcza lub starszej programu hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk), ten artykuł pomoże Ci uaktualnienie wersji toouse aplikacji 3.</span><span class="sxs-lookup"><span data-stu-id="4793a-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="4793a-105">Aby uzyskać bardziej ogólne wskazówki hello SDK tym przykłady, zobacz [jak toouse Azure wyszukiwanie od aplikacji .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4793a-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="4793a-106">Wersja 3 hello zestawu .NET SDK usługi Azure Search zawiera pewne zmiany z wcześniejszych wersji.</span><span class="sxs-lookup"><span data-stu-id="4793a-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="4793a-107">Są to przede wszystkim niewielkie, tak więc zmiana kodu powinny wymagać tylko minimalnym wysiłku.</span><span class="sxs-lookup"><span data-stu-id="4793a-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="4793a-108">Zobacz [tooupgrade kroki](#UpgradeSteps) instrukcje na temat toochange Twojego nowej wersji zestawu SDK kodu toouse hello.</span><span class="sxs-lookup"><span data-stu-id="4793a-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="4793a-109">Jeśli używasz wersji 1.0.2-preview lub starsze, należy najpierw uaktualnić tooversion 1.1, a następnie Uaktualnij tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="4793a-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="4793a-110">Zobacz [dodatku: kroki tooupgrade tooversion 1.1](#UpgradeStepsV1) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="4793a-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="4793a-111">Wystąpienia usługi Azure Search obsługuje kilka wersji interfejsu API REST, w tym hello najnowszy numer.</span><span class="sxs-lookup"><span data-stu-id="4793a-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="4793a-112">Można kontynuować toouse wersji, gdy nie jest już hello najnowszego, ale zaleca się przeprowadzenie migracji kodu toouse hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="4793a-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="4793a-113">Korzystając z hello interfejsu API REST, należy określić wersję interfejsu API hello w każde żądanie za pośrednictwem parametru api-version hello.</span><span class="sxs-lookup"><span data-stu-id="4793a-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="4793a-114">Używając hello zestawu .NET SDK, wersja hello hello używasz zestawu SDK określa hello odpowiedniej wersji hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4793a-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="4793a-115">Jeśli używasz starszej zestawu SDK można kontynuować toorun kodu bez zmian, nawet jeśli usługa hello jest wersja uaktualniona toosupport nowszej interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4793a-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="4793a-116">Nowości w wersji 3</span><span class="sxs-lookup"><span data-stu-id="4793a-116">What's new in version 3</span></span>
<span data-ttu-id="4793a-117">Wersja 3 hello elementów docelowych zestawu .NET SDK usługi Azure Search hello najnowszej wersji ogólnie dostępna hello interfejsu API REST wyszukiwanie Azure, w szczególności 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="4793a-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="4793a-118">Dzięki temu możliwe toouse wiele nowych funkcji usługi Azure Search z aplikacji .NET, w tym następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4793a-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="4793a-119">Analizatory niestandardowe</span><span class="sxs-lookup"><span data-stu-id="4793a-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="4793a-120">[Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md) i [Azure Table Storage](search-howto-indexing-azure-tables.md) indeksatorze obsługi</span><span class="sxs-lookup"><span data-stu-id="4793a-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="4793a-121">Dostosowywanie indeksatora za pośrednictwem [mapowań pól](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="4793a-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="4793a-122">Elementy etag obsługuje tooenable bezpieczne równoczesnych aktualizowania indeksu definicje, indeksatorów i źródeł danych</span><span class="sxs-lookup"><span data-stu-id="4793a-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="4793a-123">Obsługę tworzenia indeksu definicje pól deklaratywnie dekoracji klasy modelu, a następnie użyć nowego hello `FieldBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="4793a-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="4793a-124">Obsługa platformy .NET Core i przenośnych profilu platformy .NET 111</span><span class="sxs-lookup"><span data-stu-id="4793a-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="4793a-125">Kroki tooupgrade</span><span class="sxs-lookup"><span data-stu-id="4793a-125">Steps tooupgrade</span></span>
<span data-ttu-id="4793a-126">Najpierw należy zaktualizować odwołania programu NuGet dla `Microsoft.Azure.Search` używając albo hello Konsola Menedżera pakietów NuGet lub przez kliknięcie prawym przyciskiem myszy odwołania projektu i wybierając pozycję "Zarządzaj NuGet pakietów..." w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4793a-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="4793a-127">Po NuGet pobrała nowe pakiety hello oraz ich zależności, ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="4793a-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="4793a-128">W zależności od struktury kodu jego może odbudować pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4793a-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="4793a-129">Jeśli tak, wszystko jest gotowe toogo!</span><span class="sxs-lookup"><span data-stu-id="4793a-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="4793a-130">W przypadku niepowodzenia kompilacji powinien zostać wyświetlony błąd kompilacji, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4793a-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="4793a-131">Witaj, następnym krokiem jest toofix ten błąd kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="4793a-132">Zobacz [fundamentalne zmiany w wersji 3](#ListOfChanges) szczegółowe informacje na temat co powoduje błąd hello i w jaki sposób toofix go.</span><span class="sxs-lookup"><span data-stu-id="4793a-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="4793a-133">Dodatkowe kompilacji może zostać wyświetlony ostrzeżenia dotyczące tooobsolete metody lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="4793a-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="4793a-134">ostrzeżenia Hello zawiera instrukcje dotyczące jakie toouse zamiast z hello przestarzałe funkcji.</span><span class="sxs-lookup"><span data-stu-id="4793a-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="4793a-135">Na przykład, jeśli aplikacja używa hello `IndexingParameters.Base64EncodeKeys` właściwość, należy pobrać ostrzeżenie informujące,`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="4793a-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="4793a-136">Gdy problem został rozwiązany błędy kompilacji, możesz wprowadzić zmiany tooyour aplikacji tootake korzystać z nowych funkcji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4793a-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="4793a-137">Nowe funkcje w hello SDK wyszczególnione w [nowości w wersji 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="4793a-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="4793a-138">Fundamentalne zmiany w wersji 3</span><span class="sxs-lookup"><span data-stu-id="4793a-138">Breaking changes in version 3</span></span>
<span data-ttu-id="4793a-139">Brak niewielkiej liczby zmian podziału w wersji 3, które mogą wymagać kod zmienia dodatkowo toorebuilding aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="4793a-140">Zwracany typ Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="4793a-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="4793a-141">Witaj `Indexes.GetClient` metoda ma nowy typ zwracany.</span><span class="sxs-lookup"><span data-stu-id="4793a-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="4793a-142">Wcześniej, zwracana `SearchIndexClient`, ale ta zmiana została wprowadzona zbyt`ISearchIndexClient` w wersji 2.0-preview, a zmiany są przenoszone tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="4793a-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="4793a-143">Jest to toosupport klientów, którzy mają toomock hello `GetClient` metodę dla testów jednostkowych przez zwrócenie implementację testową z `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="4793a-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="4793a-144">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-144">Example</span></span>
<span data-ttu-id="4793a-145">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="4793a-146">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="4793a-147">AnalyzerName, typ danych i inne osoby nie są już toostrings umożliwiają niejawnej konwersji</span><span class="sxs-lookup"><span data-stu-id="4793a-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="4793a-148">Istnieje wiele typów w hello Azure Search .NET SDK, który pochodzi z `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="4793a-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="4793a-149">Wcześniej te typy zostały wszystkie niejawnego tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="4793a-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="4793a-150">Jednak usterki zostało odnalezione hello `Object.Equals` implementacji dla tych klas i ustalające usterki hello wymagane wyłączenie niejawnej konwersji.</span><span class="sxs-lookup"><span data-stu-id="4793a-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="4793a-151">Jawna konwersja zbyt`string` jest nadal dozwolone.</span><span class="sxs-lookup"><span data-stu-id="4793a-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="4793a-152">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-152">Example</span></span>
<span data-ttu-id="4793a-153">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="4793a-154">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="4793a-155">Usunięte przestarzali członkowie</span><span class="sxs-lookup"><span data-stu-id="4793a-155">Removed obsolete members</span></span>

<span data-ttu-id="4793a-156">Może pojawić się właściwości, które zostały oznaczone jako przestarzałe w wersji 2.0-preview, a później usunięte w wersji 3 lub toomethods powiązane błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="4793a-157">Jeśli wystąpią błędy takie, Oto jak tooresolve je:</span><span class="sxs-lookup"><span data-stu-id="4793a-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="4793a-158">W przypadku używania tego konstruktora: `ScoringParameter(string name, string value)`, zamiast tego użyj tego:`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="4793a-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="4793a-159">W przypadku używania hello `ScoringParameter.Value` właściwość, użyj hello `ScoringParameter.Values` właściwości lub hello `ToString` metody zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="4793a-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="4793a-160">W przypadku używania hello `SearchRequestOptions.RequestId` właściwość, użyj hello `ClientRequestId` właściwości zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="4793a-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="4793a-161">Funkcje usunięte w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="4793a-161">Removed preview features</span></span>

<span data-ttu-id="4793a-162">Jeśli uaktualniasz tooversion Podgląd 2.0 w wersji 3 należy pamiętać, że JSON i analizowania pomocy technicznej dla obiekt Blob indeksatorów CSV została usunięta, ponieważ te funkcje są nadal w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="4793a-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="4793a-163">W szczególności hello następujące metody hello `IndexingParametersExtensions` klasy zostały usunięte:</span><span class="sxs-lookup"><span data-stu-id="4793a-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="4793a-164">Jeśli aplikacja ma twardych zależność od tych funkcji, nie będzie możliwe tooupgrade tooversion 3 z hello zestawu .NET SDK usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4793a-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="4793a-165">Można kontynuować toouse wersji 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="4793a-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="4793a-166">Jednak należy należy pamiętać, że **zaleca się używania Podgląd zestawów SDK w aplikacji produkcyjnych**.</span><span class="sxs-lookup"><span data-stu-id="4793a-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="4793a-167">Funkcje w wersji zapoznawczej są tylko do oceny i może ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="4793a-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4793a-168">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4793a-168">Conclusion</span></span>
<span data-ttu-id="4793a-169">Aby uzyskać więcej informacji na temat używania hello zestawu .NET SDK usługi Azure Search, zobacz nasze niedawno zaktualizowanego [porad](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4793a-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="4793a-170">Chętnie poznamy Twoją opinię na powitania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4793a-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="4793a-171">Jeśli wystąpią problemy, możesz wolnego tooask nam Aby uzyskać pomoc dotyczącą hello [forum usługi Azure Search w witrynie MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="4793a-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="4793a-172">Jeśli napotkasz błąd, możesz pliku problemu w hello [repozytorium GitHub zestawu SDK .NET usługi Azure](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="4793a-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="4793a-173">Upewnij się, że tooprefix tytuł problemu z "wyszukiwania zestawu SDK:".</span><span class="sxs-lookup"><span data-stu-id="4793a-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="4793a-174">Dziękujemy za skorzystanie z usługi Azure Search!</span><span class="sxs-lookup"><span data-stu-id="4793a-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="4793a-175">Dodatek: Kroki tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="4793a-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="4793a-176">Ta sekcja dotyczy tylko toousers 1.0.2-preview wersji zestawu .NET SDK usługi Azure Search hello i starszych.</span><span class="sxs-lookup"><span data-stu-id="4793a-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="4793a-177">Najpierw należy zaktualizować odwołania programu NuGet dla `Microsoft.Azure.Search` używając albo hello Konsola Menedżera pakietów NuGet lub przez kliknięcie prawym przyciskiem myszy odwołania projektu i wybierając pozycję "Zarządzaj NuGet pakietów..." w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4793a-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="4793a-178">Po NuGet pobrała nowe pakiety hello oraz ich zależności, ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="4793a-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="4793a-179">Jeśli wcześniej przy użyciu wersji 1.0.0-preview, 1.0.1-preview lub 1.0.2-preview, hello ma być pomyślnie wykonane i wszystko jest gotowe toogo!</span><span class="sxs-lookup"><span data-stu-id="4793a-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="4793a-180">Jeśli zostały wcześniej przy użyciu wersji 0.13.0-preview lub starsze, powinny pojawić się błędy, takie jak następujące hello kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="4793a-181">Witaj następnym krokiem jest błędy kompilacji hello toofix jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="4793a-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="4793a-182">Większość wymaga zmiana niektóre nazwy klasy i metody, których nazwy zostały zmienione w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4793a-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="4793a-183">[Lista fundamentalne zmiany w wersji 1.1](#ListOfChangesV1) zawiera listę tych zmian nazw.</span><span class="sxs-lookup"><span data-stu-id="4793a-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="4793a-184">Jeśli używasz niestandardowej klasy toomodel dokumentów, a te klasy mają właściwości typów pierwotnych wartości null (na przykład `int` lub `bool` w języku C#), jest w wersji hello 1.1 hello zestawu SDK, które należy zwrócić uwagę poprawkę.</span><span class="sxs-lookup"><span data-stu-id="4793a-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="4793a-185">Zobacz [poprawki błędów w wersji 1.1](#BugFixesV1) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="4793a-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="4793a-186">Ponadto po problem został rozwiązany błędy kompilacji, możesz wprowadzić zmiany tooyour aplikacji tootake korzystać z nowych funkcji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4793a-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="4793a-187">Lista fundamentalne zmiany w wersji 1.1</span><span class="sxs-lookup"><span data-stu-id="4793a-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="4793a-188">Witaj poniżej jest określona przez prawdopodobieństwo hello czy hello zmiany będzie miało wpływ na kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="4793a-189">IndexBatch i IndexAction zmian</span><span class="sxs-lookup"><span data-stu-id="4793a-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="4793a-190">`IndexBatch.Create`Zmieniono zbyt`IndexBatch.New` i nie ma już `params` argumentu.</span><span class="sxs-lookup"><span data-stu-id="4793a-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="4793a-191">Można użyć `IndexBatch.New` partii, które mieszać różnego rodzaju akcje (scalenia, usuwa itp.).</span><span class="sxs-lookup"><span data-stu-id="4793a-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="4793a-192">Ponadto istnieją nowe metody statyczne do tworzenia instancji gdzie wszystkie akcje hello są takie same hello: `Delete`, `Merge`, `MergeOrUpload`, i `Upload`.</span><span class="sxs-lookup"><span data-stu-id="4793a-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="4793a-193">`IndexAction`nie ma konstruktorów publicznych i jego właściwości są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="4793a-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="4793a-194">Należy użyć nowych metod statycznych hello tworzenia akcje do różnych celów: `Delete`, `Merge`, `MergeOrUpload`, i `Upload`.</span><span class="sxs-lookup"><span data-stu-id="4793a-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="4793a-195">`IndexAction.Create`została usunięta.</span><span class="sxs-lookup"><span data-stu-id="4793a-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="4793a-196">Jeśli używane jest przeciążenie hello, który przyjmuje tylko dokumenty, upewnij się, że toouse `Upload` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="4793a-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="4793a-197">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-197">Example</span></span>
<span data-ttu-id="4793a-198">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="4793a-199">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="4793a-200">Jeśli chcesz, możesz dodatkowo upraszcza go toothis:</span><span class="sxs-lookup"><span data-stu-id="4793a-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="4793a-201">IndexBatchException zmiany</span><span class="sxs-lookup"><span data-stu-id="4793a-201">IndexBatchException changes</span></span>
<span data-ttu-id="4793a-202">Witaj `IndexBatchException.IndexResponse` właściwości została zmieniona za`IndexingResults`, a jej typ jest teraz `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="4793a-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="4793a-203">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-203">Example</span></span>
<span data-ttu-id="4793a-204">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="4793a-205">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="4793a-206">Operacja zmiany — metoda</span><span class="sxs-lookup"><span data-stu-id="4793a-206">Operation method changes</span></span>
<span data-ttu-id="4793a-207">Każdej operacji w hello zestawu .NET SDK usługi Azure Search jest ujawniona jako zbiór przeciążenia metody dla wywoływania synchroniczne i asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="4793a-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="4793a-208">Witaj podpisów i factoring z tych przeciążenia metody została zmieniona w wersji 1.1.</span><span class="sxs-lookup"><span data-stu-id="4793a-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="4793a-209">Na przykład Witaj "Uzyskać statystyki indeksu" operacji w starszych wersjach hello SDK widoczne te podpisy:</span><span class="sxs-lookup"><span data-stu-id="4793a-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="4793a-210">W `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="4793a-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="4793a-211">W `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="4793a-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="4793a-212">Sygnatury metody Hello hello tej samej operacji w wersji 1.1 wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="4793a-213">W `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="4793a-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="4793a-214">W `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="4793a-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="4793a-215">Począwszy od wersji 1.1, hello zestawu .NET SDK usługi Azure Search porządkuje metody operacji inaczej:</span><span class="sxs-lookup"><span data-stu-id="4793a-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="4793a-216">Parametry opcjonalne są teraz modelowane jako domyślne parametry raczej niż przeciążenia metody dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="4793a-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="4793a-217">Czasami znacznie zmniejsza liczbę hello przeciążenia metody.</span><span class="sxs-lookup"><span data-stu-id="4793a-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="4793a-218">metody rozszerzenia Hello Ukryj teraz dużo hello nadmiarowe szczegóły HTTP z hello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="4793a-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="4793a-219">Na przykład starsze wersje zestawu SDK zwrócił obiekt odpowiedzi z kodem stanu HTTP, która będzie często hello nie potrzebuję toocheck, ponieważ throw metody operacji `CloudException` dla dowolnego kodu stanu wskazujący błąd.</span><span class="sxs-lookup"><span data-stu-id="4793a-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="4793a-220">Witaj nowe obiekty modelu Zwróć metody rozszerzenia, zapisywanie możesz hello problemy o toounwrap je w kodzie.</span><span class="sxs-lookup"><span data-stu-id="4793a-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="4793a-221">Z drugiej strony hello podstawowych interfejsów teraz ujawniać metod, które zapewniają większą kontrolę na poziomie hello HTTP, jeśli zajdzie taka potrzeba.</span><span class="sxs-lookup"><span data-stu-id="4793a-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="4793a-222">Teraz można przekazać niestandardowe toobe nagłówki HTTP dołączone do żądania i hello nowe `AzureOperationResponse<T>` zwracany typ zapewnia bezpośredni dostęp do toohello `HttpRequestMessage` i `HttpResponseMessage` hello operacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="4793a-223">`AzureOperationResponse`jest zdefiniowany w hello `Microsoft.Rest.Azure` przestrzeni nazw i zastępuje `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="4793a-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="4793a-224">ScoringParameters zmiany</span><span class="sxs-lookup"><span data-stu-id="4793a-224">ScoringParameters changes</span></span>
<span data-ttu-id="4793a-225">Nową klasę o nazwie `ScoringParameter` zostało dodane w najnowszej toomake SDK hello łatwiejsze profile tooscoring tooprovide parametrów w zapytaniu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="4793a-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="4793a-226">Wcześniej hello `ScoringProfiles` właściwości hello `SearchParameters` klasy została wpisana jako `IList<string>`; Teraz jest wpisana jako `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="4793a-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="4793a-227">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-227">Example</span></span>
<span data-ttu-id="4793a-228">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="4793a-229">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="4793a-230">Zmiany modelu klasy</span><span class="sxs-lookup"><span data-stu-id="4793a-230">Model class changes</span></span>
<span data-ttu-id="4793a-231">Powodu toohello podpisu zmian opisanych w [operację zmiany metody](#OperationMethodChanges), wiele klas w hello `Microsoft.Azure.Search.Models` przestrzeni nazw został przeniesiony lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="4793a-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="4793a-232">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4793a-232">For example:</span></span>

* <span data-ttu-id="4793a-233">`IndexDefinitionResponse`został zastąpiony`AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="4793a-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="4793a-234">`DocumentSearchResponse`Zmieniono zbyt`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="4793a-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="4793a-235">`IndexResult`Zmieniono zbyt`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="4793a-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="4793a-236">`Documents.Count()`obecnie zwraca `long` o liczbie dokumentów hello zamiast`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="4793a-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="4793a-237">`IndexGetStatisticsResponse`Zmieniono zbyt`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="4793a-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="4793a-238">`IndexListResponse`Zmieniono zbyt`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="4793a-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="4793a-239">toosummarize, `OperationResponse`-pochodzi z klasy, które były dostępne tylko toowrap obiekt modelu zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="4793a-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="4793a-240">Witaj pozostałych klasy miały ich sufiks zmieniła się z `Response` zbyt`Result`.</span><span class="sxs-lookup"><span data-stu-id="4793a-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="4793a-241">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-241">Example</span></span>
<span data-ttu-id="4793a-242">Jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="4793a-243">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="4793a-244">Klasy odpowiedzi i IEnumerable</span><span class="sxs-lookup"><span data-stu-id="4793a-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="4793a-245">Dodatkowe zmiany, które mogą mieć wpływ na kod jest klasy odpowiedzi, zawierających kolekcje nie implementuje `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="4793a-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="4793a-246">Zamiast tego można bezpośredni dostęp hello właściwości kolekcji.</span><span class="sxs-lookup"><span data-stu-id="4793a-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="4793a-247">Na przykład, jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="4793a-248">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="4793a-249">Szczególnych przypadkach dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="4793a-249">Special case for web applications</span></span>
<span data-ttu-id="4793a-250">Jeśli masz aplikację sieci web, który serializuje `DocumentSearchResponse` bezpośrednio w przeglądarce toohello wyniki wyszukiwania toosend, konieczne będzie toochange kodu lub hello wyniki nie zostaną poprawnie serializować.</span><span class="sxs-lookup"><span data-stu-id="4793a-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="4793a-251">Na przykład, jeśli kod wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="4793a-252">Można ją zmienić, pobierając hello `.Results` właściwości hello wyszukiwania odpowiedzi toofix wyszukiwania wynik renderowania:</span><span class="sxs-lookup"><span data-stu-id="4793a-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="4793a-253">Konieczne będzie toolook w takich przypadkach w kodzie **hello kompilatora nie ostrzega** ponieważ `JsonResult.Data` jest typu `object`.</span><span class="sxs-lookup"><span data-stu-id="4793a-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="4793a-254">CloudException zmiany</span><span class="sxs-lookup"><span data-stu-id="4793a-254">CloudException changes</span></span>
<span data-ttu-id="4793a-255">Witaj `CloudException` klasy została przeniesiona z hello `Hyak.Common` toohello przestrzeni nazw `Microsoft.Rest.Azure` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4793a-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="4793a-256">Ponadto jego `Error` zbyt zmieniono właściwość`Body`.</span><span class="sxs-lookup"><span data-stu-id="4793a-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="4793a-257">Zmiany SearchServiceClient i SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="4793a-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="4793a-258">Witaj typu hello `Credentials` właściwość zostanie zmieniona z `SearchCredentials` tooits podstawowa klasa `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4793a-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="4793a-259">Jeśli potrzebujesz tooaccess hello `SearchCredentials` z `SearchIndexClient` lub `SearchServiceClient`, użyj nowego hello `SearchCredentials` właściwości.</span><span class="sxs-lookup"><span data-stu-id="4793a-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="4793a-260">W starszych wersjach hello zestawu SDK `SearchServiceClient` i `SearchIndexClient` ma konstruktorów, które miały `HttpClient` parametru.</span><span class="sxs-lookup"><span data-stu-id="4793a-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="4793a-261">Te zostały zastąpione konstruktorów przyjmujących `HttpClientHandler` i tablica `DelegatingHandler` obiektów.</span><span class="sxs-lookup"><span data-stu-id="4793a-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="4793a-262">Dzięki temu można łatwiej tooinstall niestandardowe programy obsługi procesu toopre żądań HTTP w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4793a-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="4793a-263">Na koniec hello konstruktorów, które miały `Uri` i `SearchCredentials` zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="4793a-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="4793a-264">Na przykład, jeśli kod, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="4793a-265">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="4793a-266">Ponadto należy pamiętać, że typ hello hello poświadczenia parametru został zmieniony zbyt`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4793a-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="4793a-267">Jest to prawdopodobnie nie tooaffect kodu od `SearchCredentials` jest pochodną `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4793a-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="4793a-268">Przekazywanie identyfikator żądania</span><span class="sxs-lookup"><span data-stu-id="4793a-268">Passing a request ID</span></span>
<span data-ttu-id="4793a-269">Identyfikator żądania w starszych wersjach hello zestawu SDK, można ustawić na powitania `SearchServiceClient` lub `SearchIndexClient` i może być uwzględniony w każdym toohello żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4793a-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="4793a-270">Jest to przydatne podczas rozwiązywania problemów z usługą wyszukiwania, jeśli potrzebujesz pomocy technicznej toocontact.</span><span class="sxs-lookup"><span data-stu-id="4793a-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="4793a-271">Jednak jest bardziej użyteczne tooset Unikatowy identyfikator dla każdej operacji zamiast toouse hello tym samym identyfikatorze dla wszystkich operacji.</span><span class="sxs-lookup"><span data-stu-id="4793a-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="4793a-272">Z tego powodu hello `SetClientRequestId` metody `SearchServiceClient` i `SearchIndexClient` zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="4793a-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="4793a-273">Zamiast tego można przekazać metodę operacji tooeach identyfikator żądania za pośrednictwem hello opcjonalne `SearchRequestOptions` parametru.</span><span class="sxs-lookup"><span data-stu-id="4793a-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="4793a-274">W przyszłym wydaniu hello zestawu SDK zostanie dodany nowy mechanizm do ustawiania Identyfikatora żądania globalnie na powitania klienta obiektów zgodny z podejścia hello używane przez innych zestawów SDK usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4793a-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="4793a-275">Przykład</span><span class="sxs-lookup"><span data-stu-id="4793a-275">Example</span></span>
<span data-ttu-id="4793a-276">Jeśli masz kod, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4793a-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="4793a-277">Można zmienić toothis toofix wszelkie błędy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="4793a-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="4793a-278">Zmiany nazwy interfejsu</span><span class="sxs-lookup"><span data-stu-id="4793a-278">Interface name changes</span></span>
<span data-ttu-id="4793a-279">nazwy interfejsu grup operacja Hello są wszystkie zmienione toobe zgodne z odpowiadającymi im nazwami właściwości:</span><span class="sxs-lookup"><span data-stu-id="4793a-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="4793a-280">Witaj typu `ISearchServiceClient.Indexes` została zmieniona z `IIndexOperations` zbyt`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="4793a-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="4793a-281">Witaj typu `ISearchServiceClient.Indexers` została zmieniona z `IIndexerOperations` zbyt`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="4793a-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="4793a-282">Witaj typu `ISearchServiceClient.DataSources` została zmieniona z `IDataSourceOperations` zbyt`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="4793a-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="4793a-283">Witaj typu `ISearchIndexClient.Documents` została zmieniona z `IDocumentOperations` zbyt`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="4793a-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="4793a-284">Ta zmiana jest kod tooaffect mało prawdopodobne, chyba że zostaną utworzone mocks te interfejsy do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="4793a-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="4793a-285">Poprawki błędów w wersji 1.1</span><span class="sxs-lookup"><span data-stu-id="4793a-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="4793a-286">Wystąpił błąd w starszych wersjach tooserialization dotyczące zestawu .NET SDK usługi Azure Search hello klas niestandardowych modelu.</span><span class="sxs-lookup"><span data-stu-id="4793a-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="4793a-287">Hello błąd mógł wystąpić, jeśli klasę modelu niestandardowe zostały utworzone z właściwością typu niedopuszczające wartości.</span><span class="sxs-lookup"><span data-stu-id="4793a-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="4793a-288">Kroki tooreproduce</span><span class="sxs-lookup"><span data-stu-id="4793a-288">Steps tooreproduce</span></span>
<span data-ttu-id="4793a-289">Utwórz klasę modelu niestandardowych z właściwością typ niedopuszczający wartości null.</span><span class="sxs-lookup"><span data-stu-id="4793a-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="4793a-290">Na przykład, Dodaj publiczną `UnitCount` właściwości typu `int` zamiast `int?`.</span><span class="sxs-lookup"><span data-stu-id="4793a-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="4793a-291">Jeśli indeks dokument z wartością domyślną hello tego typu (na przykład 0 dla `int`), pole hello będzie mieć wartość null w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4793a-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="4793a-292">Następnie wyszukiwania dla tego dokumentu, hello `Search` zgłosi wywołania `JsonSerializationException` strona skarżąca, który nie może przekonwertować `null` zbyt`int`.</span><span class="sxs-lookup"><span data-stu-id="4793a-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="4793a-293">Ponadto filtry mogą nie działać zgodnie z oczekiwaniami, ponieważ wartość null została napisana indeksu toohello zamiast wartości hello przeznaczone.</span><span class="sxs-lookup"><span data-stu-id="4793a-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="4793a-294">Usuń szczegóły</span><span class="sxs-lookup"><span data-stu-id="4793a-294">Fix details</span></span>
<span data-ttu-id="4793a-295">Ten problem został rozwiązany w wersji 1.1 hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4793a-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="4793a-296">Teraz, jeśli masz klasę modelu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4793a-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="4793a-297">i `IntValue` too0, czy wartość jest teraz prawidłowo zserializowanej 0 umieszczonego hello i przechowywane jako 0 hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="4793a-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="4793a-298">Również uruchomienie round działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="4793a-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="4793a-299">Jest świadome tego podejścia przy rozwiązywaniu jednego toobe potencjalny problem: Jeśli używasz typu modelu z właściwością wartości null, jest zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello.</span><span class="sxs-lookup"><span data-stu-id="4793a-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="4793a-300">Hello zestawu SDK ani hello API REST usługi Azure Search nie pomoże tooenforce można to.</span><span class="sxs-lookup"><span data-stu-id="4793a-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="4793a-301">To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="4793a-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="4793a-302">Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search).</span><span class="sxs-lookup"><span data-stu-id="4793a-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="4793a-303">Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:</span><span class="sxs-lookup"><span data-stu-id="4793a-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="4793a-304">Z tego powodu Będziemy nadal zaleca się używanie typów dopuszczających wartości zerowe w klasach modeli najlepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="4793a-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="4793a-305">Aby uzyskać więcej szczegółów na tej poprawki błędów i hello, zobacz [ten problem w usłudze GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="4793a-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

