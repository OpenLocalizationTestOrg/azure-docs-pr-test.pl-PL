---
title: "Usługa Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat warstwy usługi dla pojedynczej i baz danych puli zapewnienie poziomy wydajności i rozmiaru magazynu."
keywords: 
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Active
ms.date: 08/20/2017
ms.author: carlrab
ms.openlocfilehash: 55f59fddee008eb42b7252d6368a56873a6abd16
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2017
---
# <a name="what-are-azure-sql-database-service-tiers"></a>Co to są warstwach usług bazy danych SQL Azure

[Baza danych SQL Azure](sql-database-technical-overview.md) oferuje **podstawowe**, **standardowe**, **Premium**, i **Premium RS** warstw dla obu usług[baz danych z jednym](sql-database-single-database-resources.md) i [pule elastyczne](sql-database-elastic-pool.md). Warstwy usług są zróżnicowane głównie przez zakres poziom wydajności i opcje rozmiaru magazynu i cenę.  Wszystkie warstwy usług zapewniają elastyczność w Zmiana wydajności poziom i rozmiaru magazynu.  Pojedyncze bazy danych i pul elastycznych są rozliczane co godzinę na podstawie warstwy usług, poziom wydajności i rozmiar magazynu.   

## <a name="choosing-a-service-tier"></a>Wybieranie warstwy usług

Wybór warstwy usług zależy przede wszystkim ciągłość prowadzenia działalności biznesowej, magazynu i wymagania dotyczące wydajności.
| | **Podstawowa** | **Standardowa** |**Premium** |**R — wersja Premium** |
| :-- | --: |--:| --:| --:| 
|Obciążenie docelowego|Projektowanie i produkcji|Projektowanie i produkcji|Projektowanie i produkcji|Obciążenie może tolerować utraty danych maksymalnie 5-minut z powodu błędów usługi|
|Umowa SLA dotycząca czasu dostępności|99,99%|99,99%|99,99%|N/d znajduje się w wersji zapoznawczej|
|Przechowywanie kopii zapasowych|7 dni|35 dni|35 dni|35 dni|
|Procesor CPU|Niska|Niski, Średni, wysoki|Średni i wysoki|Medium|
|Wydajność We/Wy|Niska  | Medium | Rzędu wyższy niż standardowy|Identyczny — wersja Premium|
|Czas oczekiwania na We/Wy|Wyższa niż — wersja Premium|Wyższa niż — wersja Premium|Niższe niż Basic i Standard|Identyczny — wersja Premium|
|Indeksowanie magazynu kolumn i OLTP w pamięci|Nie dotyczy|Nie dotyczy|Obsługiwane|Obsługiwane|
|||||

## <a name="performance-level-and-storage-size-limits"></a>Poziom wydajności i magazynu limity rozmiaru

Poziomy wydajności są wyrażane pod względem jednostki transakcji bazy danych (Dtu) dla pojedynczej bazy danych i jednostek transakcji elastycznej bazy danych (Edtu) dla puli elastycznej. Aby uzyskać więcej informacji na temat jednostek Dtu a Edtu, zobacz [co to są Dtu a Edtu?](sql-database-what-is-a-dtu.md).

### <a name="single-databases"></a>Pojedyncze bazy danych

|  | **Podstawowa** | **Standardowa** | **Premium** | **R — wersja Premium**|
| :-- | --: | --: | --: | --: |
| Maksymalny rozmiar * | 2 GB | 1 TB | 4 TB  | 1 TB  |
| Maksymalna Dtu | 5 | 3000 | 4000 | 1000 |
||||||

### <a name="elastic-pools"></a>Pule elastyczne

| | **Podstawowa** | **Standardowa** | **Premium** | **R — wersja Premium**|
| :-- | --: | --: | --: | --: |
| Maksymalny rozmiar magazynu na bazie danych *  | 2 GB | 1 TB | 1 TB | 1 TB |
| Maksymalny rozmiar magazynu na puli * | 156 GB | 4 TB | 4 TB | 1 TB |
| Maksymalna liczba jednostek Edtu na bazę danych | 5 | 3000 | 4000 | 1000 |
| Maksymalna liczba jednostek Edtu na pulę | 1600 | 3000 | 4000 | 1000 |
| Maksymalna liczba baz danych dla każdej puli | 500  | 500 | 100 | 100 |
||||||

> [!IMPORTANT]
> \* Magazyn o rozmiarze większym niż ilość miejsca do magazynowania są dostępne w wersji zapoznawczej dodatkowych kosztów za dodatkową opłatą. Szczegóły można znaleźć w [cenniku usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database/). 
>
> \* W warstwie Premium magazyn o rozmiarze ponad 1 TB jest obecnie dostępny w następujących regionach: Wschodnie stany USA 2, Zachodnie stany USA, Administracja USA — Wirginia, Europa Zachodnia, Niemcy Środkowe, Azja Południowo-Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada Środkowa i Kanada Wschodnia. Więcej informacji można znaleźć na stronie [bieżących ograniczeń poziomów P11–P15](sql-database-resource-limits.md#single-database-limitations-of-p11-and-p15-when-the-maximum-size-greater-than-1-tb).  
> 

Aby uzyskać więcej informacji o określonych poziomów wydajności i dostępnych wyborów rozmiar magazynu, zobacz [limity zasobów bazy danych SQL](sql-database-resource-limits.md).


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [pojedyncze bazy danych zasobów](sql-database-single-database-resources.md).
- Dowiedz się więcej o pule elastyczne, zobacz [pule elastyczne](sql-database-elastic-pool.md).
- Dowiedz się więcej o [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md)
* Dowiedz się więcej o [Dtu a Edtu](sql-database-what-is-a-dtu.md).
* Więcej informacji na temat monitorowania użycie jednostek DTU, zobacz [monitorowania i dostrajania wydajności](sql-database-troubleshoot-performance.md).

