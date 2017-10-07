---
title: "toowork aaaHow ze źródłami danych danych big data | Dokumentacja firmy Microsoft"
description: "Wzorce wyróżnienia tooarticle sposób korzystania z danych big data źródeł danych, łącznie z magazynu obiektów Blob Azure, usługa Azure Data Lake i system plików HDFS Hadoop przy użyciu usługi Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="06117-103">Jak źródeł toowork z danymi big data w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="06117-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="06117-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="06117-104">Introduction</span></span>
<span data-ttu-id="06117-105">**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="06117-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="06117-106">Przede wszystkim chodzi o pomaga osób odnajdywania, zrozumienia i używania źródeł danych oraz tooget organizacje więcej korzyści z ich istniejących źródeł danych, łącznie z danymi big data.</span><span class="sxs-lookup"><span data-stu-id="06117-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="06117-107">**Wykaz danych Azure** obsługuje hello rejestracji obiektów blob Azure blogu magazynu i katalogi, a także system plików HDFS Hadoop plików i katalogów.</span><span class="sxs-lookup"><span data-stu-id="06117-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="06117-108">Witaj częściowo ustrukturyzowanych rodzaj tych źródeł danych zapewnia dużą elastyczność.</span><span class="sxs-lookup"><span data-stu-id="06117-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="06117-109">Jednak tooget hello największych korzyści z rejestracji je za pomocą **Azure Data Catalog**, użytkowników należy wziąć pod uwagę organizowania hello źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="06117-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="06117-110">Katalogi jako logiczne zestawów danych</span><span class="sxs-lookup"><span data-stu-id="06117-110">Directories as logical data sets</span></span>
<span data-ttu-id="06117-111">Typowe wzorzec służący do organizowania źródeł danych big data jest tootreat katalogi jako logiczne zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="06117-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="06117-112">Katalogi najwyższego poziomu są używane toodefine zestawu danych podczas podfoldery Definiuj partycje, a same dane hello przechowywania hello pliki, które zawierają.</span><span class="sxs-lookup"><span data-stu-id="06117-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="06117-113">Przykładem tego wzorca może być:</span><span class="sxs-lookup"><span data-stu-id="06117-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="06117-114">W tym przykładzie vehicle_maintenance_events i location_tracking_events reprezentują logiczne zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="06117-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="06117-115">Każdy z tych folderów zawiera pliki danych, które są zorganizowane według rok i miesiąc w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="06117-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="06117-116">Każdy z tych folderów potencjalnie może zawierać, setek lub tysięcy plików.</span><span class="sxs-lookup"><span data-stu-id="06117-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="06117-117">W tym wzorcu rejestrowania poszczególnych plików z **Azure Data Catalog** prawdopodobnie nie ma sensu.</span><span class="sxs-lookup"><span data-stu-id="06117-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="06117-118">Zamiast tego należy zarejestrować hello katalogi, które reprezentują hello zbiory danych, które Praca z danymi hello użytkowników toohello łatwy do rozpoznania.</span><span class="sxs-lookup"><span data-stu-id="06117-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="06117-119">Odwołanie do danych plików</span><span class="sxs-lookup"><span data-stu-id="06117-119">Reference data files</span></span>
<span data-ttu-id="06117-120">Uzupełniające wzorzec jest zestawów danych referencyjnych toostore jako pojedyncze pliki.</span><span class="sxs-lookup"><span data-stu-id="06117-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="06117-121">Te zestawy danych mogą być uważane za strony danych big data "mała" hello, a często są podobne toodimensions w modelu danych analitycznych.</span><span class="sxs-lookup"><span data-stu-id="06117-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="06117-122">Odwołanie do danych plików zawiera rekordy, które są używane tooprovide kontekst dla zbiorczego hello hello plików danych przechowywanych w magazynie danych big data hello w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="06117-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="06117-123">Przykładem tego wzorca może być:</span><span class="sxs-lookup"><span data-stu-id="06117-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="06117-124">Pracując naukowca analityka lub dane z danymi hello w większych struktur katalogów hello tooprovide używany dla jednostek, które są określane tooonly według nazwy lub Identyfikatora w danych większych hello bardziej szczegółowe informacje można hello dane w tych plikach odwołania zestaw.</span><span class="sxs-lookup"><span data-stu-id="06117-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="06117-125">W tym wzorcu warto tooregister hello poszczególnych odwołanie do danych plików z **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="06117-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="06117-126">Każdy plik reprezentuje zestaw danych, a każdej z nich może być adnotowany i odnalezione pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="06117-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="06117-127">Alternatywne wzorce</span><span class="sxs-lookup"><span data-stu-id="06117-127">Alternate patterns</span></span>
<span data-ttu-id="06117-128">Witaj wzorce opisane w powyższej sekcji hello są tylko dwa różne sposoby, które mogą być organizowane przechowywania danych big data, ale każda implementacja jest inny.</span><span class="sxs-lookup"><span data-stu-id="06117-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="06117-129">Niezależnie od tego, jak strukturę źródeł danych, podczas rejestrowania źródła danych big data z **Azure Data Catalog**, skupić się na rejestracji hello pliki i katalogi, które reprezentują hello zestawów danych, które mają wartość tooothers w sieci organizacja.</span><span class="sxs-lookup"><span data-stu-id="06117-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="06117-130">Rejestrowanie wszystkich plików i katalogów można zajmowały hello katalogu, dzięki czemu przeszkodę dla użytkowników toofind wymaganych.</span><span class="sxs-lookup"><span data-stu-id="06117-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="06117-131">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="06117-131">Summary</span></span>
<span data-ttu-id="06117-132">Rejestrowanie źródeł danych z **Azure Data Catalog** umożliwiają łatwiejsze toodiscover i zrozumieć.</span><span class="sxs-lookup"><span data-stu-id="06117-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="06117-133">Rejestrowanie i adnotowanie hello danych big data pliki i katalogi, które reprezentują logiczne zestawów danych, można ułatwić użytkownikom znalezienia i użycia potrzebnych im źródeł danych big data hello.</span><span class="sxs-lookup"><span data-stu-id="06117-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
