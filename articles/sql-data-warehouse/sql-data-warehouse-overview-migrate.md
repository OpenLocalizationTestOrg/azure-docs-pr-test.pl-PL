---
title: "aaaMigrate tooSQL Twojego rozwiązania magazynu danych | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące migracji za platformy SQL Data Warehouse tooAzure rozwiązania."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Migrowanie tooAzure Twojego rozwiązania magazynu danych SQL
Zobacz, na czym polega migracji istniejącej tooAzure rozwiązania bazy danych SQL Data Warehouse. 

## <a name="profile-your-workload"></a>Profilu obciążenia
Przed migracją, która ma toobe pewność, że usługa SQL Data Warehouse jest hello odpowiednie rozwiązanie dla obciążenia. Magazyn danych SQL to Rozproszony system przeznaczony analytics tooperform na dużej ilości danych.  Migrowanie tooSQL magazyn danych wymaga pewnych zmian projektowych, które nie są zbyt twardych toounderstand, ale może potrwać kilka tooimplement czas. Firmy wymaga hurtowni danych klasy korporacyjnej, korzyści hello są warto hello wysiłku. Jednak jeśli nie potrzebujesz zasilania hello usługi SQL Data Warehouse, to bardziej ekonomiczne toouse serwera SQL lub bazy danych SQL Azure.

Należy rozważyć użycie usługi SQL Data Warehouse przy możesz:
- Ma co najmniej jeden terabajtów danych
- Plan toorun analizy dużych ilości danych
- Należy hello możliwości tooscale obliczeniowej i pamięci masowej 
- Chcę koszty toosave wstrzymując zasoby obliczeniowe, gdy nie są potrzebne.

Magazyn danych SQL nie jest używany do operacyjnej obciążenia (OLTP), które mają:
- Wysoka częstotliwość odczyty i zapisy
- Wybiera dużą liczbę pojedynczych
- Dużej ilości wstawia pojedynczy wiersz
- Wiersz po wierszu przetwarzania potrzeb
- Niezgodnych formatach (JSON, XML)


## <a name="plan-hello-migration"></a>Planowanie migracji hello

Po określeniu toomigrate tooSQL istniejącego rozwiązania magazynu danych, jest ważne tooplan hello migracji przed rozpoczęciem pracy. 

Jeden cel planowania jest tooensure dane z schematy tabeli i kodu są zgodne z usługą Magazyn danych SQL. Brak niektórych zgodności różnice toowork wokół między bieżącego systemu i SQL Data Warehouse. Ponadto Migrowanie dużych ilości danych tooAzure wymaga czasu. Należy dokładnie zaplanować przyspiesza pobieranie tooAzure Twojego danych. 

Innym celem planowania jest projekt toomake tooensure dostosowań, które rozwiązanie korzysta z hello wysoką wydajność zapytań SQL Data Warehouse jest zaprojektowany tooprovide. Projektowania magazynów danych do skalowania wprowadza wzorce projektowania i dlatego tradycyjnych metod nie są zawsze hello najlepiej. Mimo że pewnych zmian projektu mogą być wykonywane po migracji, wcześniej wprowadzania zmian w procesie hello zapisze późniejszym czasie.

tooperform udanej migracji, należy toomigrate Twojego schematy tabeli, kodu i danych. Aby uzyskać wskazówki dotyczące tych tematów migracji zobacz:

-  [Migracja z schematów](sql-data-warehouse-migrate-schema.md)
-  [Migrowanie kodu](sql-data-warehouse-migrate-code.md)
-  [Migrowanie danych](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Następne kroki
Hello CAT (zespół doradczy klientów) ma także niektóre dużą wskazówek magazyn danych SQL, które publikują one za pośrednictwem blogów.  Spójrz na ich artykułu [migrowanie danych tooAzure SQL Data Warehouse w praktyce] [ Migrating data tooAzure SQL Data Warehouse in practice] dodatkowe wskazówki dotyczące migracji.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
