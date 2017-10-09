---
title: "aaaAdd odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd odporność na uszkodzenia w przypadku działania kopiowania fabryki danych Azure przez pominięcie niezgodne wierszy podczas kopiowania"
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
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="6a396-103">Dodaj odporność na uszkodzenia w przypadku działania kopiowania przez pominięcie niezgodne wierszy</span><span class="sxs-lookup"><span data-stu-id="6a396-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="6a396-104">Fabryka danych Azure [działanie kopiowania](data-factory-data-movement-activities.md) oferuje dwa sposoby toohandle niezgodne wierszy podczas kopiowania danych między źródłowy i odbiorczy magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="6a396-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="6a396-105">Możesz przerwać i niepowodzenie kopiowania hello działanie w przypadku niezgodnych danych napotkało (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="6a396-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="6a396-106">Można kontynuować toocopy wszystkich danych hello odporności na uszkodzenia i pomijanie niezgodne dane wierszy.</span><span class="sxs-lookup"><span data-stu-id="6a396-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="6a396-107">Ponadto możesz zalogować się niezgodny wierszy hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a396-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="6a396-108">Można następnie zbadać hello dziennika toolearn hello Przyczyna niepowodzenia hello, Usuń dane hello na powitania źródła danych i spróbuj ponownie hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6a396-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="6a396-109">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="6a396-109">Supported scenarios</span></span>
<span data-ttu-id="6a396-110">Działanie kopiowania obsługuje trzy scenariusze wykrywanie, pomijanie i rejestrowanie danych niezgodne:</span><span class="sxs-lookup"><span data-stu-id="6a396-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="6a396-111">**Niezgodność między hello źródłowego typu danych i typ macierzysty ujścia hello**</span><span class="sxs-lookup"><span data-stu-id="6a396-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="6a396-112">Na przykład: kopiowanie danych z pliku CSV w tooa magazynu obiektów Blob SQL bazy danych z definicji schematu, która zawiera trzy **INT** kolumny o typie.</span><span class="sxs-lookup"><span data-stu-id="6a396-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="6a396-113">Witaj wierszy pliku CSV, które zawierają dane liczbowe, takich jak `123,456,789` została pomyślnie skopiowana toohello ujścia magazynu.</span><span class="sxs-lookup"><span data-stu-id="6a396-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="6a396-114">Jednak hello wiersze zawierające wartości nieliczbowe, takich jak `123,456,abc` zostały wykryte jako niezgodna ale są pomijane.</span><span class="sxs-lookup"><span data-stu-id="6a396-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="6a396-115">**Niezgodność hello liczby kolumn między hello źródłowy i odbiorczy hello**</span><span class="sxs-lookup"><span data-stu-id="6a396-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="6a396-116">Na przykład: kopiowanie danych z pliku CSV w tooa magazynu obiektów Blob SQL bazy danych z definicji schematu, który zawiera sześć kolumn.</span><span class="sxs-lookup"><span data-stu-id="6a396-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="6a396-117">Witaj pliku CSV, który wierszy zawierających sześć kolumn została pomyślnie skopiowana toohello ujścia magazynu.</span><span class="sxs-lookup"><span data-stu-id="6a396-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="6a396-118">wiersze pliku CSV Hello, które zawierają więcej lub mniej niż sześć kolumn są wykrywane niezgodne i są pomijane.</span><span class="sxs-lookup"><span data-stu-id="6a396-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="6a396-119">**Naruszenia dotyczącego klucza podstawowego podczas zapisywania tooa relacyjnej bazy danych**</span><span class="sxs-lookup"><span data-stu-id="6a396-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="6a396-120">Na przykład: kopiowanie danych z bazy danych programu SQL server tooa SQL.</span><span class="sxs-lookup"><span data-stu-id="6a396-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="6a396-121">W bazie danych SQL zbiornika hello jest zdefiniowany klucz podstawowy, ale żaden klucz podstawowy jest zdefiniowany w hello źródła programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="6a396-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="6a396-122">Hello zduplikowane wiersze, które istnieją w źródle hello nie może być zbiornika toohello skopiowane.</span><span class="sxs-lookup"><span data-stu-id="6a396-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="6a396-123">Działanie kopiowania kopiuje tylko hello pierwszy wiersz hello źródła danych do zbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="6a396-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="6a396-124">Witaj źródła kolejnych wierszy, które zawierają hello zduplikowane wartości klucza podstawowego są wykrywane niezgodne i są pomijane.</span><span class="sxs-lookup"><span data-stu-id="6a396-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="6a396-125">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="6a396-125">Configuration</span></span>
<span data-ttu-id="6a396-126">Witaj poniższym przykładzie przedstawiono tooconfigure definicji JSON, pomijanie hello niezgodne wierszy w przypadku działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="6a396-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="6a396-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6a396-127">Property</span></span> | <span data-ttu-id="6a396-128">Opis</span><span class="sxs-lookup"><span data-stu-id="6a396-128">Description</span></span> | <span data-ttu-id="6a396-129">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6a396-129">Allowed values</span></span> | <span data-ttu-id="6a396-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a396-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6a396-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="6a396-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="6a396-132">Włącz pomijanie niezgodne wierszy podczas kopiowania lub nie.</span><span class="sxs-lookup"><span data-stu-id="6a396-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="6a396-133">True</span><span class="sxs-lookup"><span data-stu-id="6a396-133">True</span></span><br/><span data-ttu-id="6a396-134">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="6a396-134">False (default)</span></span> | <span data-ttu-id="6a396-135">Nie</span><span class="sxs-lookup"><span data-stu-id="6a396-135">No</span></span> |
| <span data-ttu-id="6a396-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="6a396-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="6a396-137">Grupy właściwości, które mogą być określone, kiedy mają niezgodne wierszy hello toolog.</span><span class="sxs-lookup"><span data-stu-id="6a396-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="6a396-138">Nie</span><span class="sxs-lookup"><span data-stu-id="6a396-138">No</span></span> |
| <span data-ttu-id="6a396-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="6a396-139">**linkedServiceName**</span></span> | <span data-ttu-id="6a396-140">Witaj połączonej usługi magazynu Azure toostore hello dziennika, który zawiera wiersze hello pominięte.</span><span class="sxs-lookup"><span data-stu-id="6a396-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="6a396-141">Nazwa Hello [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [element AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) połączonej usługi, która odwołuje się toohello magazynu wystąpienia, które mają plik dziennika hello toostore toouse.</span><span class="sxs-lookup"><span data-stu-id="6a396-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="6a396-142">Nie</span><span class="sxs-lookup"><span data-stu-id="6a396-142">No</span></span> |
| <span data-ttu-id="6a396-143">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="6a396-143">**path**</span></span> | <span data-ttu-id="6a396-144">Ścieżka Hello hello pliku dziennika, który zawiera hello pominięte wierszy.</span><span class="sxs-lookup"><span data-stu-id="6a396-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="6a396-145">Określ, które mają niezgodne dane hello toolog toouse ścieżki do magazynu obiektów Blob hello.</span><span class="sxs-lookup"><span data-stu-id="6a396-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="6a396-146">Jeśli ścieżka nie zostanie określona, usługa hello tworzy kontener dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6a396-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="6a396-147">Nie</span><span class="sxs-lookup"><span data-stu-id="6a396-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="6a396-148">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="6a396-148">Monitoring</span></span>
<span data-ttu-id="6a396-149">Po zakończeniu uruchamiania działania kopiowania hello, można wyświetlić hello Liczba pominiętych wierszy w sekcji monitorowanie hello:</span><span class="sxs-lookup"><span data-stu-id="6a396-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Monitor pominięte niezgodne wierszy](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="6a396-151">Jeśli skonfigurujesz toolog hello niezgodne wiersze pliku dziennika hello na tej ścieżce można znaleźć: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` w pliku dziennika hello, można zobaczyć hello wierszy, które zostały pominięte i hello główną przyczynę hello niezgodności.</span><span class="sxs-lookup"><span data-stu-id="6a396-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="6a396-152">Zarówno hello oryginalnych danych, jak i odpowiednie błąd hello są rejestrowane w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="6a396-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="6a396-153">Oto przykład zawartości pliku dziennika hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="6a396-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="6a396-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a396-154">Next steps</span></span>
<span data-ttu-id="6a396-155">toolearn więcej informacji na temat działania kopiowania fabryki danych Azure, zobacz [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6a396-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
