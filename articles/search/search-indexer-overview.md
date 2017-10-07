---
title: "aaaIndexers w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Przeszukiwania bazy danych Azure SQL, Azure DB rozwiązania Cosmos lub danych z możliwością tooextract magazynu Azure i wypełnienia indeksu usługi Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indeksatory w usłudze Azure Search
> [!div class="op_single_selector"]
>
> * [Omówienie](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md)
> * [Azure Table Storage](search-howto-indexing-azure-tables.md)
>
>

**Indeksatora** w usłudze Azure Search jest przeszukiwarką, która umożliwia wyodrębnianie metadanych i danych z możliwością wyszukiwania z zewnętrznego źródła danych i wypełnienie indeksu na podstawie pola do mapowania między hello indeks i źródło danych. Ta metoda jest czasami tooas określony model ściągania, ponieważ hello usługa pobiera dane w bez konieczności toowrite kodu, który wypycha dane tooan indeksu.

Można korzystać z indeksatora jako jedynego hello oznacza na wprowadzanie danych lub użyj kombinacji metod obejmujących użycie hello indeksatora do załadowania tylko niektórych pól hello w indeksie.

Indeksatory można uruchamiać na żądanie lub według cyklicznego harmonogramu odświeżania danych uruchamianego co 15 minut. Częstsze aktualizacje wymagają modelu wypychania, który pozwala jednocześnie aktualizować dane w usłudze Azure Search i zewnętrznym źródle danych.

## <a name="approaches-for-creating-and-managing-indexers"></a>Podejścia do tworzenia indeksatorów i zarządzania nimi
Tworzenie ogólnie dostępnych indeksatorów, takich jak Azure SQL czy Azure Cosmos DB, i zarządzanie nimi może odbywać się przy użyciu następujących podejść:

* [Portal > Kreator importowania danych ](search-get-started-portal.md)
* [Interfejs API REST usługi](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [Zestaw SDK platformy .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Podstawowe kroki konfiguracji
Indeksatory można udostępniają funkcje, które są unikatowe toohello źródła danych. W związku z tym niektóre aspekty konfiguracji indeksatora lub źródła danych różnią się w zależności od typu indeksatora. Jednak wszystkie indeksatory udostępnianie hello tego samego podstawowego kompozycji i wymagań. Kroki, które są typowe tooall, który indeksatory są przedstawione poniżej.

### <a name="step-1-create-an-index"></a>Krok 1. Tworzenie indeksu
Indeksator będzie zautomatyzować niektóre zadania pokrewne toodata wprowadzanie, ale tworzenia indeksu nie jest jednym z nich. Jako warunek wstępny należy posiadać wstępnie zdefiniowany indeks z polami, które odpowiadają polom w zewnętrznym źródle danych. Aby uzyskać więcej informacji dotyczących tworzenia struktury indeksu, zobacz [Create an Index (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx) (Tworzenie indeksu — interfejs API REST usługi Azure Search).

### <a name="step-2-create-a-data-source"></a>Krok 2. Tworzenie źródła danych
Indeksator pobiera dane ze **źródła danych**, które zawiera na przykład parametry połączenia. Obecnie są obsługiwane następujące źródła danych hello:

* [Usługa Azure SQL Database lub program SQL Server na maszynie wirtualnej platformy Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md), używane tooextract tekstu z plików PDF, dokumentów pakietu Office, HTML lub XML
* [Azure Table Storage](search-howto-indexing-azure-tables.md)

Źródła danych są konfigurowane i zarządzane niezależnie od indeksatorów hello, korzystających z nich, co oznacza, że źródła danych mogą być używane przez wiele indeksatorów tooload więcej niż jednego indeksu w czasie.

### <a name="step-3create-and-schedule-hello-indexer"></a>Krok 3: tworzenie i planowanie hello indeksatora
Definicja indeksatora Hello jest konstrukcję określenie hello indeksu, źródła danych i harmonogram. Indeksator można odwołać źródła danych z innej usługi, pod warunkiem, że źródło danych jest z hello tej samej subskrypcji. Aby uzyskać więcej informacji dotyczących tworzenia struktury indeksatora, zobacz [Create Indexer (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx) (Tworzenie indeksatora — interfejs API REST usługi Azure Search).

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz podstawową koncepcją hello hello następnym krokiem jest tooreview wymagania i typ źródła danych tooeach określonego zadania.

* [Usługa Azure SQL Database lub program SQL Server na maszynie wirtualnej platformy Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md), używane tooextract tekstu z plików PDF, dokumentów pakietu Office, HTML lub XML
* [Azure Table Storage](search-howto-indexing-azure-tables.md)
* [Indeksowanie obiektów blob CSV przy użyciu hello obiektów Blob platformy Azure Search indeksatora](search-howto-index-csv-blobs.md)
* [Indeksowanie obiektów blob plików JSON za pomocą indeksatora obiektów blob usługi Azure Search](search-howto-index-json-blobs.md)
