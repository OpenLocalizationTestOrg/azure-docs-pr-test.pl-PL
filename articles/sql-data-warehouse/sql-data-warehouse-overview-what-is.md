---
title: Co to jest Azure SQL Data Warehouse? | Microsoft Docs
description: "Rozproszona baza danych klasy korporacyjnej, która może przetwarzać woluminy zawierające petabajty danych relacyjnych i nierelacyjnych. Jest to pierwszy magazyn danych w chmurze w branży, którym umożliwia powiększanie, zmniejszanie i wstrzymanie w ciągu kilku sekund."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jenniehubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 10/23/2017
ms.author: jrj
ms.openlocfilehash: 7fd17c29c413905084c6b3736018d111d3b28fea
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Co to jest Azure SQL Data Warehouse?

Usługa SQL Data Warehouse to oparty na chmurze magazyn danych przedsiębiorstwa (EDW), który wykorzystuje architekturę MPP (Massively Parallel Processing) do szybkiego uruchamiania złożonych zapytań obejmujących petabajty danych. Użyj usługi SQL Data Warehouse jako głównego składnika rozwiązania danych big data. Zaimportuj dane big data do usługi SQL Data Warehouse za pomocą prostych zapytań PolyBase T-SQL, a następnie użyj zaawansowanych funkcji architektury MPP do uruchomienia analityki wysokiej wydajności. Podczas integracji i analizy hurtownia danych stanie się pojedynczym źródłem danych, na którym Twoja firma może polegać przy szukaniu szczegółowych informacji.  


## <a name="key-component-of-big-data-solution"></a>Kluczowy składnik rozwiązania danych big data
Usługa SQL Data Warehouse to kluczowy składnik całościowego rozwiązania danych big data w chmurze.

![Rozwiązanie magazynu danych](media/sql-data-warehouse-overview-what-is/data-warehouse-solution.png) 

W rozwiązaniu danych w chmurze dane są pozyskiwane do magazynów danych big data z różnych źródeł. Platformy Hadoop, Spark i algorytmy uczenia maszynowego przygotowują i przystosowują dane, gdy te już znajdą się w magazynie danych big data. Jeśli dane są gotowe do kompleksowej analizy, usługa SQL Data Warehouse używa programu PolyBase do wykonywania zapytań kierowanych do magazynów danych big data. Program PolyBase używa standardowych zapytań T-SQL do przenoszenia danych do usługi SQL Data Warehouse.
 
Usługa SQL Data Warehouse przechowuje dane w tabelach relacyjnych z magazynem kolumnowym. Ten format znacznie zmniejsza koszty przechowywania danych i poprawia wydajność zapytań. Gdy dane są przechowywane w usłudze SQL Data Warehouse, możesz uruchomić analitykę na dużą skalę. W porównaniu do tradycyjnych systemów bazy danych, zapytania analizy kończą się w ciągu sekund zamiast minut lub godzin zamiast dni. 

Wyniki analizy można odnieść do ogólnoświatowych baz danych raportowania lub aplikacji. Analitycy biznesowi mogą zatem uzyskiwać wyniki analizy w celu świadomego podejmowania decyzji biznesowych.

## <a name="optimization-choices"></a>Opcje optymalizacji

Usługa SQL Data Warehouse oferuje [warstwy wydajności](performance-tiers.md) zaprojektowane pod kątem elastyczności w celu zaspokojenia Twojego zapotrzebowania na dane, czy to dużego, czy to małego. Możesz wybrać magazyn danych, który jest zoptymalizowany pod kątem elastyczności lub obliczeń. 

- **Warstwa wydajności zoptymalizowana pod kątem elastyczności** oddziela warstwy obliczeń i magazynu w architekturze. Ta opcja najlepiej działa dla obciążeń, które mogą w pełni korzystać z rozdzielenia obliczeń i magazynu dzięki częstemu skalowaniu w celu obsługi krótkich okresów szczytowej aktywności. Ta warstwa obliczeń ma najniższą cenę wejściową i możliwość skalowania do obsługi większości obciążeń klientów.

- **Warstwa wydajności zoptymalizowana pod kątem obliczeń** wykorzystuje najnowszy sprzęt platformy Azure do wprowadzania nowej pamięci podręcznej NVMe Solid State Disk, która przechowuje dane, do których najczęściej następuje dostęp, w pobliżu procesorów CPU, co jest dokładnie tym, czego potrzebujesz. Dzięki automatycznemu podziałowi magazynu na warstwy ta warstwa wydajności najlepiej działa dla kompleksowych zapytań, ponieważ wszystkie operacje We/Wy są przechowywane lokalnie względem warstwy obliczeń. Ponadto magazyn kolumn jest rozszerzony w celu przechowywania nieograniczonej ilości danych w usłudze SQL Data Warehouse. Warstwa wydajności zoptymalizowana pod kątem obliczeń zapewnia najwyższy poziom skalowalności, dzięki któremu można skalować do 30 000 jednostek obliczeniowych magazynu danych (cDWU). Wybierz tę warstwę dla obciążeń, które ciągle wymagają niezwykle wysokiej wydajności.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz już podstawową wiedzę na temat usługi SQL Data Warehouse, możesz dowiedzieć się, jak szybko [utworzyć bazę danych w usłudze SQL Data Warehouse][create a SQL Data Warehouse] i [ładowanie danych przykładowych][load sample data]. Jeśli dopiero zaczynasz korzystać z platformy Azure, [słownik platformy Azure][Azure glossary] może pomóc Ci zaznajomić się z nową terminologią. Możesz też zwrócić uwagę na inne zasoby dotyczące usługi SQL Data Warehouse.  

* [Historie sukcesu klientów]
* [Blogi]
* [Żądania funkcji]
* [Filmy wideo]
* [Blogi zespołu doradczego klientów]
* [Tworzenie biletu pomocy technicznej]
* [Forum MSDN]
* [Forum Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Tworzenie biletu pomocy technicznej]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Historie sukcesu klientów]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogi]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogi zespołu doradczego klientów]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Żądania funkcji]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Forum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Filmy wideo]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[Service Level Agreements]: https://azure.microsoft.com/en-us/support/legal/sla/
