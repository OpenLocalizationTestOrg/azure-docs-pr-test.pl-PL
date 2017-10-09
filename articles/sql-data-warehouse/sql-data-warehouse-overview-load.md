---
title: "aaaLoad danych do usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello typowe scenariusze dotyczące danych ładowania do usługi SQL Data Warehouse. Obejmują one przy użyciu programu PolyBase, magazynu obiektów blob platformy Azure, plików prostych i wysyłania dysku. Można także użyć narzędzi innych firm."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Ładowanie danych do usługi Azure SQL Data Warehouse
Podsumowanie opcji scenariusz hello i zalecenia dotyczące ładowania danych do usługi SQL Data Warehouse.

Najtrudniejsze części Hello podczas ładowania danych jest zwykle przygotowywania danych hello hello obciążenia. Azure upraszcza ładowania przy użyciu magazynu obiektów blob platformy Azure jako magazynu danych wspólne dla wielu usług hello i przy użyciu fabryki danych Azure hello tooorchestrate przepływu danych i komunikacji między usługami Azure. Te procesy są zintegrowane z technologii PolyBase, która korzysta z ogromną skalę równoległe przetwarzanie danych tooload (MPP) równolegle z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse. 

Samouczki, które ładują przykładowe bazy danych, zobacz [załadować przykładowe bazy danych][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Ładowanie z magazynu obiektów blob platformy Azure
Witaj najszybszy sposób tooimport danych do usługi SQL Data Warehouse jest toouse PolyBase tooload danych z magazynu obiektów blob platformy Azure. PolyBase używa usługi SQL Data Warehouse na ogromną skalę równoległe przetwarzania (MPP) projektu tooload danych równolegle z magazynu obiektów blob platformy Azure. toouse PolyBase, można użyć polecenia T-SQL lub potoku fabryki danych Azure.

### <a name="1-use-polybase-and-t-sql"></a>1. Użyj programu PolyBase i T-SQL
Podsumowanie procesu ładowania:

1. Przeniesienie magazynu obiektów blob tooAzure danych lub w usłudze Azure Data Lake Store i zapisze go w plikach tekstowych.
2. Skonfiguruj obiekty zewnętrznego w lokalizacji hello toodefine SQL Data Warehouse i format danych hello
3. Równolegle danych hello tooload polecenia T-SQL do nowej tabeli bazy danych.

<!-- 5. Schedule and run a loading job. --> 

Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Używanie usługi Azure Data Factory
Dla prostszy sposób toouse PolyBase można utworzyć potok fabryki danych Azure, który używa danych tooload PolyBase z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse. Jest to szybkie tooconfigure, ponieważ nie ma potrzeby toodefine hello T-SQL obiektów. Jeśli potrzebujesz danych zewnętrznych hello tooquery nie jest importowany, użyj T-SQL. 

Podsumowanie procesu ładowania:

1. Przenieś usługi magazynu obiektów blob tooAzure danych i zapisze go w plikach tekstowych. Fabryka danych Azure nie obsługuje obecnie łączności ADLS przy użyciu programu PolyBase).
2. Tworzenie fabryki danych Azure potoku tooingest hello danych. Opcja hello PolyBase.
4. Planowanie i uruchamianie potoku hello.

Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (fabryka danych Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Ładowanie z programu SQL Server
dane tooload z tooSQL programu SQL Server Integration Services (SSIS), można użyć magazynu danych transferu plików prostych lub wysłać tooMicrosoft dysków. Poniżej toosee podsumowanie hello różnych ładowania tootutorials procesy i łącza.

tooplan migracji danych z programu SQL Server tooSQL hurtowni danych, zobacz hello [Omówienie migracji][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Użyj usług Integration Services (SSIS)
Jeśli korzystasz już z tooload pakietów Integration Services (SSIS) do programu SQL Server, należy zaktualizować toouse Twojego pakiety programu SQL Server jako hello źródła i magazynu danych SQL jako miejsce docelowe hello. Jest to szybki i łatwy toodo i jest dobrym rozwiązaniem, jeśli nie chcesz toomigrate Twojego ładowania przetwarzania danych toouse już w chmurze hello. zależnościami Hello jest obciążenia hello będzie przebiegać wolniej niż przy użyciu programu PolyBase, ponieważ ta SSIS nie przeprowadza obciążenia hello równolegle.

Podsumowanie procesu ładowania:

1. Popraw wystąpienia programu SQL Server Integration Services pakietu toopoint toohello hello źródła i bazy danych magazynu danych SQL hello hello docelowym.
2. Migrowanie tooSQL Twojego schematu magazynu danych, jeśli nie jest już.
3. Zmień mapowanie hello w pakietach Użyj tylko typy danych hello, które są obsługiwane przez usługi SQL Data Warehouse.
4. Planowanie i uruchamianie hello pakietu.

Samouczek, zobacz [ładowanie danych z programu SQL Server tooAzure magazynu danych SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Przy użyciu programu AZCopy (zalecane dla < 10 TB danych)
Jeśli rozmiar danych jest < 10 TB, można eksportować dane hello z pliki tooflat programu SQL Server, kopiowanie magazynu obiektów blob tooAzure pliki hello i następnie użyj programu PolyBase tooload hello danych do usługi SQL Data Warehouse

Podsumowanie procesu ładowania:

1. Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server.
2. Użyj hello AZCopy narzędzia wiersza polecenia toocopy danych z magazynu obiektów blob tooAzure plików prostych.
3. Użyj programu PolyBase tooload do usługi SQL Data Warehouse.

Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Użyj narzędzia bcp
Jeśli masz niewielką ilość danych można użyć narzędzia bcp tooload bezpośrednio do usługi Azure SQL Data Warehouse.

Podsumowanie procesu ładowania:

1. Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server.
2. Użyj narzędzia bcp tooload danych z płaski plików bezpośrednio tooSQL hurtowni danych.

Samouczek, zobacz [ładowanie danych z programu SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Użyj importu/eksportu (zalecane dla > 10 TB danych)
Jeśli rozmiar danych jest > 10 TB, toomove go tooAzure, firma Microsoft zaleca użycie naszych dysku wysyłania usługi [importu/eksportu][Import/Export]. 

Podsumowanie procesu ładowania

1. Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server na dyskach możliwej.
2. Należy najpierw wydać hello tooMicrosoft dysków.
3. Microsoft ładuje hello dane do magazynu danych SQL

## <a name="load-from-hdinsight"></a>Ładowanie z usługi HDInsight
Magazyn danych SQL obsługuje ładowanie danych z usługi HDInsight przy użyciu programu PolyBase. proces Hello jest hello taki sam jak podczas ładowania danych z magazynu obiektów Blob Azure - przy użyciu programu PolyBase tooconnect tooHDInsight tooload danych. 

### <a name="1-use-polybase-and-t-sql"></a>1. Użyj programu PolyBase i T-SQL
Podsumowanie procesu ładowania:

1. Przenieś tooHDInsight Twoje dane i zapisze go w plikach tekstowych ORC lub Parquet format.
2. Skonfiguruj obiekty zewnętrznego w lokalizacji hello toodefine SQL Data Warehouse i format danych hello.
3. Równolegle danych hello tooload polecenia T-SQL do nowej tabeli bazy danych.

Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Zalecenia
Wiele naszych partnerów ma ładowania rozwiązania. toofind się więcej, zobacz listę naszych [rozwiązania partnerów][solution partners]. 

Jeśli dane pochodzące ze źródłem danych nierelacyjnych i tooload go do danych SQL można magazynu należy tootransform go do wierszy i kolumn przed rozpoczęciem ładowania. Witaj przekształcone dane nie wymaga toobe przechowywane w bazie danych, mogą być przechowywane w plikach tekstowych.

Tworzenie statystyk na nowo załadowanych danych. Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.  W kolejności tooget hello najlepszą wydajność zapytań należy najpierw załadować toocreate statystyki dla wszystkich kolumn wszystkich tabel po hello lub każdej istotnej zmianie występują w danych hello.  Aby uzyskać więcej informacji, zobacz [statystyki][Statistics].

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz hello [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
