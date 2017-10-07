---
title: "przekazywanie aaaData w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooan danych tooupload indeksu w usłudze Azure Search."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Przekazywanie danych tooAzure wyszukiwania
> [!div class="op_single_selector"]
> * [Omówienie](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Istnieją dwa sposoby toopopulate indeksu z danymi. Hello pierwsza opcja polega na ręcznym wypychaniu danych do indeksu hello przy użyciu usługi Azure Search hello [interfejsu API REST](search-import-data-rest-api.md) lub [zestawu .NET SDK](search-import-data-dotnet.md). Druga opcja Hello jest zbyt[punktu obsługiwanego źródła danych](search-indexer-overview.md) tooyour indeksu i zezwolenie usłudze Azure Search na automatyczne ściągnięcie danych hello.

## <a name="push-data-tooan-index"></a>Wypychanie danych tooan indeksu
Ta metoda obejmuje tooprogrammatically wysyłania toomake wyszukiwania tooAzure Twojego danych będzie dostępna do wyszukiwania. W przypadku aplikacji o bardzo niskich opóźnień (na przykład wyszukiwania toobe operacji synchronizacji z dynamicznymi bazami danych zapasów) hello model wypychania jest jedynym rozwiązaniem.

Można użyć hello [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) lub [zestawu .NET SDK](search-import-data-dotnet.md) toopush danych tooan indeksu. Obecnie nie jest narzędzie obsługiwane dla wypychania danych za pośrednictwem portalu hello.

Takie podejście jest bardziej elastyczne niż model ściągania hello, ponieważ możesz przekazywać dokumenty pojedynczo lub w partiach (się too1000 na partię lub 16 MB, niezależnie od limit zostanie osiągnięty jako pierwszy). model wypychania Hello umożliwia także tooupload dokumenty tooAzure wyszukiwania niezależnie od tego, gdzie dane.

format danych Hello zrozumiałe dla usługi Azure Search jest JSON, a wszystkie dokumenty w zestawie danych hello musi zawierać pola, które mapują toofields zdefiniowanej w schemacie Twojego indeksu. 

## <a name="pull-data-into-an-index"></a>Ściąganie danych do indeksu
model ściągania Hello obejmuje przeszukiwanie obsługiwanego źródła danych i automatyczne przekazywanie hello danych do indeksu. W usłudze Azure Search ta możliwość jest zaimplementowana za pomocą *indeksatorów*, które obecnie są dostępne dla usług [Blob Storage](search-howto-indexing-azure-blob-storage.md), [Table Storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer) i [Azure SQL Database oraz programu SQL Server na maszynach wirtualnych platformy Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Indeksatory Połącz indeksu tooa źródła danych (zazwyczaj tabeli, widoku lub równoważnej struktury) i mapowanie źródła pola tooequivalent pól w indeksie hello. W czasie wykonywania hello zestawu wierszy jest automatycznie po przekształceniu tooJSON i ładowane do hello określonego indeksu. Wszystkie indeksatory obsługuje planowania, dzięki czemu można określić, jak często hello dane są odświeżane toobe. Większość indeksatory Podaj śledzenia, jeśli źródło danych hello obsługuje zmian. Śledzenie zmian i usuwa tooexisting dokumentów dodatkowo toorecognizing nowych dokumentów, indeksatory eliminują konieczność hello tooactively zarządzać danymi hello w indeksie. 

Funkcja indeksatora jest widoczna w hello [portalu Azure](search-import-data-portal.md), hello [interfejsu API REST](/rest/api/searchservice/Indexer-operations)i hello [zestawu .NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Portal hello toousing zaletą jest, że usługi Azure Search zwykle wygenerować domyślny schemat indeksu dla Ciebie odczytu hello metadanych zestawu hello źródła danych. Witaj generowania indeksu można modyfikować, dopóki indeks hello jest przetwarzany, po którym hello są tymi, które nie wymagają indeksowanie dozwolone tylko zmiany schematu. Jeśli zmiany hello ma wpływ toomake hello schematu bezpośrednio, będzie potrzebny toorebuild hello indeksu. 

Po hello indeks zostanie wypełnione, można użyć **Eksplorator wyszukiwania** na pasku poleceń portalu hello krokiem weryfikacji.

## <a name="query-an-index-using-search-explorer"></a>Tworzenie zapytań względem indeksu za pomocą Eksploratora wyszukiwania

Szybko tooperform wstępnego wyboru na przekazanie dokumentu hello jest toouse **Eksplorator wyszukiwania** w portalu hello. Program Hello explorer umożliwia tworzenie zapytań względem indeksu bez żadnego kodu toowrite. Witaj wyników wyszukiwania jest na podstawie domyślnych ustawień, takich jak hello [proste składni](/rest/api/searchservice/simple-query-syntax-in-azure-search) i domyślne [parametru zapytania searchMode](/rest/api/searchservice/search-documents). Wyniki są zwracane w formacie JSON, dzięki czemu możesz sprawdzić hello całego dokumentu.

> [!TIP]
> Wiele [przykłady kodu usługi Azure Search](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) obejmują osadzonego lub łatwo dostępne zestawy danych, oferty tooget łatwy sposób pracy. Hello portal także przykładowe indeksatora i źródła danych składający się z zestawu danych nieruchomości małej (o nazwie "współużytkowania us test"). Po uruchomieniu indeksatora wstępnie skonfigurowane hello na źródła danych przykładowych hello indeksu jest tworzony i załadowane z dokumentami, które następnie można wyszukiwać w Eksploratorze wyszukiwania lub przez kod, który można zapisać.
