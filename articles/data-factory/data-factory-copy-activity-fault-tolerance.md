---
title: "Dodaj odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy podczas kopiowania"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="a6353-103">Dodaj odporność na uszkodzenia w przypadku działania kopiowania przez pominięcie niezgodne wierszy</span><span class="sxs-lookup"><span data-stu-id="a6353-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="a6353-104">Fabryka danych Azure [działanie kopiowania](data-factory-data-movement-activities.md) oferuje obsługi niezgodne wierszy, gdy kopiowanie danych między źródłowy i odbiorczy magazynów danych na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="a6353-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="a6353-105">Możesz przerwać i niepowodzenie kopiowania działanie w przypadku niezgodnych danych napotkało (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="a6353-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="a6353-106">Możesz skopiować wszystkie dane przez dodanie odporność na uszkodzenia i pomijanie niezgodne dane wierszy.</span><span class="sxs-lookup"><span data-stu-id="a6353-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="a6353-107">Ponadto możesz zalogować się niezgodne wiersze magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6353-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="a6353-108">Następnie można sprawdzić dziennik Dowiedz się przyczynę błędu, Usuń dane w źródle danych, a następnie ponów działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a6353-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a6353-109">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="a6353-109">Supported scenarios</span></span>
<span data-ttu-id="a6353-110">Działanie kopiowania obsługuje trzy scenariusze wykrywanie, pomijanie i rejestrowanie danych niezgodne:</span><span class="sxs-lookup"><span data-stu-id="a6353-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="a6353-111">**Niezgodność między typem źródła danych i typ macierzysty ujścia**</span><span class="sxs-lookup"><span data-stu-id="a6353-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="a6353-112">Na przykład: kopiowanie danych z pliku CSV w magazynie obiektów Blob do bazy danych SQL z definicji schematu, która zawiera trzy **INT** kolumny o typie.</span><span class="sxs-lookup"><span data-stu-id="a6353-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="a6353-113">Wiersze pliku CSV, które zawierają dane liczbowe, takie jak `123,456,789` są pomyślnie skopiowane do ujścia magazynu.</span><span class="sxs-lookup"><span data-stu-id="a6353-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="a6353-114">Jednak wiersze zawierające wartości innych niż alfanumeryczne, takie jak `123,456,abc` zostały wykryte jako niezgodna ale są pomijane.</span><span class="sxs-lookup"><span data-stu-id="a6353-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="a6353-115">**Niezgodność liczby kolumn między serwerem źródłowym a sink**</span><span class="sxs-lookup"><span data-stu-id="a6353-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="a6353-116">Na przykład: kopiowanie danych z pliku CSV w magazynie obiektów Blob do bazy danych SQL z definicji schematu, który zawiera sześć kolumn.</span><span class="sxs-lookup"><span data-stu-id="a6353-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="a6353-117">Wiersze pliku CSV, które zawierają sześć kolumn są została pomyślnie skopiowana do ujścia magazynu.</span><span class="sxs-lookup"><span data-stu-id="a6353-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="a6353-118">Wiersze pliku CSV, które zawierają więcej lub mniej niż sześć kolumn są wykryte jako niezgodne, są pomijane.</span><span class="sxs-lookup"><span data-stu-id="a6353-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="a6353-119">**Naruszenia dotyczącego klucza podstawowego podczas zapisywania relacyjnej bazy danych**</span><span class="sxs-lookup"><span data-stu-id="a6353-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="a6353-120">Na przykład: kopiowanie danych z programu SQL server z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a6353-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="a6353-121">W bazie danych SQL zbiornika jest zdefiniowany klucz podstawowy, ale taki klucz podstawowy jest zdefiniowany w programie SQL server źródła.</span><span class="sxs-lookup"><span data-stu-id="a6353-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="a6353-122">Zduplikowane wiersze, które istnieją w źródle nie można skopiować do ujścia.</span><span class="sxs-lookup"><span data-stu-id="a6353-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="a6353-123">Działanie kopiowania kopiuje tylko pierwszy wiersz źródła danych do ujścia.</span><span class="sxs-lookup"><span data-stu-id="a6353-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="a6353-124">Wiersze kolejnych źródła, które zawierają zduplikowane wartości klucza podstawowego są wykrywane niezgodne i są pomijane.</span><span class="sxs-lookup"><span data-stu-id="a6353-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="a6353-125">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="a6353-125">Configuration</span></span>
<span data-ttu-id="a6353-126">W poniższym przykładzie przedstawiono definicji JSON, aby skonfigurować pomijanie niezgodne wierszy w przypadku działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="a6353-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="a6353-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a6353-127">Property</span></span> | <span data-ttu-id="a6353-128">Opis</span><span class="sxs-lookup"><span data-stu-id="a6353-128">Description</span></span> | <span data-ttu-id="a6353-129">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="a6353-129">Allowed values</span></span> | <span data-ttu-id="a6353-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a6353-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a6353-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="a6353-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="a6353-132">Włącz pomijanie niezgodne wierszy podczas kopiowania lub nie.</span><span class="sxs-lookup"><span data-stu-id="a6353-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="a6353-133">True</span><span class="sxs-lookup"><span data-stu-id="a6353-133">True</span></span><br/><span data-ttu-id="a6353-134">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="a6353-134">False (default)</span></span> | <span data-ttu-id="a6353-135">Nie</span><span class="sxs-lookup"><span data-stu-id="a6353-135">No</span></span> |
| <span data-ttu-id="a6353-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="a6353-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="a6353-137">Grupy właściwości, które można określić, kiedy mają być rejestrowane niezgodne wierszy.</span><span class="sxs-lookup"><span data-stu-id="a6353-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="a6353-138">Nie</span><span class="sxs-lookup"><span data-stu-id="a6353-138">No</span></span> |
| <span data-ttu-id="a6353-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="a6353-139">**linkedServiceName**</span></span> | <span data-ttu-id="a6353-140">Połączonej usługi magazynu Azure do przechowywania dziennika, który zawiera wiersze zostało pominięte.</span><span class="sxs-lookup"><span data-stu-id="a6353-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="a6353-141">Nazwa [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [element AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) połączonej usługi, która odwołuje się do wystąpienia magazynu, który ma być używany do przechowywania plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="a6353-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="a6353-142">Nie</span><span class="sxs-lookup"><span data-stu-id="a6353-142">No</span></span> |
| <span data-ttu-id="a6353-143">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="a6353-143">**path**</span></span> | <span data-ttu-id="a6353-144">Ścieżka pliku dziennika, który zawiera wiersze zostało pominięte.</span><span class="sxs-lookup"><span data-stu-id="a6353-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="a6353-145">Określ ścieżki do magazynu obiektów Blob, który ma być używany do rejestrowania danych niezgodne.</span><span class="sxs-lookup"><span data-stu-id="a6353-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="a6353-146">Jeśli ścieżka nie zostanie określona, usługa tworzy kontener.</span><span class="sxs-lookup"><span data-stu-id="a6353-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="a6353-147">Nie</span><span class="sxs-lookup"><span data-stu-id="a6353-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="a6353-148">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="a6353-148">Monitoring</span></span>
<span data-ttu-id="a6353-149">Po zakończeniu uruchamiania działania kopiowania, można wyświetlić Liczba pominiętych wierszy w sekcji monitorowania:</span><span class="sxs-lookup"><span data-stu-id="a6353-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Monitor pominięte niezgodne wierszy](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="a6353-151">Jeśli konfigurujesz dziennika niezgodne wiersze, można znaleźć pliku dziennika na tej ścieżce: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` w pliku dziennika, możesz wyświetlać wiersze, które zostały pominięte i przyczynę niezgodności.</span><span class="sxs-lookup"><span data-stu-id="a6353-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="a6353-152">Zarówno oryginalnych danych, jak i odpowiednie błąd są rejestrowane w pliku.</span><span class="sxs-lookup"><span data-stu-id="a6353-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="a6353-153">Oto przykład zawartości pliku dziennika jest następujący:</span><span class="sxs-lookup"><span data-stu-id="a6353-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="a6353-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6353-154">Next steps</span></span>
<span data-ttu-id="a6353-155">Aby dowiedzieć się więcej na temat działania kopiowania fabryki danych Azure, zobacz [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a6353-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>