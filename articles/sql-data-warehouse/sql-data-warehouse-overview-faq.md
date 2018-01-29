---
title: "Magazyn danych Azure SQL — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono się często zadawane pytania dotyczące usługi Azure SQL Data Warehouse z klientów i deweloperów"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>SQL Data Warehouse często zadawane pytania

## <a name="general"></a>Ogólne

Q. Co oferuje magazynu danych SQL dla bezpieczeństwa danych?

A. Magazynu danych SQL oferuje kilka rozwiązań do ochrony danych, takich jak funkcji TDE i inspekcji. Aby uzyskać więcej informacji, zobacz [zabezpieczeń].

Q. Gdzie mogę znaleźć się, jakie normy prawnych lub biznesowych jest SQL magazynu danych zgodne z?

A. Odwiedź stronę [Compliance Microsoft] strony dla różnych ofert zgodności przez produktów, takich jak SOC i ISO. Najpierw wybierz przez tytuł zgodności, a następnie rozwiń węzeł Azure w sekcji firmy Microsoft w zakresie chmury usług w prawej strony, aby sprawdzić, jakie usługi są Azure usługi są zgodne.

Q. Czy można połączyć usługi Power BI?

A. Tak! Chociaż usługa Power BI obsługuje zapytania bezpośredniego z magazynu danych SQL, nie jest przeznaczony dla dużej liczby użytkowników lub danych w czasie rzeczywistym. Do użytku produkcyjnego usługi Power BI zaleca się przy użyciu usługi Power BI na górze usług Azure Analysis Services lub analizy usługi IaaS. 

Q. Jakie są limity pojemności magazynu danych SQL?

A. Zobacz nasze bieżące [limity pojemności] strony. 

Q. Dlaczego moja skali/wstrzymanie/wznowienie trwa tak długo?

A. Różne czynniki mogą mieć wpływ czasu dla operacji zarządzania obliczeń. Typowy przypadek długotrwałe operacje jest transakcyjna wycofywania. Po zainicjowaniu operacji skalowania lub Wstrzymaj wszystkie sesje przychodzące są blokowane, a zostały opróżnione zapytania. Aby opuścić system stabilna, transakcje muszą wycofana, przed rozpoczęciem operacji. Większa liczba i większa rozmiaru dziennika transakcji, zostanie zablokowany im dłuższy operacji przywracania systemu do stabilności.

## <a name="user-support"></a>Obsługa użytkowników

Q. Mam zgłoszenie dotyczące funkcji, gdzie jest przesyłanie?

A. Jeśli żądanie funkcji, Prześlij go na naszych [UserVoice] strony

Q. Jak mogę przeprowadzić x?

A. Aby uzyskać pomoc w tworzeniu z usługą Magazyn danych SQL, można zadawać pytania na naszych [przepełnienie stosu] strony. 

Q. Jak przesłać biletu pomocy technicznej

A. [Bilety obsługi] można złożyć za pośrednictwem portalu Azure.

## <a name="sql-languagefeature-support"></a>Obsługa języka/funkcja SQL 

Q. Jakie typy danych obsługuje magazyn danych SQL?

A. Zobacz SQL Data Warehouse [typy danych].

Q. Jakie funkcje tabeli są obsługiwane?

A. Podczas gdy magazyn danych SQL obsługuje wiele funkcji, niektóre nie są obsługiwane i są udokumentowane w artykule [nieobsługiwanych funkcji tabeli].

## <a name="tooling-and-administration"></a>Narzędzia i administracji

Q. Obsługuje projektów bazy danych w programie Visual Studio.

A. Obecnie nie obsługujemy projektów baz danych w programie Visual Studio dla usługi SQL Data Warehouse. Jeśli chcesz oddanych głosów można pobrać tej funkcji, można znaleźć w naszych User Voice [projektów bazy danych funkcji żądania].

Q. Magazyn danych SQL obsługuje interfejsy API REST?

A. Tak. Większość funkcji REST, które mogą być używane z bazą danych SQL jest również dostępna w programie SQL Data Warehouse. Możesz znaleźć informacji interfejsu API REST stron z dokumentacją lub [MSDN].


## <a name="loading"></a>Ładowanie

Q. Jakie sterowniki klienta są obsługiwane?

A. Obsługa sterowników dla magazynu danych można znaleźć w [parametry połączenia] strony

Pytanie: jakie formaty plików są obsługiwane przez aparat PolyBase z magazynu danych SQL?

Odpowiedź: Orc, RC Parquet i płaskiej tekstu rozdzielanego

Pytanie: jakie mogą I łączyć się z magazynu danych SQL przy użyciu programu PolyBase? 

Odpowiedź: [usługi Azure Data Lake Store] i [obiektów blob magazynu Azure]

Pytanie: jest przekazywanie obliczeń możliwe podczas nawiązywania połączenia obiektach blob magazynu Azure lub ADLS? 

Odpowiedź: nie PolyBase magazynu danych SQL interakcja składników magazynu. 

Pytanie: czy można podłączyć do HDI?

Odpowiedź: HDI służy ADLS lub WASB warstwy systemu plików HDFS. Jeśli masz jako warstwa systemu plików HDFS można załadować danych do magazynu danych SQL. Jednak nie można wygenerować obliczeń przekazywanie do wystąpienia HDI. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na magazyn danych SQL jako całość, zobacz nasze [omówienie] strony.


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[parametry połączenia]: ./sql-data-warehouse-connection-strings.md
[przepełnienie stosu]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Bilety obsługi]: ./sql-data-warehouse-get-started-create-support-ticket.md
[zabezpieczeń]: ./sql-data-warehouse-overview-manage-security.md
[Compliance Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[limity pojemności]: ./sql-data-warehouse-service-capacity-limits.md
[typy danych]: ./sql-data-warehouse-tables-data-types.md
[nieobsługiwanych funkcji tabeli]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[usługi Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[obiektów blob magazynu Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[projektów bazy danych funkcji żądania]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[omówienie]: ./sql-data-warehouse-overview-faq.md