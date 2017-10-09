---
title: "aaaMove tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Tworzenie tabeli SQL i załadować tooSQL danych tabeli"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Przenoszenie danych tooan bazy danych SQL Azure dla usługi Azure Machine Learning
W tym temacie opisano opcje hello do przenoszenia danych z plików prostych (w formatach CSV lub TSV) albo z danych przechowywanych w bazie danych Azure SQL tooan programu SQL Server lokalne. Te zadania dla ruchu danych w chmurze toohello są częścią hello proces nauki danych zespołu.

Dla tematu przedstawiono hello Opcje przenoszenia danych tooan lokalnego programu SQL Server do uczenia maszynowego, zobacz [przenoszenia danych tooSQL serwera na maszynie wirtualnej platformy Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

następujące Hello **menu** łączy tootopics, które opisują sposób tooingest danych w środowisku docelowym, gdzie hello dane mogą być przechowywane i przetwarzane podczas hello zespołu danych nauki procesu (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Witaj Poniższa tabela zawiera podsumowanie hello Opcje przenoszenia danych tooan bazy danych SQL Azure.

| <b>ŹRÓDŁO</b> | <b>Miejsce docelowe: Baza danych Azure SQL</b> |
| --- | --- |
| <b>Plik prosty (CSV lub sformatowany TSV)</b> |<a href="#bulk-insert-sql-query">Zapytanie SQL wstawiania zbiorczego |
| <b>Lokalny serwer SQL</b> |1. <a href="#export-flat-file">TooFlat eksportu pliku<br> 2. <a href="#insert-tables-bcp">Kreator migracji bazy danych SQL<br> 3. <a href="#db-migration">Baza danych kopii zapasowej i przywracanie<br> 4. <a href="#adf">Fabryka danych Azure |

## <a name="prereqs"></a>Wymagania wstępne
procedury Hello opisane tutaj wymagają:

* **Subskrypcji platformy Azure**. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* **Konto magazynu Azure**. Używasz konta magazynu Azure do przechowywania danych hello w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu. Po utworzeniu konta magazynu hello, musisz mieć konto hello tooobtain się, że klucz używany tooaccess hello magazynu. Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Dostęp tooan **bazy danych SQL Azure**. Jeśli baza danych SQL Azure, należy skonfigurować [wprowadzenie do korzystania z bazy danych SQL Azure Microsoft](../sql-database/sql-database-get-started.md) informacje na temat sposobu tooprovision nowe wystąpienie bazy danych SQL Azure.
* Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie. Aby uzyskać instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

**Dane**: procesy migracji hello przedstawiono przy użyciu hello [dataset taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/). Witaj taksówki NYC zestaw danych zawiera informacje na temat danych podróży i targach i jest dostępny w magazynie obiektów blob platformy Azure: [danych taksówki NYC](http://www.andresmh.com/nyctaxitrips/). Przykładowe i opis te pliki znajdują się w [opis zestawu danych rund taksówki NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Można dostosować hello procedury opisane tutaj tooa zbiór danych użytkownika lub wykonaj kroki hello, zgodnie z opisem przy użyciu hello taksówki NYC zestawu danych. tooupload hello dataset taksówki NYC do lokalnej bazy danych programu SQL Server, wykonaj procedurę hello opisane w temacie [zbiorczego importowania danych do bazy danych serwera SQL](machine-learning-data-science-process-sql-walkthrough.md#dbload). Te instrukcje dotyczą programu SQL Server na maszynie wirtualnej platformy Azure, ale hello procedurę przekazywania toohello lokalnego programu SQL Server jest hello takie same.

## <a name="file-to-azure-sql-database"></a>Przenoszenie danych z bazy danych Azure SQL tooan źródło pliku prostego
Dane plików prostych (formacie CSV lub TSV) może być przeniesiony tooan bazy danych Azure SQL za pomocą kwerendy SQL wstawiania zbiorczego.

### <a name="bulk-insert-sql-query"></a>Zapytanie SQL wstawiania zbiorczego
kroki Hello hello procedury przy użyciu hello zapytania SQL wstawiania zbiorczego są podobne toothose omówione w sekcjach hello do przenoszenia danych z pliku prostego tooSQL źródłowego serwera na maszynie Wirtualnej platformy Azure. Aby uzyskać więcej informacji, zobacz [zapytania SQL wstawiania zbiorczego](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Przenoszenie danych z lokalną bazą danych Azure SQL tooan dla programu SQL Server
Jeśli hello źródło danych jest przechowywany w lokalnym serwerze SQL, istnieją różne możliwości przenoszenia hello danych tooan bazy danych Azure SQL:

1. [TooFlat eksportu pliku](#export-flat-file)
2. [Kreator migracji bazy danych SQL](#insert-tables-bcp)
3. [Baza danych kopii zapasowej i przywracanie](#db-migration)
4. [Azure Data Factory](#adf)

Hello hello pierwsze trzy kroki są podobne jak w sekcjach toothose [przenoszenia danych tooSQL serwera na maszynie wirtualnej platformy Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) obejmujących te same procedury. Łącza toohello odpowiednich części tego tematu znajdują się w hello, postępując zgodnie z instrukcjami.

### <a name="export-flat-file"></a>TooFlat eksportu pliku
kroki tego Eksportowanie pliku prostego tooa Hello są podobne toothose omówione w [wyeksportować tooFlat pliku](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Kreator migracji bazy danych SQL
Witaj kroki do używania hello Kreator migracji bazy danych SQL są podobne toothose objęte [Kreatora migracji bazy danych SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Baza danych kopii zapasowej i przywracanie
Witaj kroki dotyczące korzystania z bazy danych kopii zapasowej i przywracania są podobne toothose objęte [bazy danych kopii zapasowej i przywracania](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Fabryka danych Azure
Witaj procedurę przenoszenia danych tooan bazy danych SQL Azure z fabryki danych Azure (ADF) znajduje się w temacie hello [przenoszenia danych z lokalnego tooSQL serwera SQL Azure z fabryką danych Azure](machine-learning-data-science-move-sql-azure-adf.md). W tym temacie przedstawiono sposób toomove danych z lokalnego tooan bazy danych programu SQL Server Azure SQL bazy danych za pomocą usługi Azure Blob Storage przy użyciu fabryki danych AZURE.

Należy rozważyć użycie ADF, gdy dane potrzeb toobe stale migracji w scenariuszu hybrydowym, który uzyskuje dostęp do swoich lokalnych zasobów w chmurze i danych hello jest nietransakcyjnego lub wymaga modyfikacji toobe lub logiki biznesowej dodano tooit podczas jej migrowania. ADF umożliwia hello planowania i monitorowania zadań przy użyciu prostych skryptów JSON, które zarządzają hello przepływu danych w regularnych odstępach czasu. ADF ma również innych funkcji, takich jak obsługa złożonych operacji.
