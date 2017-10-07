---
title: "aaaMove tooor danych z magazynu obiektów Blob Azure za pomocą łączników SSIS | Dokumentacja firmy Microsoft"
description: "Przenieś tooor danych z magazynu obiektów Blob Azure za pomocą łączników SSIS."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Przenieś tooor danych z magazynu obiektów Blob Azure za pomocą łączników SSIS
Witaj [programu SQL Server Integration Services Feature Pack dla platformy Azure](https://msdn.microsoft.com/library/mt146770.aspx) zawiera składniki tooconnect tooAzure, transfer danych między Azure i lokalnego źródła danych i przetwarzania danych przechowywanych na platformie Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Gdy klienci przeniesione danych lokalnych w chmurze hello, ich do niego dostęp z dowolnej usługi Azure tooleverage hello pełną moc pakiet hello Azure technologii. Mogą być używane, na przykład w usłudze Azure Machine Learning lub w klastrze usługi HDInsight.

Zazwyczaj jest to być pierwsze hello hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) i [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) wskazówki.

Omówienie canonical scenariusze biznesowe tooaccomplish SSIS musi typowe w scenariuszy integracji danych hybrydowego, w temacie [zrobić więcej z programu SQL Server Integration Services Feature Pack dla platformy Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blogu.

> [!NOTE]
> Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
tooperform hello zadania opisane w tym artykule, musi mieć subskrypcję platformy Azure i skonfigurowane konto magazynu platformy Azure. Należy znać Twojego magazynu Azure konta nazwy i konta klucza tooupload lub pobierania danych.

* tooset się **subskrypcji platformy Azure**, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać instrukcje dotyczące tworzenia **konta magazynu** oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

Witaj toouse **łączniki SSIS**, należy pobrać:

* **SQL Server 2014 lub 2016 Standard (lub nowszej)**: instalacja zawiera SQL Server Integration Services.
* **Microsoft SQL Server 2014 lub 2016 integracji usług Feature Pack dla systemu Azure**: te mogą być pobierane, odpowiednio z hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) i [integracji programu SQL Server 2016 Usługi](https://www.microsoft.com/download/details.aspx?id=49492) stron.

> [!NOTE]
> SSIS jest instalowany z serwerem SQL, ale nie znajduje się w wersji Express hello. Informacje dotyczące poszczególnych aplikacji znajdują się w różnych wersjach programu SQL Server znajdują się w temacie [wersjach programu SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Materiałów szkoleniowych w sprawie SSIS, zobacz [ręce na szkolenia dotyczące SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Aby uzyskać informacje na temat tooget w górę i uruchomić przy użyciu SISS toobuild proste wyodrębniania, przekształcania i ładowania (ETL) pakietów, zobacz [SSIS samouczek: Tworzenie prostego pakietu ETL](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Pobierz taksówki NYC zestawu danych
Witaj przykład opisanej tutaj Użyj publicznie dostępnych zestawu danych--hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych. Witaj zestawu danych składa się z około 173 milionów taksówki było w NYC w roku hello 2013. Istnieją dwa typy danych: podróży szczegóły danych i taryfy danych. Ponieważ plik jest dostępny dla każdego miesiąca, mamy 24 plików we wszystkich, z których każdy jest nieskompresowane około 2GB.

## <a name="upload-data-tooazure-blob-storage"></a>Przekazywanie danych tooAzure obiektu blob magazynu
toomove danych przy użyciu hello SSIS funkcji pakietu z magazynu obiektów blob tooAzure lokalnymi, możemy użyć wystąpienia hello [ **zadań przekazania obiektu Blob Azure**](https://msdn.microsoft.com/library/mt146776.aspx), pokazano poniżej:

![Konfigurowanie danych nauki vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

Parametry Hello hello używa zadania są opisane w tym miejscu:

| Pole | Opis |
| --- | --- |
| **AzureStorageConnection** |Określa istniejącą Menedżera połączeń magazynu Azure lub tworzy nowy klucz, który odwołuje się kontem magazynu platformy Azure tooan wskazujące toowhere hello blob plików są obsługiwane. |
| **BlobContainer** |Określa nazwę hello kontenerze obiektów blob hello hello przekazać pliki jako obiekty BLOB. |
| **BlobDirectory** |Określa katalog blob hello przechowywania hello przekazany plik jako blokowych obiektów blob. katalog blob Hello jest wirtualnego strukturę hierarchiczną. Jeśli istnieje już obiekt blob hello, it ia zastąpione. |
| **LocalDirectory** |Określa hello katalog lokalny, który zawiera hello toobe pliki przekazywane. |
| **Nazwa pliku** |Określa nazwę filtru tooselect pliki hello wzorzec określonej nazwy. Na przykład MySheet\*xls\* zawiera pliki takie jak MySheet001.xls i MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Określa filtr przedziału czasu. Pliki zmodyfikowane po *TimeRangeFrom* i przed *TimeRangeTo* są uwzględniane. |

> [!NOTE]
> Witaj **AzureStorageConnection** poświadczenia wymagane toobe poprawne i hello **BlobContainer** musi istnieć przed próbą przeniesienia hello.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Pobierz dane z magazynu obiektów blob platformy Azure
toodownload danych z magazynu lokalnego tooon magazynu obiektów blob platformy Azure z SSIS, używając wystąpienia hello [zadań przekazania obiektu Blob Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Bardziej zaawansowanych scenariuszy SSIS Azure
Pakiet funkcji SSIS Hello umożliwia bardziej złożonych toobe przepływów obsługiwane przez opakowanie zadań jednocześnie. Na przykład hello obiektu blob można strumieniowego źródła danych bezpośrednio do klastra usługi HDInsight, której wyjście mogły zostać pobrane wstecz tooa obiektów blob, a następnie tooon lokalnego magazynu. SSIS można uruchamiać zadania Hive i Pig w klastrze usługi HDInsight za pomocą łączników SSIS dodatkowe:

* klaster skryptu Hive w usłudze Azure HDInsight z SSIS, użyj toorun [zadań Hive HDInsight Azure](https://msdn.microsoft.com/library/mt146771.aspx).
* skrypt programu Pig w usłudze Azure HDInsight klaster z SSIS, użyj toorun [Azure HDInsight Pig zadań](https://msdn.microsoft.com/library/mt146781.aspx).

