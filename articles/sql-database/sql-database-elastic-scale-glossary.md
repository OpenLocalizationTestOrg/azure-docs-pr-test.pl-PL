---
title: "Słownik Narzędzia bazy danych aaaElastic | Dokumentacja firmy Microsoft"
description: "Wyjaśnienie pojęcia dotyczące narzędzi elastycznej bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Elastyczne słownik Narzędzia bazy danych
Witaj poniższe terminy są definiowane dla hello [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md), funkcja bazy danych SQL Azure. Hello narzędzia są używane toomanage [mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md)i zawierają hello [biblioteki klienta](sql-database-elastic-database-client-library.md), hello [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md), [pule elastyczne](sql-database-elastic-pool.md), i [zapytania](sql-database-elastic-query-overview.md). 

Te terminy są używane w [Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych](sql-database-elastic-scale-add-a-shard.md) i [przy użyciu hello RecoveryManager klasy toofix niezależnego fragmentu mapy problemów](sql-database-elastic-database-recovery-manager.md).

![Elastyczne warunki skali][1]

**Baza danych**: baza danych SQL Azure. 

**Routing zależnych danych**: hello funkcje umożliwiające aplikacji niezależnego fragmentu tooa tooconnect danego klucza określonego dzielenia na fragmenty. Zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md). Porównywanie za**[zapytania wielu niezależnych](sql-database-elastic-scale-multishard-querying.md)**.

**Globalny identyfikator niezależnego fragmentu mapy**: mapy hello między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów w **zestaw niezależnych**. mapy globalne niezależnych Hello są przechowywane w hello **menedżera map niezależnego fragmentu**. Porównywanie za**mapy lokalnego niezależnych**.

**Lista niezależnych mapy**: mapy niezależnego fragmentu, w których dzielenia na fragmenty klucze są mapowane pojedynczo. Porównywanie za**mapy niezależnego fragmentu zakresu**.   

**Mapa lokalnych niezależnych**: przechowywane na niezależnego fragmentu, mapy niezależnych lokalne powitania zawiera mapowania dla shardlets hello, znajdującej się na powitania niezależnego fragmentu.

**Wiele niezależnych zapytania**: hello tooissue możliwości zapytanie wielu odłamków; zestawy wyników są zwracane, używając semantyki UNION ALL (znanej także jako "rozdysponowywania zapytania"). Porównywanie za**danych zależnych routingu**.

**Wielodostępne** i **pojedynczej dzierżawy**: Pokazuje dzierżawy pojedynczej bazy danych i bazy danych wielu dzierżawców:

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Oto reprezentację **podzielonej** jednym i wieloma dzierżawcami baz danych. 

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Zakres niezależnych mapy**: mapy niezależnego fragmentu, w których hello strategii dystrybucji niezależnego fragmentu opiera się na różnych zakresów wartości ciągłe. 

**Tabele odwołań dla**: tabel, które nie są podzielonej, ale są replikowane między fragmentów. Na przykład kodów pocztowych mogą być przechowywane w tabeli odniesienia. 

**Identyfikator niezależnego fragmentu**: bazy danych SQL Azure, która przechowuje dane z zestawu danych podzielonej. 

**Elastyczność niezależnego fragmentu**: hello możliwości tooperform zarówno **skalowanie w poziomie** i **skalowanie w pionie**.

**Tabele podzielonej**: tabele, które są podzielonej, tj., których danych jest rozłożona odłamków na podstawie ich wartości klucza dzielenia na fragmenty. 

**Klucz dzielenia na fragmenty**: wartość kolumny, która określa, jak dane są przesyłane między fragmentów. Witaj typ wartości może być jedną z następujących hello: **int**, **bigint**, **varbinary**, lub **uniqueidentifier**. 

**Zestaw niezależnych**: hello kolekcji fragmentów, które są oparte na atrybutach toohello tej samej mapy niezależnego fragmentu w Menedżerze mapy niezależnego fragmentu hello.  

**Shardlet**: wszystkie dane hello skojarzone z pojedynczą wartość klucz w niezależnych dzielenia na fragmenty. Shardlet jest hello najmniejsza możliwa przenoszenie danych do rozpowszechniania podzielonej tabel. 

**Mapa niezależnego fragmentu**: hello zestaw mapowań między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów.

**Menedżer mapy niezależnego fragmentu**: Zarządzanie obiektu i danych sklepu, która zawiera poprzedzających hello niezależnego fragmentu map, niezależnych lokalizacji i mapowania dla jednego lub więcej zestawów niezależnego fragmentu.

![Mapowania][2]

## <a name="verbs"></a>Zlecenia
**Skalowanie w poziomie**: hello polega na skalowanie w poziomie (lub w) kolekcja odłamków przez dodanie lub usunięcie fragmentów tooa niezależnego fragmentu mapy, jak pokazano poniżej.

![Skalowanie w poziomie i w pionie][3]

**Scal**: hello act przenoszenie shardlets z dwóch odłamków tooone niezależnych i odpowiednio aktualizacji hello niezależnego fragmentu mapy.

**Przenieś Shardlet**: hello act przenoszenia niezależnych różnych tooa shardlet pojedynczego. 

**Identyfikator niezależnego fragmentu**: hello polega na poziomie partycjonowania identycznie strukturalnych danych między wieloma bazami danych oparte na kluczu dzielenia na fragmenty.

**Podziel**: hello act przenoszenia shardlets kilka z niezależnych (zazwyczaj jest to nowy) tooanother jednego niezależnego fragmentu. Klucz dzielenia na fragmenty są dostarczane przez użytkownika hello, jak hello podzielić punktu.

**Skalowanie w pionie**: hello polega na skalowanie w górę (lub w dół) hello poziomu wydajności poszczególnych niezależnego fragmentu. Na przykład zmiana niezależnych od standardowego tooPremium, (co powoduje więcej zasobów obliczeniowych). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

