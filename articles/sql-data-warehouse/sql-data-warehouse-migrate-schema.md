---
title: aaaMigrate Twojego tooSQL schematu magazynu danych | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące migrowania tooAzure Twojego schematu SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Migracja z tooSQL schematów magazynu danych
Wskazówki dotyczące migrowania tooSQL schematy programu SQL Data Warehouse. 

## <a name="plan-your-schema-migration"></a>Planowanie migracji do schematu

Podczas planowania migracji, zobacz hello [omówienie tabeli] [ table overview] toobecome zapoznać się z tabeli projektowania, takich jak statystyka, dystrybucja, partycjonowanie i indeksowania.  Przedstawiono także niektóre [nieobsługiwane funkcje tabeli] [ unsupported table features] i ich obejścia.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Użyj bazy danych tooconsolidate schematy zdefiniowane przez użytkownika

Obciążenie istniejących prawdopodobnie ma więcej niż jednej bazy danych. Na przykład magazynu danych programu SQL Server może obejmować tymczasowej bazy danych, bazy danych magazynu danych i niektóre bazy danych składnicy danych. W tej topologii każda baza danych jest uruchamiany jako oddzielny obciążenia przy użyciu zasad zabezpieczeń.

Z kolei SQL Data Warehouse uruchamia obciążeniu magazynu danych całego hello w ramach jednej bazy danych. Sprzężenia między bazy danych nie są dozwolone. W związku z tym usługi SQL Data Warehouse oczekuje, że wszystkie tabele używane przez toobe magazynu danych hello przechowywane w hello jedną bazę danych.

Firma Microsoft zaleca używanie tooconsolidate użytkownika schematy istniejące obciążenia na jedną bazę danych. Przykłady można znaleźć [schematy zdefiniowane przez użytkownika](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Użyj kompatybilne typy danych
Modyfikowanie użytkownika toobe typy danych zgodne z usługą Magazyn danych SQL. Dla listy typów obsługiwanych i nieobsługiwanych danych, zobacz [typy danych][data types]. Ten temat stanowi obejścia hello nieobsługiwane typy. Udostępnia również zapytania tooidentify istniejących typów, które nie są obsługiwane w usłudze SQL Data Warehouse.

## <a name="minimize-row-size"></a>Minimalizuj rozmiar wiersza
Aby uzyskać najlepszą wydajność zminimalizować hello długość wiersza równą tabel. Ponieważ krótszą długości wiersza prowadzić toobetter wydajności, należy użyć hello najmniejszą typów danych, które działają danych. 

Szerokość wiersza tabeli PolyBase ma limit 1 MB.  Jeśli planujesz tooload danych do usługi SQL Data Warehouse przy użyciu programu PolyBase, zaktualizuj tabele toohave wiersza maksymalnej szerokości mniej niż 1 MB. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Wybierz opcję dystrybucji hello
Usługa SQL Data Warehouse to system rozproszoną bazę danych. Każda tabela jest dystrybuowane lub replikowane w węzłach obliczeniowych hello. Brak opcji tabeli, która pozwala określić, jak toodistribute hello danych. Wybór Hello jest działanie okrężne, replikowane, albo rozproszone wyznaczania wartości skrótu. Każdy ma zalet i wad. Jeśli nie określisz opcję dystrybucji hello SQL Data Warehouse użyje okrężnego jako domyślny hello.

- Działanie okrężne jest domyślnym hello. Jest najprostsza toouse hello i ładuje hello dane tak szybko, jak to możliwe, ale sprzęga wymaga przenoszenia danych, co zmniejsza szybkość działania zapytania.
- Zreplikowane magazyny kopii tabeli hello w każdym węźle obliczeń. Zreplikowane tabele są wydajność, ponieważ nie wymaga przenoszenia danych do sprzęgania i agregacji. One wymagają dodatkowe miejsce do magazynowania, a w związku z tym najlepiej dla mniejszych tabel.
- Skrót rozproszonych dystrybuuje wiersze hello we wszystkich węzłach hello za pomocą funkcji skrótu. Tabele hash rozproszone są hello Puls usługi SQL Data Warehouse, ponieważ są one zaprojektowane tooprovide wysoką wydajność zapytań na dużych tabel. Ta opcja wymaga niektórych planowania tooselect hello najlepsze kolumny o danych hello toodistribute. Jednak jeśli nie wybierzesz hello najlepsze hello kolumny po raz pierwszy, można łatwo ponownie dystrybuować hello dane na inną kolumnę. 

Zobacz toochoose hello najlepszych opcji dystrybucji dla każdej tabeli [rozproszonych tabel](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Następne kroki
Po pomyślnej migracji z tooSQL schematu bazy danych magazynu danych można kontynuować tooone hello następujące artykuły:

* [Migrowanie danych][Migrate your data]
* [Migrowanie kodu][Migrate your code]

Aby uzyskać więcej informacji o najlepszych rozwiązaniach SQL Data Warehouse, zobacz hello [najlepsze rozwiązania] [ best practices] artykułu.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
