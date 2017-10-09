---
title: "źródła danych profilu tooData aaaHow"
description: "Tooarticle jak wyróżnianie jak danych na poziomie tabeli i kolumny tooinclude profile podczas rejestrowania źródła danych w usłudze Azure Data Catalog i jak danych toouse profile toounderstand źródeł danych."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="e059f-103">Źródła danych profilu danych</span><span class="sxs-lookup"><span data-stu-id="e059f-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="e059f-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e059f-104">Introduction</span></span>
<span data-ttu-id="e059f-105">**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="e059f-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="e059f-106">Innymi słowy **Azure Data Catalog** wszystkie o osobach myśl odnajdywania, zrozumienia i używania źródeł danych, a także pomaga organizacjom tooget więcej wartość z ich istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="e059f-107">Jeśli źródło danych jest zarejestrowana w usłudze **Azure Data Catalog**, jego metadanych jest kopiowany i indeksowane przez usługę hello, ale hello wątku nie istnieje zakończyć.</span><span class="sxs-lookup"><span data-stu-id="e059f-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="e059f-108">Witaj **danych profilowania** funkcji **Azure Data Catalog** sprawdza hello danych z obsługiwanych źródeł danych w katalogu i zbiera dane statystyczne i informacje o tych danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="e059f-109">Jest łatwy tooinclude profil zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="e059f-110">Podczas rejestrowania zasobów danych, wybierz **obejmują dane profilu** w narzędzia rejestracji źródła danych hello.</span><span class="sxs-lookup"><span data-stu-id="e059f-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="e059f-111">Co to jest danych profilowania</span><span class="sxs-lookup"><span data-stu-id="e059f-111">What is Data Profiling</span></span>
<span data-ttu-id="e059f-112">Dane profilowania sprawdza hello danych w źródle danych hello jest zarejestrowany i zbiera dane statystyczne i informacje o tych danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="e059f-113">Podczas odnajdowania źródła danych statystyki te mogą ułatwić określenie przydatności hello toosolve danych hello problemy biznesowe.</span><span class="sxs-lookup"><span data-stu-id="e059f-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="e059f-114">Witaj następujące źródła danych obsługuje dane profilowania:</span><span class="sxs-lookup"><span data-stu-id="e059f-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="e059f-115">SQL Server (łącznie z bazy danych SQL Azure i usługi Azure SQL Data Warehouse) tabel i widoków</span><span class="sxs-lookup"><span data-stu-id="e059f-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="e059f-116">Oracle tabele i widoki</span><span class="sxs-lookup"><span data-stu-id="e059f-116">Oracle tables and views</span></span>
* <span data-ttu-id="e059f-117">Teradata tabele i widoki</span><span class="sxs-lookup"><span data-stu-id="e059f-117">Teradata tables and views</span></span>
* <span data-ttu-id="e059f-118">Tabele programu hive</span><span class="sxs-lookup"><span data-stu-id="e059f-118">Hive tables</span></span>

<span data-ttu-id="e059f-119">Takie jak profile danych podczas rejestrowania zasobów danych ułatwia użytkownikom odpowiedzi na pytania dotyczące źródeł danych, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e059f-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="e059f-120">Może ona być używane toosolve Mój problem biznesowy?</span><span class="sxs-lookup"><span data-stu-id="e059f-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="e059f-121">Dane hello jest zgodny, standardów tooparticular lub wzorce?</span><span class="sxs-lookup"><span data-stu-id="e059f-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="e059f-122">Jakie są anomalii hello hello źródła danych?</span><span class="sxs-lookup"><span data-stu-id="e059f-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="e059f-123">Co to są potencjalnych problemów o włączenie tych danych do mojej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="e059f-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="e059f-124">Można również dodać toodescribe zasobów tooan dokumentacji jak danych może być zintegrowane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e059f-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="e059f-125">Zobacz [jak źródeł danych toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="e059f-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="e059f-126">Jak tooinclude danych profilu podczas rejestrowania źródła danych</span><span class="sxs-lookup"><span data-stu-id="e059f-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="e059f-127">Jest łatwy tooinclude profilu źródła danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="e059f-128">Podczas rejestrowania źródła danych w hello **toobe obiektów w zarejestrowany** panelu rejestracji źródła danych hello narzędzie, wybierz **obejmują dane profilu**.</span><span class="sxs-lookup"><span data-stu-id="e059f-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="e059f-129">więcej informacji o toolearn, tooregister źródeł danych, zobacz temat [jak źródeł danych tooregister](data-catalog-how-to-register.md) i [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e059f-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="e059f-130">Filtrowanie zasobów danych, które dotyczą profili danych</span><span class="sxs-lookup"><span data-stu-id="e059f-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="e059f-131">toodiscover zasobów danych, które obejmują profilu danych, mogą obejmować `has:tableDataProfiles` lub `has:columnsDataProfiles` jako jeden z warunkami wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e059f-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="e059f-132">Wybieranie **obejmują dane profilu** danych hello narzędzia rejestracji źródła zawiera tabelę i informacje o profilu na poziomie kolumny.</span><span class="sxs-lookup"><span data-stu-id="e059f-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="e059f-133">Jednak hello interfejsu API usługi Data Catalog pozwala toobe zasoby danych zarejestrowany tylko jeden zestaw uwzględnione informacje o profilu.</span><span class="sxs-lookup"><span data-stu-id="e059f-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="e059f-134">Wyświetlanie informacji o profilu danych</span><span class="sxs-lookup"><span data-stu-id="e059f-134">Viewing data profile information</span></span>
<span data-ttu-id="e059f-135">Po znalezieniu źródła danych odpowiednie za pomocą profilu można wyświetlić szczegółów profilu hello danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="e059f-136">tooview hello danych profilu, zaznacz zasobu danych i wybierz polecenie **profilu danych** w oknie portalu wykazu danych hello.</span><span class="sxs-lookup"><span data-stu-id="e059f-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="e059f-137">Dane profilu w **Azure Data Catalog** zawiera tabela i kolumna profilu informacje w tym:</span><span class="sxs-lookup"><span data-stu-id="e059f-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="e059f-138">Obiekt danych profilu</span><span class="sxs-lookup"><span data-stu-id="e059f-138">Object data profile</span></span>
* <span data-ttu-id="e059f-139">Liczba wierszy</span><span class="sxs-lookup"><span data-stu-id="e059f-139">Number of rows</span></span>
* <span data-ttu-id="e059f-140">Rozmiar tabeli</span><span class="sxs-lookup"><span data-stu-id="e059f-140">Table size</span></span>
* <span data-ttu-id="e059f-141">Gdy obiekt hello ostatniej aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e059f-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="e059f-142">Kolumny danych profilu</span><span class="sxs-lookup"><span data-stu-id="e059f-142">Column data profile</span></span>
* <span data-ttu-id="e059f-143">Typ danych kolumny</span><span class="sxs-lookup"><span data-stu-id="e059f-143">Column data type</span></span>
* <span data-ttu-id="e059f-144">Liczba wartości odrębnych</span><span class="sxs-lookup"><span data-stu-id="e059f-144">Number of distinct values</span></span>
* <span data-ttu-id="e059f-145">Liczba wierszy z wartości NULL</span><span class="sxs-lookup"><span data-stu-id="e059f-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="e059f-146">Minimalna, maksymalna, średnia i odchylenie standardowe dla wartości w kolumnie</span><span class="sxs-lookup"><span data-stu-id="e059f-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="e059f-147">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e059f-147">Summary</span></span>
<span data-ttu-id="e059f-148">Dane profilowania zawiera dane statystyczne i informacje o zarejestrowane ustalić hello przydatności problemów biznesowych toosolve danych hello toohelp zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="e059f-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="e059f-149">Wraz z adnotacji i dokumentowanie źródeł danych, danych profilów można umożliwić użytkownikom lepiej zrozumieć dane.</span><span class="sxs-lookup"><span data-stu-id="e059f-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="e059f-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e059f-150">See Also</span></span>
* [<span data-ttu-id="e059f-151">Jak tooregister źródeł danych</span><span class="sxs-lookup"><span data-stu-id="e059f-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="e059f-152">Rozpoczynanie pracy z usługą Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="e059f-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
