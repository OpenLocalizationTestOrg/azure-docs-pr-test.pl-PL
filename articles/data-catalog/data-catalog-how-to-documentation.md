---
title: "Jak dokumentować źródła danych | Dokumentacja firmy Microsoft"
description: "Artykule wyróżnianie jak dokumentować zasobów danych w wykazie danych Azure."
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="55213-103">Dokumentowanie źródeł danych</span><span class="sxs-lookup"><span data-stu-id="55213-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="55213-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="55213-104">Introduction</span></span>
<span data-ttu-id="55213-105">**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="55213-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="55213-106">Innymi słowy **Azure Data Catalog** wszystkim chodzi o pomoc osób odnajdywania, *zrozumieć*i używać źródeł danych i który pomaga organizacjom osiąganie większych zysków z ich istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="55213-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="55213-107">Jeśli źródło danych jest zarejestrowana w usłudze **Azure Data Catalog**, jego metadanych jest kopiowany i indeksowania przez usługę, ale wątku nie zakończyć.</span><span class="sxs-lookup"><span data-stu-id="55213-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="55213-108">**Wykaz danych Azure** pozwala użytkownikom na ich własnych pełną dokumentację opisujące użycia i typowe scenariusze dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="55213-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="55213-109">W [jak dodawać adnotacje do źródeł danych](data-catalog-how-to-annotate.md), możesz dowiedzieć się, że ekspertów znających źródła danych może dodawać adnotacje do go z tagami i opis.</span><span class="sxs-lookup"><span data-stu-id="55213-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="55213-110">**Azure Data Catalog** portal zawiera edytor tekstu sformatowanego, dzięki czemu użytkownicy mogą pełni dokumentu zasobów danych i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="55213-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="55213-111">Edytor obejmuje formatowanie akapitów, takich jak nagłówki, formatowania tekstu, listy punktowane, numerowane i tabele.</span><span class="sxs-lookup"><span data-stu-id="55213-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="55213-112">Znaczniki i opisy są bardzo proste adnotacji.</span><span class="sxs-lookup"><span data-stu-id="55213-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="55213-113">Jednak aby konsumenci danych lepiej zrozumieć użycie źródła danych i scenariuszy biznesowych dla źródła danych, eksperta zapewniają pełne, szczegółowe dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="55213-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="55213-114">To proste dokumentować źródła danych.</span><span class="sxs-lookup"><span data-stu-id="55213-114">It's easy to document a data source.</span></span> <span data-ttu-id="55213-115">Wybierz kontener lub zasobów danych, a następnie wybierz pozycję **dokumentacji**.</span><span class="sxs-lookup"><span data-stu-id="55213-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="55213-116">Dokumentowanie zasobów danych</span><span class="sxs-lookup"><span data-stu-id="55213-116">Documenting data assets</span></span>
<span data-ttu-id="55213-117">Zaletą **Azure Data Catalog** dokumentacji umożliwia użycie wykazu danych jako repozytorium zawartości można utworzyć pełną udostępniono elementów zawartości danych.</span><span class="sxs-lookup"><span data-stu-id="55213-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="55213-118">Można sprawdzić szczegółowe zawierającego opis kontenery i tabele.</span><span class="sxs-lookup"><span data-stu-id="55213-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="55213-119">Jeśli masz już zawartości w innej repozytorium zawartości, takich jak SharePoint lub udziału plików, można dodać łącza dokumentacji zasobów do odwołania do tego istniejącej zawartości.</span><span class="sxs-lookup"><span data-stu-id="55213-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="55213-120">Ta funkcja umożliwia istniejące dokumenty mogą szybciej odnajdywać.</span><span class="sxs-lookup"><span data-stu-id="55213-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="55213-121">Dokumentacja nie jest uwzględniony w indeksie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="55213-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="55213-122">Poziom dokumentacji mogą należeć do zakresu od opisu właściwości i wartość kontener zasobów danych, aby uzyskać szczegółowy opis schemat tabeli w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="55213-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="55213-123">Poziomu z dokumentacją dostarczoną powinien być regulowane przez potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55213-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="55213-124">Jednak ogólnie rzecz biorąc, poniżej przedstawiono kilka zalet i wad dokumentowanie zasobów danych:</span><span class="sxs-lookup"><span data-stu-id="55213-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="55213-125">Tylko kontenerem dokumentów: cała zawartość znajduje się w jednym miejscu, ale może być brak niezbędne informacje dla użytkowników podjąć świadomej decyzji.</span><span class="sxs-lookup"><span data-stu-id="55213-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="55213-126">Dokument tylko tabele: zawartość jest specyficzne dla tego obiektu, ale użytkownicy korzystają z wielu miejscach dokumentów.</span><span class="sxs-lookup"><span data-stu-id="55213-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="55213-127">Kontenery i tabele dokumentów: najbardziej kompleksowe rozwiązanie, ale może powodować więcej obsługi dokumentów.</span><span class="sxs-lookup"><span data-stu-id="55213-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="55213-128">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="55213-128">Summary</span></span>
<span data-ttu-id="55213-129">Dokumentowanie źródeł danych za pomocą **Azure Data Catalog** można utworzyć udostępniono o danych w stopniu szczegółowości.</span><span class="sxs-lookup"><span data-stu-id="55213-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="55213-130">Przy użyciu łącza, można połączyć się z zawartością przechowywaną w istniejących repozytorium zawartości, które połączono z istniejących dokumentów i zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="55213-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="55213-131">Gdy użytkownicy odnajdywania zasobów danych, mogą oni mieć kompletny zestaw dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="55213-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
