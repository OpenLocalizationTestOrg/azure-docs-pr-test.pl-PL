---
title: "Data Lake Store z innymi usługami Azure aaaIntegrating | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak Data Lake Store integruje się z innymi usługami platformy Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Integrating Data Lake Store with other Azure Services (Integracja usługi Data Lake Store z innymi usługami platformy Azure)
Azure Data Lake Store można używać w połączeniu z innymi usługami Azure tooenable szerszego zakresu scenariuszy. Hello artykule wymieniono hello usług, które można zintegrować z usługą Data Lake Store.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Użyj Data Lake Store z usługą Azure HDInsight
Umożliwia obsługę [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) klastrze korzystającym z usługi Data Lake Store jako magazyn hello zgodne z systemem plików HDFS. W tej wersji dla klastrów platformy Hadoop i Storm w systemach Windows i Linux, można użyć usługi Data Lake Store tylko jako dodatkowego magazynu. Takie klastry nadal używać usługi Azure Storage (WASB) jako hello domyślny magazyn. Jednak w przypadku klastrów HBase w systemach Windows i Linux, można użyć usługi Data Lake Store jako magazynu domyślne hello lub dodatkowego miejsca do magazynowania.

Aby uzyskać instrukcje dotyczące sposobu klastra tooprovision HDInsight z usługą Data Lake Store zobacz:

* [Udostępnić klastra usługi HDInsight przy użyciu portalu Azure usługi Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Udostępnianie klastra usługi HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Udostępnianie klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego magazynu za pomocą programu Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Użyj Data Lake Store z usługi Azure Data Lake Analytics
[Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-overview.md) pozwala toowork z danymi Big Data w skali chmury. Dynamicznie udostępnia zasoby i umożliwia terabajtów, a nawet eksabajtów danych, które mogą być przechowywane w wielu obsługiwanych źródeł danych, jednego z nich usługi Data Lake Store. Data Lake Analytics to specjalnie zoptymalizowana toowork z usługi Azure Data Lake Store - dostarczanie hello najwyższy poziom wydajności, przepływności i przetwarzania równoległego na potrzeby obciążeń danych big data.

Aby uzyskać instrukcje dotyczące toouse usługi Data Lake Analytics z usługą Data Lake Store, zobacz [wprowadzenie do usługi Data Lake Analytics przy użyciu usługi Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Użyj Data Lake — magazyn z fabryką danych Azure
Można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) tooingest dane z tabel Azure, baza danych SQL Azure, Magazyn danych SQL Azure, obiektach blob magazynu Azure i lokalnych baz danych. Trwa pierwszej klasie obywateli w hello ekosystemu platformy Azure, fabryki danych Azure mogą być używane tooorchestrate hello wprowadzanie danych z tych tooAzure źródła usługi Data Lake Store.

Aby uzyskać instrukcje dotyczące toouse fabryka danych Azure z usługą Data Lake Store, zobacz temat [przenieść tooand danych z usługi Data Lake Store przy użyciu fabryki danych](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Kopiowanie danych z obiektów blob magazynu Azure do usługi Data Lake Store
Azure Data Lake Store udostępnia narzędzie wiersza polecenia, AdlCopy, umożliwiającą toocopy danych z magazynu obiektów Blob Azure do konta usługi Data Lake Store. Aby uzyskać więcej informacji, zobacz [skopiować dane z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Kopiowanie danych między bazą danych SQL Azure i usługi Data Lake Store
Można użyć narzędzia Apache Sqoop tooimport i eksportowanie danych między bazą danych SQL Azure i usługi Data Lake Store. Aby uzyskać więcej informacji, zobacz [kopiowanie danych między Data Lake Store i bazy danych Azure SQL przy użyciu Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Użyj Data Lake Store z usługi analiza strumienia
Data Lake Store można użyć jako jeden z hello generuje toostore dane przesyłane strumieniowo przy użyciu usługi Azure Stream Analytics. Aby uzyskać więcej informacji, zobacz [strumienia danych z obiektu Blob magazynu Azure do usługi Data Lake Store za pomocą usługi Azure Stream Analytics](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Użyj Data Lake Store przy użyciu usługi Power BI
Możesz używać usługi Power BI tooimport danych z tooanalyze konta usługi Data Lake Store i wizualizacji danych hello. Aby uzyskać więcej informacji, zobacz [analizowanie danych w usłudze Data Lake Store za pomocą usługi Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Użyj Data Lake Store z wykazu danych
Możesz zarejestrować dane z usługi Data Lake Store hello wykrywalny w całej organizacji hello danych hello toomake Azure Data Catalog. Aby uzyskać więcej informacji, zobacz [zarejestrować dane z usługi Data Lake Store w usłudze Azure Data Catalog](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Użyj Data Lake Store z usług SQL Server Integration Services (SSIS)
Można użyć Menedżera połączeń hello Azure Data Lake Store w tooconnect SSIS pakietów SSIS z usługi Azure Data Lake Store. Aby uzyskać więcej informacji, zobacz [Użyj Data Lake Store z SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Użyj Data Lake Store z usługą Magazyn danych SQL
Program PolyBase tooload danych z usługi Azure Data Lake Store służy do usługi SQL Data Warehouse. Aby uzyskać więcej informacji, zobacz [Użyj Data Lake Store z usługą Magazyn danych SQL](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Wprowadzenie do usługi Data Lake Store za pomocą portalu](data-lake-store-get-started-portal.md)
* [Wprowadzenie do usługi Data Lake Store za pomocą programu PowerShell](data-lake-store-get-started-powershell.md)  

