---
title: "źródła danych toodocument aaaHow | Dokumentacja firmy Microsoft"
description: "Wyróżnianie jak tooarticle jak toodocument zasobów danych w wykazie danych Azure."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="acf1a-103">Dokumentowanie źródeł danych</span><span class="sxs-lookup"><span data-stu-id="acf1a-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="acf1a-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="acf1a-104">Introduction</span></span>
<span data-ttu-id="acf1a-105">**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="acf1a-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="acf1a-106">Innymi słowy **Azure Data Catalog** wszystkim chodzi o pomoc osób odnajdywania, *zrozumieć*, używać źródeł danych i pomaga organizacjom tooget więcej wartości z ich istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="acf1a-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="acf1a-107">Jeśli źródło danych jest zarejestrowana w usłudze **Azure Data Catalog**, jego metadanych jest kopiowany i indeksowane przez usługę hello, ale hello wątku nie istnieje zakończyć.</span><span class="sxs-lookup"><span data-stu-id="acf1a-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="acf1a-108">**Wykaz danych Azure** umożliwia również użytkownikom tooprovide własnych pełną dokumentację opisujące hello użycia i typowe scenariusze dla źródła danych hello.</span><span class="sxs-lookup"><span data-stu-id="acf1a-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="acf1a-109">W [jak źródeł danych tooannotate](data-catalog-how-to-annotate.md), możesz dowiedzieć się, że ekspertów znających hello źródła danych może dodawać adnotacje do go z tagami i opis.</span><span class="sxs-lookup"><span data-stu-id="acf1a-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="acf1a-110">Witaj **Azure Data Catalog** portal zawiera edytor tekstu sformatowanego, dzięki czemu użytkownicy mogą pełni dokumentu zasobów danych i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="acf1a-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="acf1a-111">Edytor Hello obejmuje formatowanie, takich jak nagłówki, formatowania listy punktowane, numerowane i tabele tekstu akapitu.</span><span class="sxs-lookup"><span data-stu-id="acf1a-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="acf1a-112">Znaczniki i opisy są bardzo proste adnotacji.</span><span class="sxs-lookup"><span data-stu-id="acf1a-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="acf1a-113">Konsumenci danych toohelp lepiej zrozumieć użycie hello źródła danych i scenariuszy biznesowych dla źródła danych, ekspertów zapewniają pełne, szczegółowe dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="acf1a-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="acf1a-114">Jest łatwy toodocument źródła danych.</span><span class="sxs-lookup"><span data-stu-id="acf1a-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="acf1a-115">Wybierz kontener lub zasobów danych, a następnie wybierz pozycję **dokumentacji**.</span><span class="sxs-lookup"><span data-stu-id="acf1a-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="acf1a-116">Dokumentowanie zasobów danych</span><span class="sxs-lookup"><span data-stu-id="acf1a-116">Documenting data assets</span></span>
<span data-ttu-id="acf1a-117">Witaj zaletą **Azure Data Catalog** dokumentacji umożliwia toouse danych katalogu jako toocreate repozytorium zawartości pełną udostępniono elementów zawartości danych.</span><span class="sxs-lookup"><span data-stu-id="acf1a-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="acf1a-118">Można sprawdzić szczegółowe zawierającego opis kontenery i tabele.</span><span class="sxs-lookup"><span data-stu-id="acf1a-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="acf1a-119">Jeśli masz już zawartości w innej repozytorium zawartości, takich jak SharePoint lub udziału plików, można dodać toohello zasobów dokumentacji łącza tooreference tego istniejącej zawartości.</span><span class="sxs-lookup"><span data-stu-id="acf1a-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="acf1a-120">Ta funkcja umożliwia istniejące dokumenty mogą szybciej odnajdywać.</span><span class="sxs-lookup"><span data-stu-id="acf1a-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="acf1a-121">Dokumentacja nie jest uwzględniony w indeksie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="acf1a-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="acf1a-122">Witaj poziom dokumentacji mogą należeć do zakresu od opisujące hello właściwości i wartości danych zasobów kontenera tooa szczegółowy opis schemat tabeli w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="acf1a-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="acf1a-123">poziom Hello dokumentację powinien uzależniona potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="acf1a-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="acf1a-124">Jednak ogólnie rzecz biorąc, poniżej przedstawiono kilka zalet i wad dokumentowanie zasobów danych:</span><span class="sxs-lookup"><span data-stu-id="acf1a-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="acf1a-125">Tylko kontenerem dokumentów: wszystkie hello zawartość znajduje się w jednym miejscu, ale może być konieczne Brak szczegółów toomake użytkowników podjąć świadomą decyzję.</span><span class="sxs-lookup"><span data-stu-id="acf1a-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="acf1a-126">Dokument tylko tabele hello: zawartości toothat określonego obiektu, ale użytkownicy korzystają z wielu miejscach dokumentów.</span><span class="sxs-lookup"><span data-stu-id="acf1a-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="acf1a-127">Kontenery i tabele dokumentów: najbardziej kompleksowe rozwiązanie, ale może powodować więcej konserwacji hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="acf1a-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="acf1a-128">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="acf1a-128">Summary</span></span>
<span data-ttu-id="acf1a-129">Dokumentowanie źródeł danych za pomocą **Azure Data Catalog** można utworzyć udostępniono o danych w stopniu szczegółowości.</span><span class="sxs-lookup"><span data-stu-id="acf1a-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="acf1a-130">Przy użyciu łącza, możesz połączyć toocontent przechowywane w istniejących repozytorium zawartości, które połączono z istniejących dokumentów i zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="acf1a-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="acf1a-131">Gdy użytkownicy odnajdywania zasobów danych, mogą oni mieć kompletny zestaw dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="acf1a-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
